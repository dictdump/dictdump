[English](readme.md) | [日本語](readme.ja.md) | [简体中文](readme.zh-Hans.md)

# 電子辞書ファームウェア

このプロジェクトには、カシオの電子辞書「Ex-Word」シリーズのファームウェアとデータのコレクションが含まれています。 このスクリプトを使用してダンプしました: https://github.com/dictscript/dictscript

## ディレクトリ構造

-   `nor-and-nand/`: 各種モデルの辞書のNORおよびNANDファームウェアイメージを格納します。
    -   `<model>/nor/`: NORイメージを格納します。
        -   `1fxxxcleaned-true`: 抽出されたNORデータがクリーンアップされたことを示します。
        -   `trimmed-true`: ファイル末尾の空白の`FF`データが切り詰められたことを示します。
        -   `unlocked-true`: テストメニューのパスワードが解除されたことを示します。
    -   `<model>/nand/`: NANDイメージを格納します。
        -   `builded-nand-from-extracted-files`: 抽出されたファイルから構築されたNANDイメージ。
        -   `extracted-nand-files-from-device`: デバイスから抽出されたNANDファイル。
-   `nor-and-nand-extracted/`: リソース ファイルから抽出された内容を辞書の NOR と NAND に保存します。
-   `nor-and-nand-updater/`: ファームウェアアップデーターを格納します。
    -   `CY-series-dataplus5-updater/UPDADN3.BIN`: DP5シリーズ用のアップデーター。
    -   `L-series-dataplus4-updater/UPDADN2.BIN`: DP4シリーズ用のアップデーター。
-   `addons-on-dictionary/`: 追加の辞書を格納します。
-   `addons-on-dictionary-extracted/`: リソースファイルから抽出したコンテンツを追加辞書に保存します。

> **注意**: 100MBを超えるファイルは圧縮され、分割されます（*.xz.001、*.xz.002など）。元のファイルに戻すには、それらを結合して解凍してください。

## 書き込みガイド

書き込みプロセスは、辞書のエンジニアリングモード（Test Menu）で行う必要があります。

1.  **Test Menuに入る**:
    1.  辞書が**電源オフ**の状態であることを確認します。
    2.  **終了 + ページアップ + 電源キー**を約5秒間押し続け、画面が点灯して「Model」ウィンドウが表示されるまで待ちます。
    3.  キーを離し、**右キーを2回**押し、次に**入力キー**を押してメニューに入ります。

2.  **TFカードの準備**: Test Menuで対応するオプションを選択し、TFカード（2GB推奨）をフォーマットします。

3.  **ファームウェアファイルの準備**:
    -   **NORファームウェア**: `nor-and-nand/<model>/nor/`ディレクトリから適切なNORイメージを選択します。`unlocked-true`バージョンの使用を推奨します。ファイル名を変更し（例：`CY123OSB.BIN`）、TFカードのルートディレクトリにコピーします。
    -   **NANDファームウェア**（オプション）: `nand_build.py`でビルドするか、`nor-and-nand/<model>/nand/`からNANDイメージ（例：`CY123D0B.bin`）を選択し、TFカードのルートディレクトリにコピーします。
    -   **アップデータプログラム**: 辞書のモデルに応じて、`nor-and-nand-updater/`ディレクトリから`UPDADN2.BIN`または`UPDADN3.BIN`を選択し、TFカードのルートディレクトリにコピーします（`UPDADN2.BIN`はLYで始まるファイル名のシリーズのファームウェアアップデータ、`UPDADN3.BIN`はCYで始まるファイル名の新しいモデル用のファームウェアアップデータです）。

4.  **書き込み開始**:
    -   上記のファイルを含むTFカードを辞書に挿入します。
    -   Test Menuで`OS UPDATE`または対応するオプションを選択して、書き込みプロセスを開始します。

> **注意**: 書き込みにはリスクが伴います。必ずデータをバックアップしてください。