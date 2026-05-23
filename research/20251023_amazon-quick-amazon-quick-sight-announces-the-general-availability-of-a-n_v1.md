---
id: 20251023_amazon-quick-amazon-quick-sight-announces-the-general-availability-of-a-n_v1
itemIds:
  - amazon-quick-sight-announces-the-general-4675041c
agent: claude-code
templateId: default
createdAt: 2026-05-24T00:00:00.000Z
updatedAt: null
reviewedAt: 2026-05-23T17:50:33.783Z
reviewedBy: claude-code
---

# Amazon Quick Sight announces the general availability of a new data preparation experience

## 要約

Amazon Quick Suite の一機能である Amazon Quick Sight が、複雑なコードや SQL を書かずに高度なデータ変換を行える **ビジュアルなデータ準備 (data preparation) 体験** を GA (一般提供) した。対象はビジネスユーザー — テーブルの append・集計・柔軟な join を多段ワークフローで実行でき、各変換ステップを追跡・共有できる。データセットをソースとして利用できる階層が 3→10 に、cross-source join の処理上限が 1GB→20GB (20倍) に拡張された。Quick Sight Author / Author Pro と Quick Suite Enterprise 向けに多数のリージョンで提供される。

## 詳細

### 何が新しい / 変わった

- **ノーコードのビジュアルデータ準備**: business user が SQL やカスタムプログラミングなしで、データのクリーニング・変換・結合を実行できる。従来はカスタムコードや SQL を要した append / 集計 / flexible join 等の高度な操作が GUI で可能に。
- **多段ワークフローのトレーサビリティ**: 変換をステップ単位で追跡でき、初期状態から最終出力までの変更を可視化。ワークフローの共有・再利用 (shareability) によりチーム横断での標準化・重複排除を促進。
- **データセットのソース階層拡張 (3 → 10 levels)**: データセットをソースとして連鎖利用できる階層が 3 段から 10 段に拡張。中央のデータアナリストが foundational dataset を準備し、各地域のビジネスユーザーが territory 固有の計算・ビジネスロジックをクリック操作で重ねる、といったカスケード型の再利用ロジックを構築できる。
- **cross-source join の上限が 20 倍 (1GB → 20GB)**: 異なるソース間の join で扱えるデータ量が 1GB から 20GB へ拡大。

### 既存ワークフローへの影響

- GA のため本番利用が可能。新しい体験は既存のデータ準備体験と切り替え可能 (docs に "Switching between data preparation experiences" の項あり)。
- 新体験には **SPICE 専用機能** や、**未サポート機能 (Features not supported in the new data preparation experience)**、**データ準備の制限 (limits)**、**ingestion behavior の変更** が存在するため、既存データセットを移行する前に docs の該当セクションの確認が必要。破壊的変更というより opt-in の新体験という位置づけ。
- 対象エディション: Quick Sight **Author / Author Pro** 顧客、および一部リージョンの Quick Suite **Enterprise** subscriber。

### 提供リージョン

- **Author / Author Pro**: US East (N. Virginia, Ohio), US West (Oregon), Canada (Central), South America (São Paulo), Europe (Frankfurt, Milan, Paris, Spain, Stockholm, Ireland, London, Zurich), Africa (Cape Town), Middle East (UAE), Israel (Tel Aviv), Asia Pacific (Jakarta, Mumbai, Singapore, Tokyo, Seoul, Sydney), AWS GovCloud (US-West, US-East)
- **Quick Suite Enterprise subscriber**: US East (N. Virginia), US West (Oregon), Asia Pacific (Sydney), Europe (Ireland)

### 関連リソース

- 公式ドキュメント (data preparation experience, new): https://docs.aws.amazon.com/quicksuite/latest/userguide/data-prep-experience-new.html
  - 下位トピック: Components / Data preparation steps / Advanced workflow capabilities / SPICE-only features / Switching between experiences / Unsupported features / Data preparation limits / Ingestion behavior changes / FAQ / Dataset Enrichment

## 出典

- 原文: https://aws.amazon.com/about-aws/whats-new/2025/10/amazon-quick-sight-general-availability-data-preparation-experience
- 関連: https://docs.aws.amazon.com/quicksuite/latest/userguide/data-prep-experience-new.html

## レビュー (claude-code, 2026-05-23T17:50:33.783Z)

### 事実関係

- 原文 (`whats-new` ページ) を再取得して突合。コア数値はすべて一致 — 公開日 2025-10-23、データセットソース階層 3→10、cross-source join 上限 1GB→20GB (20X)、no-code/SQL 不要での append・集計・flexible join。誤った数値・バージョン・機能名は見当たらない。
- 対象エディション (Author / Author Pro、および一部リージョンの Quick Suite Enterprise) と両エディションの提供リージョン一覧も原文と完全一致。リージョン名の取りこぼし・誤記なし。
- 「GA (一般提供)」の位置づけは原文タイトル ("announces the general availability of") と整合。

### 抜け

- 詳細の「カスケード型再利用」例で **「各地域のビジネスユーザーが territory 固有の計算」** と地域 (territory) 軸で具体化しているが、原文の表現は "cascades across **departments**" (部門横断)。意味は近いが、原文にない「地域/territory」という軸を補っている点は留意 (下記「憶測」参照)。実害は小さい。
- コスト/課金に関する記述がないが、これは原文にも料金情報の記載がないためで、レポート側の漏れではない。念のため「原文に価格情報なし」と一文添えるとより親切。

### 憶測 / 主観の混入

- 上記のとおり「territory 固有」「各地域のビジネスユーザー」は原文の "departments" を地域軸に言い換えた**解釈ベースの例示**。事実誤認ではないが一次情報の語と差異があるため、断定を避け「部門・地域などの単位で」程度に留めるのが安全。
- それ以外の本文 (要約・既存ワークフローへの影響) は事実ベースで、不要な「〜だろう」「〜が望ましい」等の主観混入は見られない。

### 出典の妥当性

- 一次情報 (AWS What's New 原文) と公式 docs の双方が `## 出典` に記載されており妥当。二次情報のみでの断定はない。
- 既存ワークフローへの影響セクションが参照する「SPICE 専用機能 / 未サポート機能 / limits / ingestion behavior 変更」は docs 側の節 (data-prep-experience-new.html) に対応しており、出典の裏付けあり。
