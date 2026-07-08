# weekly-distill — 週次の取りこぼし蒸留

直近の作業ログから、セッション終了時に `context/` へ書き戻しきれなかった持続的な事実・決定・指導を拾う。週1回を目安に実行する。

## 手順

1. `context/INDEX.md`、`context/profile.md`、`context/feedback.md`、`context/projects/` を読む。
2. 直近7日分の `minutes/*/README.md` を読む。
3. 各 minutes について、以下だけを抽出する:
   - 今後も使う本人の好み・判断基準
   - 同じミスを防ぐための AI への指導
   - 進行中案件の状態変化
   - 環境・ツール・定型手順として再利用できる情報
4. 抽出した内容を `context/` に蒸留する:
   - 好み・判断基準 → `context/profile.md` または `context/feedback.md`
   - AI への指導 → `context/feedback.md`
   - 案件 → `context/projects/`
   - 手順・環境 → `context/reference/`
5. 新しい context 項目を作った場合は、`context/INDEX.md` に1行追加する。既存項目を更新した場合は重複行を作らない。
6. 実行記録を `minutes/YYYYMMDD_週次蒸留/README.md` に残す。

## 判断基準

- repo 構造や git 履歴から再取得できることは書き戻さない。
- 会話限りの作業メモは書き戻さない。
- 迷うものは「確認候補」として実行記録に残し、勝手に context 化しない。
- `context/` へ資料全文を貼らない。要点と適用方法だけを書く。

## 制約

- Tier S(secrets・業務機密・第三者機微情報)は context に入れない。
- 第三者については、仕事に必要な客観的事実だけにする。
- 完全削除はしない。整理が必要なら `_archive/` へ移すか、確認候補にする。
