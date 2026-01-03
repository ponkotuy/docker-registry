# Docker Registry

Docker Composeで動作するプライベートDocker Registryです。

## セットアップ

### 1. 環境変数の設定

```bash
cp .env.init .env
# .env を編集して REGISTRY_HTTP_SECRET を設定
```

### 2. 認証設定（オプション）

```bash
# htpasswdファイルを作成
htpasswd -Bc auth/htpasswd <username>
```

## 起動方法

### Docker Compose（手動）

```bash
docker compose up -d
```

### systemd（自動起動）

```bash
# シンボリックリンクを作成
sudo ln -s $(pwd)/docker-registry.service /etc/systemd/system/

# systemdをリロード
sudo systemctl daemon-reload

# 自動起動を有効化
sudo systemctl enable docker-registry

# サービスを開始
sudo systemctl start docker-registry
```

## systemd操作

```bash
# 状態確認
sudo systemctl status docker-registry

# 停止
sudo systemctl stop docker-registry

# 再起動（コンテナ再作成）
sudo systemctl reload docker-registry

# ログ確認
journalctl -u docker-registry
```

## ディレクトリ移動時

このディレクトリを移動した場合は、以下のコマンドを実行してください：

```bash
sudo systemctl daemon-reload
```

シンボリックリンクが正しいパスを指している限り、自動的に新しい場所で動作します。
