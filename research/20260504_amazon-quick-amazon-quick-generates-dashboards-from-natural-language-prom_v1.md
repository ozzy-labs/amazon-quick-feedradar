---
id: 20260504_amazon-quick-amazon-quick-generates-dashboards-from-natural-language-prom_v1
itemIds:
  - amazon-quick-generates-dashboards-from-n-9d59ca9f
agent: claude-code
templateId: default
createdAt: 2026-05-23T17:13:00.000Z
updatedAt: null
reviewedAt: 2026-05-23T17:43:19.000Z
reviewedBy: claude-code
---

# Amazon Quick generates dashboards from natural language prompts

## 要約

Amazon Quick に、自然言語プロンプトからダッシュボードを生成する **Generate Analysis** 機能が追加され、Amazon Quick が利用可能な全 AWS リージョンで GA となった。作りたいダッシュボードを文章で記述し、最大 3 つのデータセットを選択、生成前に編集可能なプランをレビューする、というフローで動作する。手作業で数時間かかっていたダッシュボード構築を数分に短縮するのが狙い。対象は Enterprise サブスクリプション / Author Pro ユーザーで、Author も 2026 年 12 月まで促進的に利用できる。

## 詳細

### 何が新しい / 変わった

- **Generate Analysis** — 自然言語の記述からダッシュボードを自動生成する新機能。たとえば「revenue trends, regional comparisons, month-over-month growth を含む sales performance dashboard を作って」のように目標を記述すると、refinement 用のドラフトが返ってくる。
- 生成フロー: ①作りたいダッシュボードを記述 → ②最大 3 つのデータセットを選択 → ③**編集可能なプラン (editable plan)** をレビュー → ④生成。
- 生成物には、データに合わせて選ばれた visuals、ディメンション別に探索するための filter controls、year-over-year growth / month-over-month comparison などの calculated fields を含む、整理された sheets が含まれる。
- 価値提案: 手動構成で数時間かかるダッシュボード作成を数分に短縮する。

### 既存ワークフローへの影響

- 生成物は既存の publishing workflows、embedding、CI/CD パイプライン、point-and-click 編集とそのまま連携する（既存資産を置き換えるのではなく入口を増やす位置づけ）。
- オプトイン的な追加機能であり、破壊的変更ではない。利用開始は任意のデータセットを開いて「Generate analysis」を選ぶだけ。

### 提供条件・対象

- 提供開始時点では **Enterprise subscription / Author Pro** ユーザーが対象。
- **Author** も、組織がアクセスを制限していない限り、Amazon Quick Enterprise の一部として **2026 年 12 月まで** 促進的 (promotional) に利用可能。
- Amazon Quick が利用可能な **全 AWS リージョン** で GA。

### 補足

- 原文の見出し（item title）は "generates dashboards" だが、機能名は **Generate Analysis**、公式 URL slug は `generates-analyses-from-natural-language-prompts` で「analysis / analyses」の語が併用されている。Amazon Quick における「analysis」はダッシュボード（sheets + visuals）の構成単位を指すため、実体は同一。
- 「QuickSight → Quick」のリブランド後ブランドである点に留意（本リリースは Amazon Quick 名義）。

## 出典

- 原文: https://aws.amazon.com/about-aws/whats-new/2026/05/amazon-quick-generates-analyses-from-natural-language-prompts/
- 関連: https://docs.aws.amazon.com/quick/latest/userguide/generating-an-analysis.html （Generating an analysis with natural language prompts — User Guide）
- 関連: https://docs.aws.amazon.com/quick/latest/userguide/regions.html#regions-qs （Amazon Quick 利用可能リージョン）

## レビュー (claude-code, 2026-05-23T17:43:19.000Z)

### 事実関係

- 一次情報 (原文 What's New) を `WebFetch` で再取得し突合。中核となる事実はすべて原文と一致: 機能名 "Generate Analysis"、生成フロー (describe → select up to three datasets → review an editable plan → generate)、「all AWS Regions where Amazon Quick is available」での GA、対象 (Enterprise subscription/Author Pro)、Author の促進的アクセスが 2026 年 12 月まで、生成物 (visuals / filter controls / calculated fields の YoY・MoM)、既存 workflow 連携 (publishing / embedding / CI/CD / point-and-click) — 誤った日付・バージョン・機能名は検出されなかった。
- データセット上限「最大 3 つ」は原文 "up to three datasets" と一致。リージョン記述も「特定リージョンに限定」ではなく「Amazon Quick 提供全リージョン」で正確。

### 抜け

- 重要な変更点・対象ユーザー・破壊的変更有無のカバレッジは十分。コストは原文も明示しておらず (subscription tier 単位のみ)、レポートが tier 条件を押さえている点で漏れはない。
- 強いて言えば、Author の「2026 年 12 月まで」が促進期間終了後にどの tier 扱いになるか (有償化 / 利用停止) は原文も本レポートも触れていない。原文に記載がないため抜けではないが、運用判断時の確認ポイントとして留意。

### 憶測 / 主観の混入

- §要約・§詳細の「手作業で数時間かかっていた構築を数分に短縮」という価値提案は、今回再取得した原文本文には verbatim では確認できなかった。AWS の典型的な訴求として妥当な要約だが、原文の明示的記述ではない可能性があるため、断定調はやや踏み込み気味。事実というより訴求の言い換えとして読むのが安全。
- §詳細の例示プロンプト「revenue trends, regional comparisons, month-over-month growth を含む sales performance dashboard」も原文本文では確認できず、レポート著者による説明用の例とみられる。「たとえば」と明示されており読者を誤導しないが、原文由来ではない点に留意。
- §補足の「QuickSight → Quick リブランド後ブランド」は、引用した 3 つの出典 URL では裏取りされていない外部知識。内容自体は妥当な背景補足だが、本リリースの一次情報からは導けない記述である。

### 出典の妥当性

- 一次情報 (What's New) の URL が記載され、再取得で実在・内容一致を確認済み。二次情報のみの断定はない。
- 関連 docs 2 件 (generating-an-analysis / regions) は本レビューでは未取得 (原文一次情報で中核事実が裏取りできたため)。URL 形式・slug は妥当だが、内容の最終確認は未実施である点を付記する。
