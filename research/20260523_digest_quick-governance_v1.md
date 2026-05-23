---
id: 20260523_digest_quick-governance_v1
itemIds:
  - amazon-quick-now-supports-cross-account-ecb19d5b
  - amazon-quick-now-supports-multi-account-f0746e69
  - amazon-quick-now-supports-multiple-owner-4c537962
  - amazon-quick-now-supports-permission-ver-ac550e76
  - amazon-quick-now-supports-document-level-0ce185df
  - amazon-quick-now-supports-document-level-bcbd0281
  - amazon-quick-now-supports-document-level-cfa7b5f0
agent: claude-code
templateId: digest
createdAt: 2026-05-23T13:40:00.000Z
updatedAt: null
reviewedAt: 2026-05-23T13:45:00.000Z
reviewedBy: claude-code
supersedes: null
---

# Digest: Amazon Quick のアクセス制御・アイデンティティ・ガバナンス

## 共通テーマ

エンタープライズ導入の前提となる**アクセス制御・権限・マルチアカウント**の整備が、2026-04〜05 に集中して進んだ。特に **document-level ACL** をデータソース横断（S3 / Google Drive / SharePoint）で揃え、ナレッジベースの権限境界を元データに忠実に反映する方向。

## 各 item の要点

- **Cross-account access for Athena**（2026-05-08）— 別アカウントの Athena データソースに対応。
- **Multi-account sign-in（同一ブラウザ）**（2026-04-16）— 複数アカウントの同時サインイン。
- **Multiple owners for SharePoint / Google Drive KB**（2026-04）— 管理者管理 KB の複数オーナー。
- **Permission verification for ACL-enabled KB**（2026-04）— ACL 対応 KB の権限検証。
- **Document-level access controls（ACL）**: **S3**（2026-04-10）/ **Google Drive** / **SharePoint** — データソース別に文書単位のアクセス制御を順次サポート。

## 差分・対立点

- document-level ACL は S3 / Google Drive / SharePoint で**別々の announcement** として段階提供。導入時はソースごとに対応状況・前提（ACL 有効化）を個別確認する必要がある。

## 推奨アクション

- エンタープライズ展開を検討中なら、自社の主要データソース（S3/SharePoint/Google Drive）の document-level ACL 対応とマルチアカウント要件を棚卸し。

## 出典

- https://aws.amazon.com/about-aws/whats-new/2026/05/amazon-quick-athena/
- https://aws.amazon.com/about-aws/whats-new/2026/04/amazon-quick-multi-account-sign-in/
- https://aws.amazon.com/about-aws/whats-new/2026/04/amazon-quick-sharepoint/
- https://aws.amazon.com/about-aws/whats-new/2026/04/amazon-quick-acl/
- https://aws.amazon.com/about-aws/whats-new/2026/04/amazon-quick-document-level-access-controls-acl-s3/
- https://aws.amazon.com/about-aws/whats-new/2026/04/amazon-quick-document-level-access-controls-google-drive/
- https://aws.amazon.com/about-aws/whats-new/2026/04/quick-sharepoint-access-control/
