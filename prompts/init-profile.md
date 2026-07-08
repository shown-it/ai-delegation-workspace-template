# init-profile — 初回プロフィール作成

この workspace を使い始めるために、本人へ短いインタビューを行い、`AGENTS.md` のプレースホルダと `context/profile.md` を初期化する。

## 手順

1. `AGENTS.md` と `context/INDEX.md` を読む。
2. まだ `context/profile.md` が未初期化であることを確認する。
3. repo 名と remote URL をローカル git から推測する。取れない場合だけユーザーに聞く。
   - repo 名: `basename "$(git rev-parse --show-toplevel)"`
   - remote URL: `git remote get-url origin`
4. ユーザーへ、必要最小限の質問をまとめて聞く。質問は多くても10個前後にする。
   - 呼び方
   - repo 名(推測できた場合は確認だけ)
   - remote URL(推測できた場合は確認だけ。未設定なら未設定でよい)
   - 通常使う言語
   - 主な役割・活動
   - AIに任せたい仕事
   - AIに任せたくない仕事
   - よく扱う資料・成果物
   - 文章の好み
   - この repo に入れてよい情報 / 入れてはいけない情報
   - commit / push を自動で行ってよいか
5. 回答をもとに `AGENTS.md` のプレースホルダを置換する。
   - `<USER_NAME>` → 呼び方
   - `<REPO_NAME>` → repo 名
   - `<REMOTE_URL>` → remote URL。未設定なら `未設定` と書くか、該当行を自然な文に直す
   - `<PRIMARY_LANGUAGE>` → 通常使う言語
6. commit / push の自動実行方針を回答に合わせて `AGENTS.md` の Git 節へ反映する。
   - 包括許可あり: 作業のまとまりごとに commit / push してよい。ただし stage は対象ファイル明示、Tier S 確認は維持する
   - 包括許可なし/未確認: commit / push はユーザー確認後に行う
7. 回答をもとに `context/profile.md` を更新する。
8. `context/INDEX.md` のプロフィール行を実態に合わせる。
9. 作業記録を `minutes/YYYYMMDD_初期プロフィール作成/README.md` に残す。

## 制約

- 秘密情報や認証情報は聞かない。
- 第三者の機微情報は書かない。
- 不明な項目は空欄か「未確認」として残す。
- `AGENTS.md` の規約は、ユーザーの回答で埋める範囲だけを変更する。無関係な規約を大きく書き換えない。
