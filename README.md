# sgmap - AWS Security Group Mapping Tool

`sgmap`は、AWS のセキュリティグループの接続関係を可視化するための CLI ツールです。指定した VPC 内のセキュリティグループ間の接続関係を mermaid 記法のフローチャートまたは JSON 形式で出力します。

## 機能

- 指定した VPC 内のすべてのセキュリティグループの接続関係を分析
- 特定のセキュリティグループのみを分析するオプション
- mermaid 記法のフローチャートまたは JSON 形式での出力
- セキュリティグループ間の接続プロトコルとポート情報の表示

## インストール

### pip を使用したインストール

```bash
pip install sgmap
```

### ソースからのインストール

```bash
git clone https://github.com/youyo/sgmap.git
cd sgmap
pip install -e .
```

## 使用方法

### 基本的な使用方法

```bash
# VPC内のすべてのセキュリティグループを分析し、mermaid記法で出力
sgmap --vpc-id vpc-12345678

# 特定のセキュリティグループのみを分析
sgmap --vpc-id vpc-12345678 --security-group-id sg-87654321

# JSON形式で出力
sgmap --vpc-id vpc-12345678 --json
```

### オプション

- `--vpc-id`, `-v` (必須): 分析対象の VPC ID
- `--security-group-id`, `-s` (オプション): 特定のセキュリティグループ ID を指定して分析
- `--json`, `-j` (フラグ): JSON 形式で出力（デフォルトは mermaid 記法）

## 出力例

### mermaid 記法の出力例

```mermaid
flowchart LR
    SG_sg_12345["Web Server\n(sg-12345)"]
    SG_sg_67890["Database\n(sg-67890)"]
    SG_sg_12345 -->|tcp/80| SG_sg_67890
```

### JSON 形式の出力例

```json
{
  "sg-12345": {
    "name": "Web Server",
    "inbound": [],
    "outbound": [
      {
        "id": "sg-67890",
        "name": "Database",
        "protocol": "tcp",
        "from_port": 80,
        "to_port": 80
      }
    ]
  },
  "sg-67890": {
    "name": "Database",
    "inbound": [
      {
        "id": "sg-12345",
        "name": "Web Server",
        "protocol": "tcp",
        "from_port": 80,
        "to_port": 80
      }
    ],
    "outbound": []
  }
}
```

## 必要条件

- Python 3.6 以上
- boto3
- click
- AWS 認証情報（環境変数、~/.aws/credentials など）

## 開発者向け情報

### 開発環境のセットアップ

```bash
git clone https://github.com/youyo/sgmap.git
cd sgmap
pip install -e ".[dev]"
```

### リリース方法

このプロジェクトは GitHub Actions を使用して PyPI にパッケージを公開しています。以下の手順でリリースを行います：

1. バージョンタグを作成します（例：`v0.1.0`）

   ```bash
   git tag -a v0.1.0 -m "Release version 0.1.0"
   git push origin v0.1.0
   ```

   **注意**: タグの形式は必ず `v` で始まり、その後に `X.Y.Z` 形式のバージョン番号が続く形式（例：`v0.1.0`、`v1.2.3`）にしてください。この形式に従わないタグはリリースプロセスで問題が発生する可能性があります。

2. GitHub Actions が自動的にパッケージをビルドし、PyPI に公開します。

### ローカルでのビルド

```bash
pip install -r requirements-dev.txt
python -m build
```

## ライセンス

MIT

## 作者

youyo
