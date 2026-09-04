# DYStudio対応 変更点まとめ

DYStudio (ZMK Studio) に対応させるため、「dya-studio」フォルダの構成を「自分用」フォルダに反映しました。
※ 既存のキーバインド（キー配列）ファイルである `mona2.keymap` は意図的に変更せず、これまでの設定を維持しています。

## 1. ZMK設定基盤・ビルド設定の更新
* **`config/west.yml`**: ZMKのベースリポジトリを公式から `cormoran` 氏のフォーク（`main+dya`）に変更。ZMK StudioとのRPC通信やランタイムマクロ等の機能モジュールを追加しました。
* **`build.yaml`**: ZMKのバージョンアップ（Zephyr 4.1等）に伴うボード名の変更 (`xiao_ble/nrf52840/zmk`) および、USB経由のStudio通信スニペット (`studio-rpc-usb-uart`) を追加しました。また、PAW3222センサー版のビルドターゲットも追加しています。
* **`.github/workflows/build.yml`**: ビルド環境を新しいZMKバージョン向けに同期しました。

## 2. ボード・シールド定義の更新
* **`boards/shields/mona2/mona2.zmk.yml`**: `features:` 項目に `- studio` を追加し、ZMK Studio互換であることを宣言しました。
* **各種 Kconfig / devicetree (.dtsi, .overlay) / .conf ファイル**: ZMK Studioや各種センサー（トラックボール等）、マウスジェスチャーの通信に必要なフラグ設定やデバイス情報を更新・最適化しました。

## 3. 新規追加ファイル
* **`config/paw3222.conf` / `config/paw3222.overlay`**: 新しいPAW3222センサーを使用する際の設定ファイル群。
* **`docs/mouse-gesture-web-numberfield.patch`**: マウスジェスチャーに関するドキュメント・パッチ。
* **`keymap-drawer/mona2_01.svg`**: Keymap Drawerによるレイアウト可視化用の新規画像。

## 4. その他ファイル
* **`README.md`**: DYStudio用の解説やリンク等が更新されました。
* **`keymap-drawer` 設定ファイル**: 新しいレイヤー構成等に合わせた描画設定を反映しました。

## 今後の作業について
今回は既存のキーバインド（`mona2.keymap`）を維持しています。もし、DYStudio上で「OSごとの自動切り替え」などの新しい独自機能が利用できない場合は、必要に応じて `dya-studio` フォルダに同梱されている新しいキーマップ（Windows用・Mac用でレイヤーが分かれた構造）を手動でマージするか、DYStudioのUI上から再設定を行ってください。
