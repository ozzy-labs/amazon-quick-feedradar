---
id: 20260428_amazon-quick-amazon-quick-now-available-as-a-desktop-application-for-maco_v1
itemIds:
  - amazon-quick-now-available-as-a-desktop-9d957fec
agent: claude-code
templateId: default
createdAt: 2026-05-24T00:00:00.000Z
updatedAt: null
reviewedAt: 2026-05-23T17:59:48.000Z
reviewedBy: claude-code
---

# Amazon Quick now available as a desktop application for macOS and Windows (Preview)

## 要約

Amazon Quick が macOS / Windows 向けの**ネイティブデスクトップアプリ**として preview 提供を開始した（2026-04-28）。ブラウザの枠を超え、ローカルファイルへの直接アクセス・OS レベルの通知・デスクトップアプリ操作の自動化といった「PC 上の文脈」を扱えるようになる点が新しい。Web 版と memory / knowledge graph / agents を共有するため、デスクトップと Web のどちらでも同じコンテキストが引き継がれる。現状は **US East (N. Virginia) の全 Quick subscriber 向け preview** で、追加課金の有無など一般提供時の条件は未確定。

## 詳細

### 何が新しい / 変わった

- **新しい配布形態**: これまで Web ベースだった Amazon Quick が、macOS / Windows の**ネイティブデスクトップアプリ**として preview 提供開始。
- **ローカルファイルへの直接アクセス**: ファイルをアップロードせずに PC 上のファイルを読み取り・操作できる。
- **OS レベルのプロアクティブ通知**: action item / カレンダーの衝突 / 対応が必要なメッセージを検知して通知する。
- **デスクトップ / ブラウザ操作の自動化**: ブラウザベースのタスクやデスクトップアプリのネイティブ操作を自動化できる。
- **personal knowledge graph**: やり取りを重ねるごとに「人・プロジェクト・関係性」を学習し、コンテキストが時間とともに蓄積（compounding）される。
- **ビルダー向け MCP 連携**: デスクトップアプリはコーディングエージェントへの **local Model Context Protocol (MCP) 接続**をサポートする。
- **Web ⇔ デスクトップのコンテキスト共有**: memory / knowledge graph / agents が両サーフェス間で共有され、コンテキストが端末をまたいで移動する。

公式 product ページ（[aws.amazon.com/quick/desktop](https://aws.amazon.com/quick/desktop/)）によれば、対応 OS は **macOS (ARM64)** と **Windows (x64)**。Slack / Microsoft Outlook / Gmail / Microsoft Teams / Salesforce 等の CRM・スプレッドシート・データベースへ、ファイルアップロードやアプリ切り替えなしで横断接続できる点を訴求している。

### 既存ワークフローへの影響

- **オプトイン**: 既存の Web 版利用に影響する破壊的変更ではなく、デスクトップアプリは追加で download して使う形態。preview のため本番ワークフローへの全面採用は時期尚早。
- **対象は全 Quick subscriber**（US East (N. Virginia)）。利用には Quick アカウントが必要。
- **セキュリティ観点**: ローカルファイル直接アクセス・デスクトップ操作の自動化・OS 通知という強い権限を持つため、エンタープライズ導入時はデータ取り扱いポリシーの確認が必要（公式は「組織が既に信頼するエンタープライズセキュリティ標準に準拠」と説明）。
- **コスト**: product ページに free tier への言及はあるが、デスクトップアプリ固有の課金条件・一般提供（GA）時期は本リリースでは明示されていない。

### 関連リソース

- ダウンロード: <https://aws.amazon.com/quick/download/>
- product ページ: <https://aws.amazon.com/quick/desktop/>
- 公式ドキュメント: <https://docs.aws.amazon.com/quick/latest/userguide/amazon-quick-desktop.html>
- サインアップ: <https://portal.aws.amazon.com/billing/signup/service?app=AmazonQuickSuite&tier=free&funnel=boost#/validation>

## 出典

- 原文: <https://aws.amazon.com/about-aws/whats-new/2026/04/amazon-quick-macos-windows-preview/>
- 関連: <https://aws.amazon.com/quick/desktop/>
- 関連: <https://docs.aws.amazon.com/quick/latest/userguide/amazon-quick-desktop.html>
- 関連: <https://aws.amazon.com/quick/download/>

## レビュー (claude-code, 2026-05-23T17:59:48.000Z)

### 事実関係

- 一次情報（[AWS What's New](https://aws.amazon.com/about-aws/whats-new/2026/04/amazon-quick-macos-windows-preview/)）を WebFetch で再取得して突合。発表日 2026-04-28、対応 OS（macOS / Windows）、機能（ローカルファイルアクセス・OS 通知・自動化・personal knowledge graph・local MCP 接続・Web ⇔ デスクトップ共有）はいずれも原文と一致。誤った日付・機能名は見当たらない。
- 提供範囲は原文の "available in preview to all Quick subscriber on MacOS and Windows in all US East (N. Virginia)" と一致。対応アーキテクチャ（macOS ARM64 / Windows x64）も product ページの記載と一致しており正確。

### 抜け

- product ページには「meeting prep / missed follow-ups / scheduling conflicts をバックグラウンドで surface する」という記述があり、本文の「OS レベルのプロアクティブ通知」とほぼ同義だが、能動的なバックグラウンド監視という性格はもう一歩踏み込んで書けた余地がある（運用判断に影響しない軽微な抜け）。
- 「preview は単一リージョン (US East N. Virginia) 限定」という制約は本文に明記済みで、リージョン展開の今後については原文にも情報がないため抜けではない。

### 憶測 / 主観の混入

- 「preview のため本番ワークフローへの全面採用は時期尚早」「エンタープライズ導入時はデータ取り扱いポリシーの確認が必要」は事実ではなく評価・推奨。preview ステータスとローカル権限の強さから導かれる妥当な助言だが、一次情報の言明ではない点は読み手が区別できるとよい。重大な誤誘導はない。

### 出典の妥当性

- 一次情報（AWS What's New）が冒頭に明記され、product ページ・公式 docs・ダウンロード URL も補足されており出典構成は妥当。二次情報のみで断定している箇所はない。
- 公式 docs URL（`docs.aws.amazon.com/quick/.../amazon-quick-desktop.html`）とサインアップ URL は本レビューでは WebFetch 再取得していない（What's New / product ページのみ突合）。いずれも公式ドメインだが、リンク到達性は未検証である点を補足する。
