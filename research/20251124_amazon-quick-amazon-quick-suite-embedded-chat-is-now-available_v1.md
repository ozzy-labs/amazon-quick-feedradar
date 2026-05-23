---
id: 20251124_amazon-quick-amazon-quick-suite-embedded-chat-is-now-available_v1
itemIds:
  - amazon-quick-suite-embedded-chat-is-now-4da620a2
agent: claude-code
templateId: default
createdAt: 2026-05-24T00:00:00.000Z
updatedAt: null
reviewedAt: 2026-05-23T17:51:38.140Z
reviewedBy: claude-code
---

# Amazon Quick Suite Embedded Chat is now available

## 要約

AWS は 2025-11-24、**Amazon Quick Suite Embedded Chat** を一般提供 (GA) した。Quick Suite の会話型 AI（構造化データと非構造化ナレッジを 1 つの会話で横断）を、自前で会話 UI・オーケストレーション・データアクセス層を実装することなく、CRM / サポートコンソール / 分析ポータルなど任意のアプリへ埋め込めるようにする機能。1-click 埋め込みと API ベースの iframe 埋め込みの 2 方式があり、SharePoint・Web・Slack・Jira 等のコネクタ連携、ブランドに合わせたカスタマイズ、アクセス範囲のスコープ制御を提供する。**追加料金はなく**、既存の Quick Suite 料金体系のまま利用できる。

## 詳細

- **何が新しい / 変わった**
  - Quick Suite の会話型エージェントを外部アプリに直接埋め込める機能が GA。「ユーザーは別ツールではなく、作業している場所で答えを得たい」という課題に対し、KPI 参照・ファイル詳細の取得・顧客フィードバック確認・アクション実行を 1 つの連続した会話内で完結させる。
  - 埋め込み方式は 2 つ:
    - **1-click 埋め込み**: 静的な embed コードを iframe に配置。利用時に Quick Suite へのサインインが必要。
    - **API ベース iframe 埋め込み**: `GenerateEmbedUrlForRegisteredUser` / `GenerateEmbedUrlForRegisteredUserWithIdentity` API でセキュアな埋め込み URL を生成し、組織の既存エンタープライズ認証基盤（IdP）でワンス認証 → 追加ログインなしでチャット利用。
  - **コネクタ連携**: SharePoint / OneDrive のドキュメント検索、Web 検索、Slack へのメッセージ送信、Jira のタスク作成など。launch blog では MCP (Model Context Protocol) 経由のカスタム接続を含む 40+ データソースに言及。
  - **カスタマイズ**: ブランドカラー、コミュニケーションスタイル（トーン）、パーソナライズされた挨拶/ウェルカムメッセージ、エージェントのペルソナ・回答フォーマット指示など。
  - **セキュリティ / アクセス制御**: エージェントが何にアクセスできるか、どのアクションを実行できるかを利用側が明示的にスコープ設定する。データアクセスは管理者が許可した範囲に限定され、Quick Suite コンソールのセキュリティ設定でドメイン allowlist の登録が必要。

- **既存ワークフローへの影響**
  - オプトインの新機能で、破壊的変更ではない。既存 Quick Suite ユーザーは追加コストなしで段階的に導入可能。
  - 自前で会話 UI・オーケストレーション・データアクセス層を作り込んでいたチームは、その実装を Embedded Chat に置き換えられる可能性がある。
  - 利用要件（launch blog 記載）: Quick Suite 有効化済み AWS アカウント、`quicksight:GenerateEmbedUrlForRegisteredUser` 権限を持つ IAM ロール、Professional / Enterprise ライセンス層、QuickSight Embedding SDK v2.11.0 以上。

- **提供リージョン**
  - GA 時点: US East (N. Virginia)、US West (Oregon)、Asia Pacific (Sydney)、Europe (Ireland)。今後数か月で追加リージョンへ拡大予定。

- **料金**
  - Embedded Chat 自体に追加料金なし。既存の Quick Suite 料金が適用される。

## 出典

- 原文: https://aws.amazon.com/about-aws/whats-new/2025/11/amazon-quick-suite-embedded-chat
- 関連（launch blog）: https://aws.amazon.com/blogs/business-intelligence/announcing-embedded-chat-in-amazon-quick-suite/
- 関連（製品ページ）: https://aws.amazon.com/quicksuite/
- 関連（料金）: https://aws.amazon.com/quicksuite/pricing/

## レビュー (claude-code, 2026-05-23T17:51:38.140Z)

### 事実関係

- 一次情報（What's New 原文）と launch blog を `WebFetch` で再取得し主要事実を突合。**いずれも一致**: 公開日 2025-11-24、追加料金なし、埋め込み 2 方式（1-click / API ベース iframe）、提供 4 リージョン（US East N. Virginia / US West Oregon / Asia Pacific Sydney / Europe Ireland）。
- launch blog 由来の技術詳細も確認できた: API 名 `GenerateEmbedUrlForRegisteredUser` / `GenerateEmbedUrlForRegisteredUserWithIdentity`、IAM 権限 `quicksight:GenerateEmbedUrlForRegisteredUser`、Professional / Enterprise ライセンス層、QuickSight Embedding SDK v2.11.0 以上、40+ データソース + MCP 経由カスタム接続。レポートの記述は正確。
- 1 点だけ要確認: 「今後数か月で追加リージョンへ拡大予定」は今回の再取得では原文から直接確認できなかった（AWS 定型句として妥当だが、断定の根拠は弱め）。低信頼度の補足として扱うのが安全。

### 抜け

- API 名・SDK バージョン・ライセンス層・40+ データソースは **What's New 原文ではなく launch blog 由来**である点を、レポートは「（launch blog 記載）」と適切に注記済み。原文単体には API/SDK 情報がない旨を読者が誤解しないため、現状の出典分けで十分。
- 補足候補（任意）: IAM アクション名・SDK 名が `quicksight:` / "QuickSight Embedding SDK" と **旧 QuickSight 系統の名前空間**を引き継いでいる点（Quick Suite は QuickSight のリブランド系譜）。実装者が IAM ポリシー作成時に混乱しやすいため一言あると親切。

### 憶測 / 主観の混入

- 「自前で会話 UI…を置き換えられる可能性がある」は「可能性がある」と明示的にヘッジされた妥当な推論であり、事実の断定ではない。問題となる憶測は見当たらない。

### 出典の妥当性

- 一次情報（What's New）+ 公式 launch blog + 製品ページ + 料金ページを列挙しており妥当。二次情報のみでの断定はなく、技術詳細は公式 blog に裏付けがある。出典構成は適切。
