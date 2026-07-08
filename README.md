# AI Delegation Workspace Template

AI に単発で相談するのではなく、自分の文脈を Markdown と git に蓄積しながら、どのモデルでも同じ前提で作業できるようにするための workspace テンプレートです。

## これは何か

この repo は、以下の3層で AI との日常作業を運用します。

```text
Rules layer   AGENTS.md / CLAUDE.md     どう振る舞うか
Memory layer  context/                  蒸留済みの記憶
Log layer     minutes/ generated/       作業ログ・生成物
```

- `AGENTS.md`: エージェントの基本規約。毎セッションの開始・終了、データ境界、書き戻し方針を書く。
- `context/`: プロフィール、案件、過去の指導、参照情報など、次回以降も使う記憶を置く。
- `minutes/`: 作業ごとの記録を置く。生ログや生成物はここに残し、持続的な学びだけ `context/` に蒸留する。
- `prompts/`: 記憶整理、資料取り込み、プライバシー監査などの定型手順。

## セットアップ

1. このテンプレートから新しい repo を作る。
2. まず private repo として始める。個人情報や未公開の判断を扱うためです。
3. `AGENTS.md` の `<USER_NAME>`、`<REPO_NAME>`、`<REMOTE_URL>` などを自分用に書き換える。
4. AI に `prompts/init-profile.md` を実行してもらい、初回インタビューから `context/profile.md` を作る。
5. 最初の仕事・生活領域を `context/projects/` または `context/reference/` に1件だけ作る。
6. 1週間ほど手動で使い、`context/feedback.md` が育つか確認する。
7. 問題なければ `.github/workflows/scheduled-jobs.yml` を自分の環境に合わせて有効化する。

## 定期運用

最初は手動で構いません。運用が安定したら、次のジョブを定期実行します。

- 週次: `prompts/weekly-distill.md`
  - 直近の `minutes/` を読み、書き戻し漏れを `context/` に蒸留する。
- 週次: `prompts/consolidate.md`
  - `context/` の重複・矛盾・INDEX 漏れを整理する。
- 月次: `prompts/monthly-review.md`
  - 1ヶ月分の `minutes/` と `context/` を見て、案件の棚卸し・古い記憶の整理候補・次に育てる参照情報を出す。
- 月次: `prompts/privacy-audit.md`
  - secrets、業務機密、第三者機微情報の混入を確認する。

`weekly-distill` は「記憶を増やす」ジョブ、`consolidate` は「記憶を整える」ジョブです。

## 最初に AI へ頼むこと

```text
prompts/init-profile.md を読み、私に必要な質問をして context/profile.md を初期化してください。
```

次に、実際のタスクをこの repo 上で頼みます。いまいちな応答があったら、その場で直すだけでなく「次からどうするか」を `context/feedback.md` に書き戻してもらいます。

## データ境界

- Tier S: secrets、認証情報、業務機密、第三者の機微情報。repo に入れない。
- Tier A: 自分自身の内面、健康、生活、未公開の判断。private repo のみ可。
- Tier B: 公開前提の草稿や資料。必要に応じて置いてよい。

迷ったら入れずに、AI ではなく本人が判断してください。

## 公開する場合

このテンプレート自体は公開可能な構成にしていますが、ここから作る個人 workspace は private 前提です。公開する場合は `context/`、`minutes/`、`generated/` に個人情報や業務情報が含まれていないか必ず確認してください。

## ディレクトリ

```text
.
├── AGENTS.md
├── CLAUDE.md
├── context/
├── prompts/
├── minutes/
├── generated/
├── examples/
└── .github/workflows/
```

## 運用のコツ

- `context/INDEX.md` を唯一の入口にする。
- `context/` へ全文を貼らない。持続的に使える事実・好み・判断だけを書く。
- 作業ログは `minutes/` に残す。
- 同じ訂正を二度しないため、指摘は `context/feedback.md` に理由と適用方法まで書く。
- 週1回は `weekly-distill` で `minutes/` から記憶化漏れを拾う。
- 記憶を消すときは削除ではなく `_archive/` へ移す。
