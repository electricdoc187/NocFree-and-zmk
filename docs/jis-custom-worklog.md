# 2026-08-23 JISカスタムファームウェアの作業状況

対象ブランチ: `jis-custom`

## 現在の状態

- NocFree & のJIS配列向けキーマップを作成した。
- 左右の基本入力を実機で確認済み。
- 入力遅延、取りこぼし、意図しないリピートは確認されていない。
- 左側はFn + Escの短押しで再起動、1.5秒以上の長押しでブートローダーへ移行する。
- 右側はFn + Deleteの短押しで再起動、長押しでブートローダーへ移行する。
- Fn + F1/F2には、ディスプレイの明るさを下げる／上げる操作を割り当てた。
- Keymap Editor向けのレイアウト定義を追加した。
- `.dts`、`.dtsi`、`.keymap`の1行の長さ上限は180文字に設定した。

## 関連する主なファイル

- `config/nocfree_and.keymap`: 実際のキー割り当て
- `config/nocfree_and.json`: Keymap Editor用の表示レイアウト
- `tests/test_board_definition.py`: キー設定・復旧機能の検査
- `tests/test_repository_hygiene.py`: 書式などの検査

## 次の作業

- `jis-studio`ブランチで、ZMK Studio対応を試験する。
- 通常利用中の`jis-custom`には、Studio検証が完了するまで変更を加えない。
