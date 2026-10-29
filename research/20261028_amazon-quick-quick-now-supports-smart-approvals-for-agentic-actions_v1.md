---
id: 20261028_amazon-quick-quick-now-supports-smart-approvals-for-agentic-actions_v1
itemIds:
  - quick-now-supports-smart-approvals-for-a-331dcf02
agent: claude-code
templateId: default
createdAt: 2026-10-29T21:15:00.000Z
updatedAt: null
reviewedAt: 2026-10-29T21:16:00.000Z
reviewedBy: claude-code
---

# Quick now supports smart approvals for agentic actions

## 要約

Amazon Quick は、agentic アクション向けの承認レイヤ "smart approvals" の提供を 2026-10-28 に発表した。別途用意された classifier モデルがエージェントのアクションをユーザーのリクエストに照らして評価し、ルーチン作業は自動承認、影響の大きい操作だけをユーザー確認に回す。全ユーザーで既定 ON、管理者はカスタム権限で利用対象を制御でき、CloudTrail に承認レビューと設定変更の両方が記録される。

## 詳細

- **何が新しくなったか**
  - Amazon Quick のエージェント実行経路に smart approvals (classifier による自動 / 手動振り分け) が追加され、個々のアクションに毎回承認を求めることで発生していた "approval fatigue" を軽減する設計になった。
  - 自動承認の対象はユーザー設定が "ask (毎回確認)" のアクションに限定される。既存ポリシーが優先され、deny は常に deny のまま、smart approvals が新たな権限を付与することはない。
  - 以下は高インパクトとして常にユーザーレビューに回る: 組織外へのコンテンツ送信、権限変更、コンテンツ削除、支払い、ユーザーが要求した範囲を超えるアクション。
  - 各自動承認は "レビューされたまさにそのアクション 1 件" にしか効かず、将来の同種アクションに自動的に拡張されない。レビューが失敗 / タイムアウトした場合はユーザーに回される。

- **既存ワークフローへの影響**
  - 全ユーザーで既定 ON のため、Amazon Quick で agentic 機能を使っている既存会話・スケジュール実行の挙動が本日以降変わる可能性がある (ルーチン操作のプロンプト頻度が減る)。ユーザーは chat options から自分の会話・scheduled run について個別にオフにできる。
  - 管理者は custom permissions で「smart approvals を使えるユーザー」を絞れる。コンプライアンス要件で "すべてのアクションに人間承認" を厳格に求める環境では、管理者側で明示的にオフにする運用変更が必要になる。
  - CloudTrail に (a) smart approvals が行った各アクションレビュー、(b) ユーザーごとの smart approvals 設定変更、の両方が記録されるため、監査証跡の列は増えるが、監査基盤側のクエリ・保存要件を見直す必要がある。

- **技術・運用上の注意**
  - classifier モデルのアーキテクチャ・評価指標・精度 (false approve / false refer のレート) は本発表では開示されていない。ユーザーガイド側で追補される可能性があるため後追い確認が必要。
  - 本発表は AWS Region 一覧ではなく「Amazon Quick agentic capabilities がサポートされている全リージョン」で利用可、という条件付きの GA。利用可否は Region table 側に依存する。

- **関連リソース**
  - 公式ドキュメント: https://docs.aws.amazon.com/quick/latest/userguide/smart-approvals.html
  - Amazon Quick 製品ページ: https://aws.amazon.com/quick/
  - AWS Region table: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/

## 出典

- 原文: https://aws.amazon.com/about-aws/whats-new/2026/10/quick-smart-approvals-agentic-actions/
- 関連: https://docs.aws.amazon.com/quick/latest/userguide/smart-approvals.html
- 関連: https://aws.amazon.com/quick/

## レビュー (claude-code, 2026-10-29T21:16:00.000Z)

### 事実関係

- 一次情報 (AWS What's New ページ、2026-10-28 付) と要約・詳細の対応は妥当。発表日・既定 ON・classifier という呼称・CloudTrail 記録 (アクションレビューと設定変更の両方) ・リージョン条件 (「agentic capabilities がサポートされている全リージョン」) はすべて原文の記述と一致する。
- 「ask (毎回確認)」の設定にだけ smart approvals が介入する、既存ポリシーが優先される、deny は deny のまま、新たな権限付与は行わない、各自動承認はそのアクション 1 件にのみ有効、レビュー失敗・タイムアウト時はユーザーへフォールバック、という挙動の 6 点も原文と一致している。
- ただし本 review は同一セッション (claude-code) が research と review を兼ねているため、ADR-0001 が推奨するクロスエージェント運用の盲点補正は得られていない。レポート本文の `## 詳細` 冒頭でもその旨は言明されていないが、frontmatter の `agent` / `reviewedBy` が同一であることから読み手は判別できる。

### 抜け

- 「高インパクトとしてユーザーに回る 5 類型」は原文の列挙そのまま (external 送信・権限変更・削除・支払い・ユーザーが要求した範囲を超えるアクション) であり、追加の脱落はない。
- ユーザー側で `scheduled runs` の chat options からオフにできる、という運用面の記述は本文に取り込まれており、cron / schedule 運用への影響にも触れられている。
- 一方で「Amazon Quick agentic capabilities がサポートされているリージョン」の具体リストや、classifier の精度・レイテンシ・ユーザーに回す閾値の仕組みは原文に無く、本レポートもその旨を明記して追補が必要と注記しており妥当。価格面 (追加課金の有無) については原文に記述がなく本文も触れていないが、GA 発表全般の読者が気にする点なので、将来 docs ページから確認する TODO として `## 詳細` に 1 行足しても良かった。

### 憶測 / 主観の混入

- 「コンプライアンス要件で "すべてのアクションに人間承認" を厳格に求める環境では、管理者側で明示的にオフにする運用変更が必要になる」は、原文の既定 ON + custom permissions での制御可能という事実から導ける範囲の運用示唆であり、過剰な憶測ではない。許容範囲。
- そのほか評価的な表現 (「〜が望ましい」等) は見当たらない。全体として事実中心に収まっている。

### 出典の妥当性

- 一次情報 (AWS What's New 原文) を筆頭に、公式ユーザーガイド (`docs.aws.amazon.com/quick/.../smart-approvals.html`) ・製品ページ・Region table と、原文がリンクしている 3 本の二次 (公式二次) をすべて拾っており、二次情報だけで断定している記述はない。
- 公式ユーザーガイドの URL は原文に記載されたパス表記そのままで、GA 時点でページが未公開だった場合でも遷移先の正しい当て先として残しておく価値がある。review 時点で 404 かどうかの実アクセス検証は本セッションでは行っていないため、長期運用で lint する場合は link-check が別途必要。
