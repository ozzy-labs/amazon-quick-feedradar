---
id: 20260428_amazon-quick-start-using-amazon-quick-for-free-in-minutes-with-free-and-p_v1
itemIds:
  - start-using-amazon-quick-for-free-in-min-7db05acf
agent: claude-code
templateId: default
createdAt: 2026-05-23T17:07:21.000Z
updatedAt: null
reviewedAt: 2026-05-23T17:40:08.000Z
reviewedBy: claude-code
---

# Start using Amazon Quick for free in minutes with Free and Plus pricing plans

## 要約

- **What**: Amazon Quick に **Free / Plus** という新しい self-serve 料金プランが追加され、AWS アカウントなしで個人メール (または Google / Apple / GitHub / Amazon 認証) から数分でサインアップできるようになった (2026-04-28 発表)。
- **Who**: 営業・マーケティング・財務・オペレーションなど、これまで AWS アカウント前提で導入障壁が高かった非インフラ系の個人 / 小規模チームのビジネスユーザー。
- **Impact**: 既存の AWS アカウント経由の **Professional / Enterprise** プランに加え、low-friction な入口 (Free=$0、Plus=$20/user/月) が新設された。**オプトインの追加であり破壊的変更ではない**。製品の導入モデルが「AWS 契約者向け」から「個人がまず無料で試せる SaaS」へ広がる packaging 変更。

## 詳細

### 何が新しい / 変わった

- **Free プラン ($0/user/月)**: AWS アカウント不要でサインアップ可能。AI アシスタントとのチャット、カスタムエージェント作成、in-depth research、デスクトップアプリ、Spaces によるワーク整理、ブラウザ拡張を利用できる。サインアップは個人メール、または既存の Google / Apple / GitHub / Amazon クレデンシャルで可能。
  - 公式 pricing ページ上では **30 日トライアル中は最大 25 ユーザーまで** といった上限の記載がある (詳細な条件は一次情報で要確認)。
- **Plus プラン ($20/user/月、年契約)**: Free の全機能に加え、チーム共有 Spaces、外部ファイル/コンテンツ連携、ナレッジベース共有、Quick Flows による自動化、本番 Web アプリ、Slack / Microsoft 365 / Google / QuickBooks 等のツール統合、Microsoft 365 形式の成果物生成。インデックスストレージはユーザーあたり 50 GB (プール)。
- **ガイド付きオンボーディング**: 「5 分以内に価値を見いだせる」とうたう role-specific (sales / marketing / finance / operations 等) のワークフローが用意される。
- **Amazon Quick の位置づけ**: 質問への回答だけでなく、ミーティングのスケジューリング・メール送信・アクションアイテムのフォローアップなど、アプリ/ツール/データに接続して「行動を取る」エージェント型 AI アシスタント (個人のナレッジグラフを構築するとされる)。

### 既存ワークフローへの影響

- **既存の Professional / Enterprise ユーザーへの破壊的影響はない**。Free / Plus は新規の self-serve 入口として追加されたもの。
  - Professional: $20/user/月 (AWS アカウント経由) + $250/account/月のインフラ料金。Quick Sight シナリオ、Quick Automate (multi-step workflow)、ダッシュボード作成、BI 機能を含む。
  - Enterprise: $40/user/月 + $250/account/月。資産認証、データ主権コントロール、RBAC/SSO、集中課金、24/7 AWS サポートを含む。
- **導入経路の二系統化**: 「quick.aws.com で個人がまず無料で始める」経路と、従来の「AWS アカウント経由でガバナンス込みで導入する」経路が並立する。チーム/組織で本格利用する場合は引き続き Professional / Enterprise が必要。
- **ブランド文脈**: Amazon Quick は旧 QuickSight 系譜の Quick Suite ブランドに連なる製品であり、本件は機能追加というより **packaging / go-to-market の変更**。FeedRadar の triage でも「価格改定 / 料金体系変更」として research 対象に分類済み。

### 関連リソース

- Amazon Quick pricing plans page: https://aws.amazon.com/quick/pricing/
- Signing up at quick.aws.com (公式 docs): https://docs.aws.amazon.com/quick/latest/userguide/standalone-signup.html
- Amazon Quick 製品トップ: https://aws.com/quick

> 注: Free / Plus の上限ユーザー数、ストレージ、エージェント稼働時間などの数値は pricing ページの記載をもとにしており、トライアル条件等は更新される可能性がある。運用判断の前に一次情報での再確認を推奨する。

## 出典

- 原文: https://aws.amazon.com/about-aws/whats-new/2026/04/amazon-quick-free-plus/
- 関連:
  - https://aws.amazon.com/quick/pricing/
  - https://docs.aws.amazon.com/quick/latest/userguide/standalone-signup.html

## レビュー (claude-code, 2026-05-23T17:40:08.000Z)

### 事実関係

- 料金 4 段構成 (Free=$0 / Plus=$20/user/月・年契約 / Professional=$20/user/月+$250/account/月 / Enterprise=$40/user/月+$250/account/月) は内部矛盾なく整理されている。Plus と Professional がともに「$20/user/月」で表記衝突しうるが、本文が「Plus は AWS アカウント不要・インフラ料金なし」「Professional は AWS 経由 +$250/account」と切り分けており可読。
- 本 review では一次情報を再取得した突合は行っていない (WebFetch 未実行)。数値項目 (25 ユーザー上限・50 GB・トライアル条件・エージェント稼働時間) は本文も「要確認」と明記しており、運用判断前に pricing ページ・whats-new 原文での再確認が必須。誤った日付・機能名は本文上は検出されず。

### 抜け

- **Free プランのストレージ容量・利用上限が未記載** (Plus は 50 GB と明記)。Free の制約 (ストレージ / エージェント実行量 / 商用利用可否) は導入判断の要なので一次情報での補完が望ましい。
- 提供リージョン・対応言語、および**旧 QuickSight ユーザーの移行/課金影響**への言及がない。ブランド系譜 (Quick Suite) は触れているが、既存契約者にとっての移行パスや名称変更の運用影響が抜けている。

### 憶測 / 主観の混入

- 「破壊的変更ではない / packaging 変更」という評価は「オプトインの追加」という論拠に基づいており妥当。marketing 文言は「うたう」「とされる」で適切に距離化されており、事実ベースでない断定の混入は概ね指摘なし。

### 出典の妥当性

- 一次情報 (whats-new 原文) を明示しており出典構成は妥当。
- ただし関連リソース末尾の「Amazon Quick 製品トップ: `https://aws.com/quick`」は **canonical ドメインでない** (正規は `https://aws.amazon.com/quick`)。リンク切れ / 誤誘導の恐れがあり修正推奨。
- pricing ページ・docs URL は妥当な形式。二次情報のみでの断定は見られない。
