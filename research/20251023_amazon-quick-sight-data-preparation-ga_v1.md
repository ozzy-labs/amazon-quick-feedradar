---
id: 20251023_amazon-quick-sight-data-preparation-ga_v1
itemIds:
  - amazon-quick-sight-announces-the-general-4675041c
agent: claude-code
templateId: default
createdAt: 2026-05-23T13:30:00.000Z
updatedAt: null
reviewedAt: 2026-05-23T13:35:00.000Z
reviewedBy: claude-code
supersedes: null
---

# Amazon Quick Sight announces the general availability of a new data preparation experience

## 要約

Amazon Quick Sight（Amazon Quick Suite の一機能）で、コードを書かずに高度なデータ変換を行えるビジュアルデータ準備機能が GA。多段の変換ワークフローを clicks で構築でき、データセットの再利用階層と join 容量が大幅に拡張された。

## 詳細

- **何が新しい**: clean / transform / combine を多段ワークフローで実行。テーブル追加・集計・柔軟な join など、従来はカスタムコードや SQL が必要だった操作をノーコードで提供。
- **スケール拡張**: データセットをソースとして利用できる階層が 3 → 10 に拡張。cross-source join が 1GB → 20GB（20倍）に拡大。
- **トレーサビリティ**: 変換をステップ単位で追跡・共有可能。中央のアナリストが基盤データセットを用意し、地域のビジネスユーザーが領域別の計算・ロジックを clicks で追加、といったカスケード運用が可能。
- **対象・リージョン**: Quick Sight Author / Author Pro 向け（多数リージョン＋GovCloud）。Quick Suite Enterprise サブスクライバは US East (N. Virginia), US West (Oregon), Asia Pacific (Sydney), Europe (Ireland)。

## 出典

- 原文: https://aws.amazon.com/about-aws/whats-new/2025/10/amazon-quick-sight-general-availability-data-preparation-experience
- ドキュメント: https://docs.aws.amazon.com/quicksuite/latest/userguide/data-prep-experience-new.html
