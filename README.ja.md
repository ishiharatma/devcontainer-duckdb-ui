# devcontainer-duckdb-ui

*Read this in other languages:* [![🇯🇵 日本語](https://img.shields.io/badge/%F0%9F%87%AF%F0%9F%87%B5-日本語-white)](./README.ja.md) [![🇺🇸 English](https://img.shields.io/badge/%F0%9F%87%BA%F0%9F%87%B8-English-white)](./README.md)


HTTPS対応とJSONログ解析のサンプルを含む、DuckDB UIの開発コンテナ環境です。

![top](./images/top.jpg)

## 特徴

- 🚀 Dev Container内ですぐに使えるDuckDB UI
- 🔒 HTTPS対応（ポート8080/8443）
- 📊 サンプルJSONログファイル付属（CloudTrail、Falco）
- 🐳 Docker Composeベースのセットアップ
- 💾 永続化データボリューム

## 必要要件

- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Dev Containers拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## 使い方

1. このリポジトリをクローン：
   ```bash
   git clone https://github.com/ishiharatma/devcontainer-duckdb-ui.git
   cd devcontainer-duckdb-ui
   ```

2. VS Codeで開く：
   ```bash
   code .
   ```

3. プロンプトが表示されたら「コンテナーで再度開く」をクリック（または、F1を押して「Dev Containers: Reopen in Container」を選択）

4. コンテナのビルドと起動を待つ

5. DuckDB UIにアクセス：
   - HTTP: http://localhost:8080/
   - HTTPS: https://localhost:8443/

## サンプル使用方法

リポジトリには`logs/`ディレクトリにサンプルのJSONログファイルが含まれています。これらのファイルからテーブルを作成できます：

```sql
CREATE TABLE cloudtrail AS SELECT * FROM read_json('/workspaces/duckdb-ui/logs/cloudtrail.json');
CREATE TABLE cloudtrail_insight AS SELECT * FROM read_json('/workspaces/duckdb-ui/logs/cloudtrail_insight.json');
CREATE TABLE falco AS SELECT * FROM read_json('/workspaces/duckdb-ui/logs/falco.json');
```

データをクエリ：

```sql
SELECT * FROM cloudtrail LIMIT 10;
```

## プロジェクト構造

```
.
├── .devcontainer/
│   ├── devcontainer.json    # Dev Container設定
│   └── docker-compose.yaml  # Docker Compose設定
├── logs/                    # サンプルJSONログファイル
│   ├── cloudtrail.json
│   ├── cloudtrail_insight.json
│   └── falco.json
├── images/                  # スクリーンショット
└── README.md
```

## DuckDB UI Dockerイメージ

このプロジェクトは [kudaw/duckdb-ui](https://hub.docker.com/r/kudaw/duckdb-ui) Dockerイメージ（バージョン1.3.2）を使用しています。

## データの永続化

データベースファイルは`duckdb_data` Dockerボリュームに保存され、コンテナの再起動後も保持されます。

## コントリビューション

コントリビューションを歓迎します！お気軽にPull Requestをお送りください。

## ライセンス

このプロジェクトはオープンソースで、[MITライセンス](LICENSE)の下で利用可能です。
