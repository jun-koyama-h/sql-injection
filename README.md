# sql-injection-with-waf
OWASP Juice Shop with nginx

## 起動方法
docker compose up

起動時にkali linuxにsqlmapをインストールします。ビルド済みイメージが存在すればそれを使用します。

    image: nginx:1.25.3
    # build: nginx

image: nginx:1.25.3をコメントアウトし、build: nginxを有効にするとwaf入りのimageをビルドします。（10分ぐらいかかるので注意）

## 起動方法　その２ バックグラウンド
docker compose up -d

## 終了し削除する方法
docker compose down

## ブラウザから確認
http://localhost

