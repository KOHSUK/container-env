# Container Environment

このリポジトリは、開発環境をすぐに立ち上げることができる dev container 環境を提供します。外部のリポジトリをルートフォルダにクローンすることで、簡単に開発を開始することができます。

## 特徴

- **ホワイトリスト形式の.gitignore**: 外部リポジトリを安全にクローンできる
- **Git Worktree 対応**: 複数のブランチでの作業が容易
- **統合開発環境**: Node.js、PostgreSQL、pgAdmin がセットアップ済み
- **Claude Code 対応**: Claude Code がプリインストール
- **Docker-in-Docker**: コンテナ内で Docker コマンドが使用可能

## クイックスタート

### 1. このリポジトリをクローン

```bash
git clone <このリポジトリのURL>
cd container-env
```

### 2. dev container を起動

```bash
devcontainer up --workspace-folder .
```

### 3. 外部リポジトリをクローン

コンテナ内で、開発したいリポジトリをルートディレクトリにクローンします：

```bash
git clone <外部リポジトリのURL>
cd <リポジトリ名>
```

## 開発環境の構成

### 含まれるサービス

- **Node.js 22**: JavaScript/TypeScript 開発環境
- **PostgreSQL**: データベースサーバー
- **pgAdmin**: PostgreSQL 管理ツール（http://localhost:8080）
- **Docker-in-Docker**: コンテナ内での Docker 操作
- **GitHub CLI**: GitHub との連携ツール
- **Claude Code**: AI 開発アシスタント

### デフォルト設定

#### PostgreSQL

- **ホスト**: `db`
- **ポート**: `5432`
- **ユーザー名**: `postgres`
- **パスワード**: `postgres`
- **データベース**: `postgres`

#### pgAdmin

- **URL**: http://localhost:8080
- **メールアドレス**: `admin@example.com`
- **パスワード**: `admin`

## 使用方法

### 基本的な開発フロー

1. このリポジトリをクローンし、dev container で開く
2. 開発したいプロジェクトをルートディレクトリにクローン
3. プロジェクトディレクトリに移動して開発開始
4. 必要に応じてデータベースを使用

### Git Worktree の活用

この環境は Git Worktree での運用も可能です：

```bash
# メインブランチで作業
git clone <リポジトリURL> project-main

# 新機能ブランチ用のworktreeを作成
git worktree add ../project-feature feature-branch

# 両方のディレクトリで同時に作業可能
```

## ディレクトリ構造例

```
container-env/
├── .devcontainer/          # Dev Container設定
├── .gitignore              # ホワイトリスト形式
├── README.md               # このファイル
├── project-main/           # 外部リポジトリ（例）
├── project-feature/        # Worktreeブランチ（例）
└── another-project/        # 別の外部リポジトリ（例）
```

## 注意事項

- 外部リポジトリは`.gitignore`のホワイトリストに追加されないため、誤ってコミットされることはありません
- 各プロジェクトは独立した Git リポジトリとして管理されます

## カスタマイズ

### 環境変数

`.env`ファイルを作成して、pgAdmin の設定をカスタマイズできます：

```env
PGADMIN_DEFAULT_EMAIL=your-email@example.com
PGADMIN_DEFAULT_PASSWORD=your-password
```

### Docker サービス

必要に応じて`.devcontainer/compose.yml`を編集して、追加のサービスを含めることができます。

## トラブルシューティング

### コンテナが起動しない場合

```bash
# コンテナを再構築
docker-compose down
docker-compose up --build
```

### PostgreSQL に接続できない場合

- サービス名`db`を使用してください（`localhost`ではありません）
- デフォルトの認証情報が正しいことを確認してください

## 貢献

この dev container 環境への改善提案やバグ報告は、Issue またはプルリクエストでお知らせください。
