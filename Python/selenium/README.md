# Selenium開発環境のセットアップ

このREADMEでは、Rye、Chrome、およびChromeDriverを使用してSeleniumの開発環境をセットアップする手順について説明します。この環境はDockerおよびDocker Composeを使用して構築され、異なるシステム間での一貫性を保証します。

## バッジ

使用しているパッケージのバッジを以下に追加します：

![Rye](https://img.shields.io/badge/Rye-latest-brightgreen)
![Google Chrome](https://img.shields.io/badge/Chrome-125.0.6422.78-blue)
![ChromeDriver](https://img.shields.io/badge/ChromeDriver-125.0.6422.78-blue)
![Docker](https://img.shields.io/badge/Docker-latest-blue)
![Selenium](https://img.shields.io/badge/Selenium-latest-green)

## 前提条件

- お使いのシステムにDockerおよびDocker Composeがインストールされていること
- Visual Studio Code (VSCode)がインストールされていること
- VSCodeのRemote - Containers拡張機能がインストールされていること

## 開発環境のセットアップ手順

1. プロジェクトディレクトリに移動します。

    ```bash
    cd your-project
    ```

2. VSCodeでプロジェクトを開きます。

    ```bash
    code .
    ```

3. VSCodeのコマンドパレットを開き（`F1`キーまたは`Ctrl+Shift+P`）、"Remote-Containers: Open Folder in Container"を選択します。

4. コンテナが起動し、必要な依存関係がインストールされるのを待ちます。

## セットアップの確認

コンテナ内で以下のコマンドを実行して、すべてが正しくセットアップされていることを確認します：

1. Ryeのインストール確認：

    ```bash
    rye --version
    ```

2. Chromeのインストール確認：

    ```bash
    google-chrome --version
    ```

3. ChromeDriverのインストール確認：

    ```bash
    chromedriver --version
    ```

すべてのコマンドが期待通りのバージョンを返す場合、環境は正しくセットアップされています。

## 結論

このセットアップにより、Rye、Chrome、およびChromeDriverを使用したSelenium開発のための一貫性のある再現可能な環境が提供されます。DockerおよびVSCodeのRemote - Containers拡張機能を使用することで、異なるマシンやプラットフォーム間で開発環境が同一であることを保証できます。