# Matching App

このプロジェクトは、Djangoを使用したアプリケーションです。以下の手順に従って、プロジェクトをセットアップし、実行してください。

## 必要な環境

- docker-desktop

## セットアップ手順

### 1. リポジトリのクローン

リポジトリをクローンします。

```bash
git clone git@github.com:Rashinban1988/matching-app.git
cd config
```

### 2. .envファイルを作成します。

```bash
cp .env.dev .env
```

### 3. docker-desktopを起動し、docker composeを実行します。

```bash
docker compose up -d --build
```

### 4. コンテナの中に入ります。(以下の作業はコンテナの中で行います。)

```bash
docker compose exec -it django bash
```

### 5. データベースのマイグレーション

データベースをマイグレーションします。

```bash
python manage.py migrate
```

### 6. スーパーユーザーの作成

スーパーユーザーを作成します。

```bash
python manage.py createsuperuser
```

プロンプトに従って、ユーザー名、メールアドレス、パスワードを入力します。

ブラウザで以下のURLにアクセスします。

```
localhost:8000/admin/
```

作成したスーパーユーザーのユーザー名とパスワードでログインします。

## 開発中に実行させるコマンド

### 1. TailwindCSSを起動する

```bash
python manage.py tailwind start
```

- VSCode 拡張機能: Tailwind CSS IntelliSense をインストールすると、TailwindCSSのコード補完が効きます。

### 2. デバッグモードを有効にする

- .envファイルにDEBUG=trueを設定してください。
- docker-compose.yamlのcommandを以下のように変更してください。

```bash
command: sh -c "echo 'デバッグ待機中です...' && python -m debugpy --listen 0.0.0.0:${DEBUG_PORT} --wait-for-client -m manage runserver 0.0.0.0:8000 --noreload"
```

- VSCodeの拡張機能: Python Debugger をインストールしてください。
- cmd + shift + d で「Python: Remote Attach」を選択してデバッグモードを有効にします。

## 注意事項

- 本番環境での使用には、適切な設定とセキュリティ対策が必要です。

## ライセンス

このプロジェクトはMITライセンスの下で提供されています。