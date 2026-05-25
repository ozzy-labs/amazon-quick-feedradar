---
id: 20260521_amazon-quick-amazon-aurora-mysql-8-4-is-now-generally-available_v1
itemIds:
  - amazon-aurora-mysql-8-4-is-now-generally-10599b4a
agent: claude-code
templateId: default
createdAt: 2026-05-25T09:51:00.000Z
updatedAt: null
reviewedAt: 2026-05-25T09:52:00.000Z
reviewedBy: claude-code
supersedes: null
---

# Amazon Aurora MySQL 8.4 is now generally available

## 要約

Amazon Aurora MySQL 互換エディションが、コミュニティ MySQL の LTS (Long Term Support) メジャーバージョンである **MySQL 8.4 を一般提供 (GA)** した。コミュニティ MySQL 8.4.7 互換で launch され、Aurora のバージョン番号を互換コミュニティ MySQL バージョンに揃える「アラインメント済みバージョン番号」を導入した。新クラスタでは TLS 強制・`caching_sha2_password` などセキュリティ既定値が強化され、アップグレード前の自動プリチェックも提供される。Aurora MySQL が利用可能な全 AWS リージョンで使え、対象は Aurora MySQL を運用する全ユーザー。破壊的変更ではなく、新規クラスタや明示的なメジャーバージョンアップグレードで適用される opt-in 型の新バージョン。

## 詳細

### 何が新しい / 変わった

- **MySQL 8.4 (LTS) 互換の GA**: Aurora MySQL 互換エディションがコミュニティ MySQL 8.4.7 互換で MySQL 8.4 をサポート。8.4 はコミュニティ MySQL の LTS メジャーバージョン。
- **アラインメント済みバージョン番号**: Aurora 上で実行するバージョン番号が、互換となるコミュニティ MySQL バージョンと一致するようになった。加えて Aurora が背後のパッチ適用を代行し、日常運用を簡素化する。
- **バージョン提供ケイデンスの目標明示**: Aurora MySQL は今後、コミュニティ MySQL の LTS リリースから 12 か月以内にメジャーバージョンを、各コミュニティ minor から 3 か月以内に minor を、各メジャーから 12 か月以内に Aurora LTS minor を提供することを目標とする。
- **新クラスタのセキュリティ既定値の強化**:
  - TLS を既定で強制し、サポートは TLS 1.2 と 1.3 のみ。
  - 新規アカウントは `caching_sha2_password` 認証プラグインを使用。
  - パスワード検証ポリシーを DB クラスタパラメータグループ経由でカスタマイズ可能。
- **自動アップグレードプリチェック**: クラスタがオフラインになる前に互換性問題を検出し、アップグレード前に確認できる。

### 既存ワークフローへの影響

- **対象ユーザー**: Aurora MySQL を運用する全ユーザー。新メジャーバージョンの追加であり、既存クラスタが自動的に 8.4 へ移行するわけではない (メジャーバージョンアップグレードは明示的な操作)。
- **アップグレード手段**: Amazon RDS Blue/Green Deployments、インプレースアップグレード、スナップショットからのリストアのいずれかで実施可能。外部 MySQL ソースからは AWS Database Migration Service (DMS) または Percona XtraBackup で移行できる。
- **セキュリティ既定値変更の留意点**: 上記のセキュリティ強化は「新クラスタ」に適用される既定値であるため、TLS 強制や `caching_sha2_password` を前提としていない既存クライアント/アプリは、8.4 の新規クラスタへ接続する際に接続設定の見直しが必要になる可能性がある。
- **位置づけ**: 破壊的変更ではなく、新バージョンとして opt-in で採用するもの。本番利用が可能 (GA)。

### 提供リージョン

- Aurora MySQL が利用可能な**全 AWS リージョン**で提供。

### 関連リソース

- Aurora / RDS オープンソースリリースカレンダー (エンジン固有のリリース目標): https://aws.amazon.com/blogs/database/knowing-when-new-open-source-database-engine-versions-release-on-amazon-aurora-and-amazon-rds/
- Aurora MySQL 8.4 launch announcement blog: https://aws.amazon.com/blogs/database/amazon-aurora-mysql-8-4-is-now-generally-available/
- Amazon RDS Blue/Green Deployments: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/blue-green-deployments.html
- メジャーバージョンアップグレード (Aurora User Guide): https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Updates.MajorVersionUpgrade.html
- 外部 MySQL からの移行: https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Migrating.ExtMySQL.S3.html
- AWS Database Migration Service: https://aws.amazon.com/dms/
- リージョンと AZ (Aurora MySQL): https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Concepts.RegionsAndAvailabilityZones.html#Aurora.Overview.Availability.MySQL
- Aurora MySQL getting started: https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.AuroraMySQL.html

## 出典

- 原文: https://aws.amazon.com/about-aws/whats-new/2026/05/amazon-aurora-mysql/8-4/
- 関連: https://aws.amazon.com/blogs/database/amazon-aurora-mysql-8-4-is-now-generally-available/

## レビュー (claude-code, 2026-05-25T09:52:00.000Z)

### 事実関係

- 本文の主要事実 (コミュニティ MySQL 8.4.7 互換、アラインメント済みバージョン番号、バージョン提供ケイデンスの 12/3/12 か月目標、新クラスタの TLS 1.2/1.3 強制・`caching_sha2_password`・パスワード検証ポリシーのパラメータグループ化、自動アップグレードプリチェック、Blue/Green・インプレース・スナップショット復元・DMS・Percona XtraBackup の移行手段、全 Aurora MySQL リージョン提供) は、いずれも検出アイテムの summary 本文と一致しており、誤った日付・バージョン・機能名は見当たらない。公開日 2026-05-21 も item と整合。
- ただし本レポートは **検出 feed の summary を一次データとして作成しており、原文ページ・launch blog を独立に WebFetch して再突合してはいない** (本実行はネットワークがソースのホスト許可リストに限定されるため)。数値・機能名の二次確認が未実施である点は運用判断の前に留意されたい。

### 抜け

- 価格・課金に関する記述がないが、これは原文 summary に料金情報の記載がないためであり、レポート側の漏れではない。Aurora MySQL 8.4 自体は新バージョン追加であり料金体系の変更を伴わない旨を一文添えるとより親切。
- 既存クラスタへの影響範囲 (どのバージョンから 8.4 へ直接アップグレード可能か等の経路条件) は summary に詳細がなく、本文も深追いしていない。これは情報源側の制約による。

### 憶測 / 主観の混入

- 「セキュリティ既定値変更の留意点」の **「既存クライアント/アプリは接続設定の見直しが必要になる可能性がある」** は、原文が「新クラスタの既定値」と述べている事実からの妥当な運用上の推論だが、原文に明示された記述ではない。「可能性がある」と適切にヘッジされており事実誤認ではないものの、解釈ベースの補足である点は明示しておく。
- それ以外の要約・詳細は事実ベースで、不要な断定・主観の混入は見られない。

### 出典の妥当性

- 一次情報 (AWS What's New 原文) と関連 launch blog が `## 出典` に記載されており妥当。関連リソースの各 URL は summary 内の埋め込みリンク由来であり、二次情報のみでの断定はない。
