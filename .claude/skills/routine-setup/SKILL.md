---
name: routine-setup
description: Register (or idempotently re-apply) a feedradar Claude Routine from its committed YAML via the claude.ai RemoteTrigger API. Claude Code only.
argument-hint: [<routine-yaml-path>] [--update] [--no-verify]
---

# routine-setup

Register a feedradar `pipeline` / `watch` routine on Claude Routines **from its
committed YAML** (the source of truth), automating the flow that otherwise
requires hand-assembling the RemoteTrigger API body, converting the cron to
UTC, writing the `routine_id` back, and walking the user through the Web-UI
steps.

**Claude Code only.** This skill uses the `RemoteTrigger` tool (the claude.ai
`/v1/code/triggers` API). That tool is available **only inside a Claude Code
session** — the OAuth token is injected in-process by the harness. It is NOT a
`radar` CLI capability, so this skill does not work under Codex / Gemini /
Copilot. (That is also why feedradar's engine SKILLs, which are 4-agent-common,
do not cover registration — this is intentionally Claude-specific, which is fine
because Claude Routines is a Claude product.)

The routine YAML (`.claude/routines/<name>.yaml`, produced by
`radar routine generate <type> --prompt-mode bootstrap`) stays the source of
truth: the registered routine runs a short **bootstrap prompt** that reads the
YAML's `instructions:` block at run time, so later edits to the procedure
propagate by commit alone — no Web-UI re-paste.

## Hard limits — these stay manual (Web UI only)

- **`Allow unrestricted branch pushes` toggle**: required for
  `--output-mode auto-merge`. The create API **rejects it (HTTP 400,
  `Extra inputs are not permitted`)** — a human must flip it once in the Web UI.
- **Deleting a routine**: Web UI only.

This skill collapses everything else into one command, leaving the user at most
**one toggle** (and only for auto-merge routines).

## Steps

1. Resolve `$ARGUMENTS`. Default routine YAML path is
   `.claude/routines/feedradar-pipeline.yaml`. On `--help`, print this usage and
   stop. `--update` forces the update path (step 6); `--no-verify` skips step 9.

2. **Read the routine YAML** (source of truth) and extract:
   `name`, `model`, `repositories[0]`, the scheduled trigger's `cron` +
   `timezone`, `permissions.allow_unrestricted_git_push` (→ is this auto-merge?),
   `routine_id`, `status`. Then read `sources/*.yaml` and collect the feed hosts
   (for the network allowlist note). Use `yq` for extraction, e.g.:

   ```bash
   F=.claude/routines/feedradar-pipeline.yaml
   yq -r '.name, .model, .repositories[0], (.triggers[]|select(.type=="scheduled")|.cron + " | " + .timezone), .routine_id, .status, .permissions.allow_unrestricted_git_push' "$F"
   ```

3. **Build the bootstrap prompt** for the API `message.content` (do NOT
   regenerate the YAML — that would reset `routine_id` / `status`). Construct it
   inline:

   ```text
   あなたはスケジュール実行される `<name>` routine です（リポジトリ <owner/repo>）。
   完全自律実行で、プロンプトに答える人間はいません。すべての判断を自分で行ってください。

   セットアップ: `gh` が未インストールなら実行する:
     sudo apt-get update -qq && sudo apt-get install -y -qq gh

   その後、リポルートの `<yaml-path>` を Read し、その top-level `instructions:`
   ブロックを そのまま忠実に 実行してください（自己完結しています）。
   ```

   Notes baked into this prompt: install `gh` (the cloud VM lacks it), and read
   the YAML. **Output language follows the workspace `radar.config.yaml`
   (`locale:`)**, not this prompt — keep a committed `radar.config.yaml` with
   `locale: ja` (etc.) for non-English reports. Match the prompt language to the
   YAML's `--lang`.

4. **Convert the schedule to UTC and confirm.** The API `cron_expression` is
   **UTC**; the YAML cron is in its `timezone`. Convert and confirm with the user
   via `AskUserQuestion`, e.g. "6:00 Asia/Tokyo = 21:00 UTC → `0 21 * * *`".
   Minimum interval is 1 hour (sub-hourly is rejected).

5. **Choose the environment.** `environment_id` is a claude.ai resource, not in
   the YAML. List existing ones and reuse one that already reaches the feed hosts
   from step 2:

   ```text
   RemoteTrigger {action: "list"}
   ```

   Confirm the environment with `AskUserQuestion`. (For arbitrary-host feeds an
   `anthropic_cloud` env with the right network access is required; a "Trusted"
   env will 403 on non-allowlisted hosts.)

6. **Create or update** with the `RemoteTrigger` tool, body per the shape below:
   - YAML `routine_id` empty → `action: "create"` with `enabled: false`.
   - `routine_id` set and `action: "get"` returns it → `action: "update"`
     (idempotent re-apply of cron / model / env / prompt). With bootstrap mode,
     `instructions:` edits do NOT need re-apply (auto-followed at run time);
     update is for the OTHER fields.
   - **Omit `allow_unrestricted_git_push`** from the body (it 400s — set via the
     Web-UI toggle in step 8). Generate a fresh UUID for `events[].data.uuid`
     (`cat /proc/sys/kernel/random/uuid`).

7. **Write back** the returned `routine_id` and set `status: active` in the YAML,
   then land it via a PR (the repo's `main` is usually branch-protected): create
   a `chore/...` branch, commit, `gh pr create`, squash-merge. Edit the two
   lines precisely (preserve comments) rather than `yq -i` (which can drop them).

8. **Hand off the one human step.** Print the routine link
   `https://claude.ai/code/routines/<routine_id>`. For **auto-merge** routines,
   ask the user to flip **`Allow unrestricted branch pushes` ON**, then
   `RemoteTrigger {action:"get"}` and confirm
   `job_config.ccr.sources[].git_repository.allow_unrestricted_git_push: true`.
   For `--output-mode pr` routines this toggle is **not** needed (they only open
   PRs) — skip it.

9. **Enable + verify** (unless `--no-verify`): `RemoteTrigger {action:"update",
   body:{"enabled":true}}`, then `{action:"run"}`. Poll the repo (`gh pr list`,
   `git ls-remote --heads origin 'claude/*'`, `origin/main`) for the routine's
   `claude/pipeline/*` PR + auto-merge, or report the clean no-op state update.
   Confirm any generated report is in the expected language.

## RemoteTrigger create body shape

```json
{
  "name": "<name>",
  "cron_expression": "<UTC cron>",
  "enabled": false,
  "job_config": { "ccr": {
    "environment_id": "<env_...>",
    "session_context": {
      "model": "<model>",
      "sources": [{ "git_repository": { "url": "https://github.com/<owner>/<repo>" } }],
      "allowed_tools": ["Bash","Read","Write","Edit","Glob","Grep","WebFetch","WebSearch"]
    },
    "events": [{ "data": {
      "uuid": "<fresh lowercase v4 uuid>",
      "session_id": "",
      "type": "user",
      "parent_tool_use_id": null,
      "message": { "role": "user", "content": "<bootstrap prompt from step 3>" }
    }}]
  }}
}
```

For a one-time run, replace `cron_expression` with `run_once_at`
(RFC3339 UTC, future). Do NOT place `allow_unrestricted_git_push` anywhere in
this body.

## Notes

- **Complements, does not replace, Claude Code's built-in `schedule` skill.**
  `schedule` is generic; this skill is YAML-driven and encodes feedradar
  conventions: the bootstrap prompt, the network allowlist from `sources/`, the
  `--max-items` cost cap, and the `routine_id` write-back.
- **Cost cap**: the routine's blast radius is bounded by `--max-items` baked into
  the YAML `instructions:`. Never raise it just to register a bigger run.
- **Auto-merge routines** push `claude/pipeline/*` and squash-merge to `main`.
  Ensure the repo permits that (and `delete_branch_on_merge: true` to avoid
  orphan branches).
- **Language**: `--lang` localizes the generated YAML's prose; report/output
  language is driven by `radar.config.yaml` `locale:` (host-agent payloads carry
  the locale output directive). Keep both consistent.
- If `RemoteTrigger create` returns HTTP 400 mentioning an unexpected input,
  the most likely cause is `allow_unrestricted_git_push` in the body — remove it
  and use the Web-UI toggle (step 8).
