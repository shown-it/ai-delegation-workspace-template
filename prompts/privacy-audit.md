# privacy-audit — 月次の Tier S 混入チェック

AGENTS.md の Data Boundary が守られているかを機械的に確認する。月1回を目安に実行する。

## 手順

1. 機械的スキャン: repo 全体(.git 除く)に対して以下のパターンを grep する。
   - APIキー/トークン形状: `sk-` `ghp_` `xoxb-` `AKIA` `-----BEGIN` `password` `secret` など
   - 個人情報形状: メールアドレスの大量列挙、電話番号、住所らしき文字列
2. 目視レビュー: 直近1ヶ月に追加・変更されたファイル(`git log --since` で抽出)を対象に、
   - 業務機密・顧客情報が混じっていないか
   - `context/people/` が客観的事実の範囲を超えていないか
3. 検出したものは削除せず、まずユーザーに報告する(git 履歴からの除去が必要になる場合があるため)。
4. 結果を `minutes/YYYYMMDD_privacy監査/README.md` に記録する(検出ゼロでもその旨を書く)。
