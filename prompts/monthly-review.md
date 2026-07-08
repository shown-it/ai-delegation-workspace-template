# monthly-review — 月次の運用レビュー

1ヶ月分の運用を見直し、記憶・案件・参照情報の育て方を調整する。月1回を目安に実行する。

## 手順

1. `context/INDEX.md` と `context/` 全体を読む。
2. 直近1ヶ月分の `minutes/*/README.md` を読む。
3. 以下を確認する:
   - 進行中案件のうち、状態が古いもの
   - `context/INDEX.md` に載っていない context 項目
   - 何度も出てくるが、まだ `context/reference/` に手順化されていない作業
   - `context/feedback.md` に昇格すべき繰り返しの指導
   - `_archive/` へ移す候補
4. 明確な更新だけ `context/` に反映する。
5. 判断に迷うものは、ユーザーへの確認リストとして残す。
6. 実行記録を `minutes/YYYYMMDD_月次レビュー/README.md` に残す。

## 出力に含めるもの

- 今月増えた記憶
- 更新した projects / feedback / reference
- archive 候補
- 次月に育てるとよい reference / howto
- ユーザーへの確認事項

## 制約

- 月次レビューは大掃除ではない。勝手に大幅な方針変更をしない。
- 完全削除はしない。
- privacy の詳細監査は `prompts/privacy-audit.md` に任せる。ただし明らかな Tier S を見つけたら報告する。
