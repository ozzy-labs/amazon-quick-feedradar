---
id: 20260521_amazon-quick-amazon-aurora-mysql-8-4-is-now-generally-available_v1
itemIds:
  - amazon-aurora-mysql-8-4-is-now-generally-10599b4a
agent: claude-code
templateId: default
createdAt: 2026-05-24T15:47:01.000Z
updatedAt: null
reviewedAt: 2026-05-24T15:47:55.000Z
reviewedBy: claude-code
---

# Amazon Aurora MySQL 8.4 is now generally available

## 要約

Amazon Aurora MySQL-Compatible Edition が community MySQL の LTS メジャーバージョンである **MySQL 8.4** に対応し、Aurora MySQL が利用可能な全 AWS リージョンで GA となった。community MySQL 8.4.7 互換で、Aurora のバージョン番号を community MySQL のバージョンに揃える **aligned version numbering** を導入。新規クラスタのセキュリティ既定値も強化され、TLS 1.2/1.3 のみの TLS 強制、`caching_sha2_password` 認証、カスタマイズ可能なパスワードポリシーが入る。対象は Aurora MySQL を使う全ユーザーで、メジャーバージョンアップグレードに該当するため運用者の計画的対応が必要。

## 詳細

### 何が新しい / 変わった

- **MySQL 8.4 (LTS) 対応** — Aurora MySQL が community MySQL 8.4.7 互換で 8.4 をサポート。community MySQL の Long Term Support メジャーバージョンに追随する位置づけ。
- **Aligned version numbering** — Aurora で動かすバージョン番号が、互換となる community MySQL のバージョン番号と一致するようになった。あわせて Aurora が裏側のパッチ適用を肩代わりし、日常運用を簡素化する。
- **バージョン追随ポリシーの明示** — Aurora MySQL は今後、community MySQL の LTS メジャーリリースに対し 12 か月以内にメジャーバージョンを、各 community マイナーに対し 3 か月以内にマイナーバージョンを、各メジャーに対し 12 か月以内に Aurora LTS マイナーを提供することを目標とする。
- **セキュリティ既定値の強化（新規クラスタ）**:
  - TLS をデフォルトで強制し、サポートは **TLS 1.2 / 1.3 のみ**。
  - 新規アカウントは **`caching_sha2_password`** 認証プラグインを使用。
  - パスワード検証ポリシーを **DB クラスタパラメータグループ**で customizable に。
- **自動アップグレード precheck** — クラスタがオフラインになる前に互換性問題を検出する automated upgrade prechecks を提供し、アップグレード前に確認できる。

### 既存ワークフローへの影響

- これは **メジャーバージョンアップグレード**に該当するため、オプトインだが計画的な対応が必要。アップグレード手段は **Amazon RDS Blue/Green Deployments**、in-place upgrade、スナップショットからのリストアの 3 通り。
- 外部 MySQL ソースからの移行は **AWS Database Migration Service (DMS)** または **Percona XtraBackup** が利用可能。
- セキュリティ既定値の変更は **新規クラスタ**が対象。TLS 強制や `caching_sha2_password` への変更は、旧来の平文接続や `mysql_native_password` 前提のクライアント／アプリに影響しうるため、接続設定・ドライバ・認証方式の事前確認が必要。
- 提供範囲は **Aurora MySQL が利用可能な全 AWS リージョン**で、特定リージョン限定ではない。

### 補足

- 本 item は workspace の検出キーワード "Aurora MySQL 8.4"（routine の research 経路検証用の一時キーワード）でヒットしたもので、Amazon Quick 製品そのものの発表ではなく Amazon Aurora (RDS) の発表である点に留意。
- 詳細は原文がリンクする launch announcement blog / Aurora User Guide を参照（下記出典）。

## 出典

- 原文: https://aws.amazon.com/about-aws/whats-new/2026/05/amazon-aurora-mysql/8-4/
- 関連: https://aws.amazon.com/blogs/database/amazon-aurora-mysql-8-4-is-now-generally-available/ （Aurora MySQL 8.4 launch announcement blog）
- 関連: https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Updates.MajorVersionUpgrade.html （major version upgrade の手順）
- 関連: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/blue-green-deployments.html （Amazon RDS Blue/Green Deployments）
- 関連: https://aws.amazon.com/blogs/database/knowing-when-new-open-source-database-engine-versions-release-on-amazon-aurora-and-amazon-rds/ （Aurora / RDS open source release calendar）

## レビュー (claude-code, 2026-05-24T15:47:55.000Z)

> 注: 本 routine は single-session pipeline のため research と review が同一 agent (claude-code) で実行されている。クロスエージェントレビューの盲点補正効果は得られていない点に留意 (ADR-0020 D2/D5)。

### 事実関係

- 一次情報（原文 What's New ページ）を `WebFetch` で再取得し本文と突合。中核事実はすべて一致: community MySQL **8.4.7** 互換、aligned version numbering、TLS デフォルト強制（**1.2 / 1.3 のみ**）、新規アカウントの **`caching_sha2_password`**、DB クラスタパラメータグループによるパスワードポリシー customization、automated upgrade prechecks、「Aurora MySQL が利用可能な全リージョン」での提供。誤った日付・バージョン・機能名は検出されなかった。
- バージョン追随ポリシー（メジャー 12 か月以内 / マイナー 3 か月以内 / Aurora LTS マイナー 12 か月以内）も原文記載と一致。

### 抜け

- アップグレード経路（Blue/Green Deployments / in-place / snapshot restore）と移行手段（DMS / Percona XtraBackup）はカバー済み。破壊的変更性（新規クラスタのセキュリティ既定値変更が既存クライアント接続に与える影響）も §既存ワークフローへの影響で明示されている。
- コスト面は原文に明示がなく（Aurora の通常課金に従う）、レポートが言及していないのは妥当。

### 憶測 / 主観の混入

- 「裏側のパッチ適用を肩代わりし、日常運用を簡素化する」は原文 "Aurora also manages the underlying patch on your behalf, simplifying day-to-day operations" の忠実な言い換えで、踏み込み過ぎはない。
- §補足の「Amazon Quick ではなく Amazon Aurora の発表」「検出キーワードが検証用の一時キーワード」は workspace 文脈に基づく注記で、一次情報からは導けないが読者の誤解を防ぐ妥当な補足。事実関係の断定ではない。

### 出典の妥当性

- 一次情報（What's New）の URL を記載し、再取得で実在・内容一致を確認済み。二次情報のみでの断定はない。
- 関連 4 件（launch blog / major version upgrade guide / Blue/Green Deployments / release calendar）は本レビューでは未取得だが、いずれも原文がリンクする一次／公式 docs であり URL 形式・slug は妥当。
