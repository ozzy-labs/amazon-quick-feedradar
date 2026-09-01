---
id: 20260831_amazon-quick-aws-agent-registry-agents-and-mcp-servers-now-available-in-a_v1
itemIds:
  - aws-agent-registry-agents-and-mcp-server-9166e0fd
agent: claude-code
templateId: default
createdAt: 2026-09-01T21:15:00.000Z
updatedAt: null
reviewedAt: 2026-09-01T21:17:00.000Z
reviewedBy: claude-code
---

# AWS Agent Registry agents and MCP servers now available in Amazon Quick

## 要約

Amazon Quick が **AWS Agent Registry** との統合を発表し、組織の Agent Registry に登録された **MCP サーバー** と **agent** を Quick 内から検索・有効化できるようになった。これにより、Bedrock AgentCore で構築された技術チーム側のリソースを、ビジネスユーザーが Quick のワークスペースから直接 chat / agents / apps / flows / deep research の各機能で利用可能となる。対応リージョンは US East (N. Virginia)、US West (Oregon)、Asia Pacific (Sydney)、Asia Pacific (Tokyo)、Europe (Frankfurt)、Europe (Ireland) の 6 リージョン。

## 詳細

- **何が新しい / 変わった**
  - Amazon Quick から AWS Agent Registry に登録されている agent および MCP server の **discovery** と **有効化 (enable)** が可能になった。
  - 有効化時に接続情報（credentials / endpoint 等）は registry から自動投入されるため、ユーザーが手動で接続設定を書き起こす必要がない。
  - 有効化したリソースはチームで共有でき、Quick の chat・agents・apps・flows・deep research 全機能で参照できる。
  - 技術チーム（Bedrock AgentCore で agent / MCP server を構築）とビジネスユーザー（Quick で日次業務を実施）の **接続ギャップを埋める** ポジショニングとして打ち出されている。

- **既存ワークフローへの影響**
  - Bedrock AgentCore で既に agent / MCP server を構築済みの組織にとっては、これまで Quick ユーザーに使わせるために別途接続を構成していた作業が不要になる。
  - Quick 単独ユーザー観点ではオプトイン（admin が明示的に Agent Registry を接続しない限り既存動作は変わらない）。
  - Amazon Quick と Amazon Bedrock AgentCore の **両方が利用可能なリージョン** のみが対象。日本ユーザーは Tokyo リージョンで利用可能。
  - 開始手順: Amazon Quick admin console → **Manage account** → **Permissions** → **AWS Agent Registry** で registry を接続。

- **関連リソース**
  - Amazon Quick Integrations documentation: `https://docs.aws.amazon.com/quick/latest/userguide/aws-agent-registry-integration.html`
  - AWS Agent Registry documentation: `https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/registry.html`

## 出典

- 原文: https://aws.amazon.com/about-aws/whats-new/2026/08/aws-agent-registry-agents-mcp-servers-quick/
- 関連: https://docs.aws.amazon.com/quick/latest/userguide/aws-agent-registry-integration.html
- 関連: https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/registry.html

## レビュー (claude-code, 2026-09-01T21:17:00.000Z)

### 事実関係

- 対応リージョン 6 拠点 (N. Virginia / Oregon / Sydney / Tokyo / Frankfurt / Ireland) と、開始手順 (admin console → Manage account → Permissions → AWS Agent Registry) は原文の記述と一致。
- 「Amazon Bedrock AgentCore で作られた agent / MCP server が Quick 側から利用可能」という結線関係も原文の説明どおり。
- レポートは `radar` の pipeline routine 内で self-session として書かれたため、`--agent` の cross 化はされていない (research/review とも claude-code)。事実誤認はないが、単一エージェント視点である点は運用上の前提として認識しておくべき。

### 抜け

- **課金 / コスト** に関する言及が原文にも本レポートにも無い。Bedrock AgentCore・Quick 双方の既存料金体系に閉じるのか、Registry 連携自体に追加課金があるのかは公式 docs 側での確認が必要 (本レポートでは URL のみ掲載)。
- 有効化した agent / MCP server を **どの Quick ロール** が実行できるか (admin のみ / share 先の end-user 全員 / etc.) の粒度が本文で触れられていない。「共有できる」以上の権限モデルは docs で追う必要がある。
- MCP server / agent の **バージョン管理** (registry 側で更新された場合の Quick 側の追従挙動) についての言及なし。運用上重要になる可能性がある。

### 憶測 / 主観の混入

- 「技術チームとビジネスユーザーの接続ギャップを埋めるポジショニング」は原文自体の narrative の要約であり、レポート側の憶測ではない。指摘なし。

### 出典の妥当性

- 一次情報 (AWS What's New) と関連 docs (Quick 統合ガイド + Bedrock AgentCore registry ガイド) の 2 系統が引用されており、二次情報のみに依拠していない。妥当。
