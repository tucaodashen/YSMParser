# YSMParser

[简体中文](README.md#zh-cn) | [English](README.md#english) | **日本語**

![ロゴ](images/brand.jpg)

**YSM モデルを復号し、編集可能な Blockbench プロジェクトへ変換するツールです。**

[オンラインデモ](https://www.ysm.rip/) · [リリース](https://github.com/OpenYSM/YSMParser/releases)

## 概要

YSMParser は Minecraft の Yes Steve Model（YSM）形式に対応し、暗号化された `.ysm` ファイルを変換します。頂点・法線・UV 情報から Blockbench の `origin`、`size`、`pivot`、`rotation`、面ごとの UV を推定して復元します。

モデル、アニメーション、コントローラー、テクスチャ、音声、言語データ、アバター設定、`ysm.json` の復元に対応します。V1、V2、および README に記載された V3 形式をサポートします。

## 使用方法

対応する OS の実行ファイルをダウンロードするか、ソースコードをビルドしてください。`.ysm` ファイルを入力フォルダーに配置して実行します。

```bash
YSMParser -i input -o output
YSMParser -i input -o output -j 4
YSMParser -i input -o output -v
```

| オプション | 説明 |
| --- | --- |
| `-i, --input` | 入力ディレクトリ（必須） |
| `-o, --output` | 出力ディレクトリ（必須） |
| `-j, --threads` | 並列スレッド数（0 は自動検出） |
| `-v, --verbose` | 詳細ログ（シングルスレッド） |
| `--version` | バージョン表示 |

## ビルド

CMake 3.12 以降と C++20 コンパイラーが必要です。

```bash
cmake --preset x64-release
cmake --build --preset x64-release
```

WASM 用には `wasm-release` または `wasm-web-release` プリセットを使用し、Emscripten の `EMSDK` 環境変数を設定してください。

## 制限事項

YSM でモデルが頂点情報に変換されると、元の寸法や回転などの編集パラメーターが失われます。YSMParser は幾何学的推定でこれらを再構成するため、元ファイルと数値が異なる場合があります。複雑な入れ子状の回転や重複頂点により、配置が崩れることもあります。問題が発生した場合は Issue に再現用ファイルを添付してください。

## 開発への参加

開発規約は [AGENTS.md](AGENTS.md) を参照してください。依存ライブラリは `external` に同梱されています。
