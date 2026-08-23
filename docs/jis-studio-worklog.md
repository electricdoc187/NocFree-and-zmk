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

## 動作確認結果

- ZMK Studio対応ファームウェアを、左側ユニットへインストールした。
- ZMK StudioにUSB接続し、JIS配列の物理レイアウトが正しく表示されることを確認した。
- BaseレイヤーとFnレイヤーのキー配置が読み込まれ、無変換キーのLayer-Tapおよび右側FnキーのMomentary Layerも正しく表示された。
- Fnレイヤーでは、`&trans` のキーが空白として表示されることを確認した。
- Fn+F7／F8／F9の前のトラック／再生・一時停止／次のトラックが表示・動作することを確認した。
- ZMK StudioからFn+F3へ`Ctrl + Arrow`を割り当て、保存後に実機で正常に動作することを確認した。
- Studioのロックは無効化して運用することにした。

## ファームウェア容量不足への対策

ZMK Studioを有効にした初回ビルドでは、ファームウェアがフラッシュ容量を約3 KB超過し、ビルドに失敗した。

ZMK Studio用の`studio-rpc-usb-uart`スニペットは、初期状態では多数の未使用ビヘイビアも含めるため、NocFree & の容量では収まらなかった。

そのため、`config/nocfree_and.keymap` の先頭で、すべてのビヘイビアを含める設定を無効化した。

```dts
#undef ZMK_BEHAVIORS_KEEP_ALL
#include <behaviors.dtsi>
```

これにより、キーマップから実際に参照されているビヘイビアだけを含める構成となり、ZMK Studio対応ファームウェアのビルドに成功した。

今後、新しい種類の特殊なビヘイビアをZMK Studioから使いたい場合は、ファームウェアに含める設定を追加する必要がある場合がある。

## デフォルトキーマップを変更するときの注意

ZMK Studioで保存した配列とは別に、GitHubでビルドするファームウェアの**初期キーマップ**を変更する場合は、次の2か所を同じ内容に更新する。

1. `config/nocfree_and.keymap`  
   実際にビルドされる、個人設定用のキーマップファイル。

2. `boards/nocfree/nocfree_and/nocfree_and.keymap`  
   ボード定義に含まれる標準キーマップファイル。

通常のカスタマイズやファームウェアのビルドでは、`config/nocfree_and.keymap` が優先される。  
ただし、将来の保守時に標準設定と個人設定の内容が食い違わないよう、デフォルト配列を変更した際は両方を揃えて更新する。

また、ZMK Studioで保存済みの設定がある場合、GitHub側の初期キーマップへ戻すには、ZMK Studioの「Restore Stock Settings」を実行する。

## 現在のStudio設定

`build.yaml` の左側ユニットには、以下を設定している。

```yaml
snippet: studio-rpc-usb-uart
cmake-args: -DCONFIG_ZMK_STUDIO=y -DCONFIG_ZMK_STUDIO_LOCKING=n
```

ロックを無効にしているため、ZMK Studio接続時にFn+6による解除操作は不要である。

## 注意事項

ZMK Studioで保存したキーマップ変更は、キーボード本体に保存される。  
今後GitHub上の`.keymap`ファイルを変更して再ビルドした場合、Studio側で保存済みの配列を初期状態へ戻すには、ZMK Studioの「Restore Stock Settings」を使用する。
