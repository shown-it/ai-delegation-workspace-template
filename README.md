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

### 1. 新しい repo を作る

おすすめは GitHub のテンプレート機能です。

1. この repo の GitHub ページで **Use this template** を押す。
2. **Create a new repository** を選ぶ。
3. repo 名を決める。例: `my-ai-workspace`
4. まず **Private** で作る。個人情報や未公開の判断を扱うためです。
5. 作成した repo を clone する。

ローカルで複製して始める場合は、テンプレート側の git 履歴を外してから、自分の repo として初期化します。

```bash
git clone https://github.com/shown-it/ai-delegation-workspace-template.git my-ai-workspace
cd my-ai-workspace
rm -rf .git
git init -b main
git add README.md AGENTS.md CLAUDE.md .gitignore .github context prompts minutes generated examples
git commit -m "Initial AI delegation workspace"
```

GitHub に空 repo を作ったら、remote を追加して push します。

```bash
git remote add origin https://github.com/<YOUR_ACCOUNT>/<YOUR_REPO>.git
git push -u origin main
```

### 2. 自分用に初期化する

1. AI にこの repo を開いて何か頼む。
   - `context/profile.md` が未初期化、または `minutes/` がまだ空なら、`AGENTS.md` の Bootstrap 手順で初回インタビューが始まる。
   - 初回インタビューから `context/profile.md` を作る。
   - `AGENTS.md` の `<USER_NAME>`、`<REPO_NAME>`、`<REMOTE_URL>`、`<PRIMARY_LANGUAGE>` も自分用に置き換える。
2. 最初の仕事・生活領域を `context/projects/` または `context/reference/` に1件だけ作る。
3. 1週間ほど手動で使い、`context/feedback.md` が育つか確認する。
4. 問題なければ `.github/workflows/scheduled-jobs.yml` を自分の環境に合わせて有効化する。

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

## 初回の動き

通常は、最初に AI が `AGENTS.md` を読んだ時点で Bootstrap が発火します。手動で明示したい場合だけ、次のように頼んでください。

```text
prompts/init-profile.md を読み、AGENTS.md と context/profile.md を初期化してください。
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
