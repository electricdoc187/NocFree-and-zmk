# 2026-08-23 ZMK Studio対応開始

対象ブランチ: `jis-studio`

元ブランチ: `jis-custom`

## 目的

NocFree & のJISカスタムファームウェアをZMK Studioに対応させる。

## 方針

- 通常利用用の`jis-custom`は変更しない。
- ZMK Studio専用の機能は、左側（中央側）のファームウェアだけで有効にする。
- JIS配列の実際のキー位置・キーサイズをStudio用の物理レイアウトとして定義する。
- Studioを使ってキーマップを書き換える前に、ブートローダーへ入る方法を実機で確認する。
- Studio版は、通常版とは別にビルド・検証する。

## 注意点

- ZMK Studioで保存したキー設定はキーボード本体へ保存される。
- Studioで設定を保存した後は、GitHub上の`.keymap`を変更しても、その内容はすぐには反映されない。
- GitHub側の標準キーマップへ戻すには、ZMK Studioで「Restore Stock Settings」を実行する。
