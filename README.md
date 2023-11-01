# sql-injection-with-waf
OWASP Juice Shop with nginx

## 起動方法
docker-compose up

## ブラウザから確認
http://localhost

## kaliリナックスに入り必要なツールをインストール
~~~
docker compose exec kali bash
~~~

### sqlmapだけをインストールする場合
~~~
apt update && apt -y install sqlmap
~~~

### 必要なツールを入れたら一旦ローカルに保存した方がよさげです。
~~~
docker ps
~~~
で、コンテナIDを調べて
~~~
docker commit {コンテナID} {自分が好きなイメージ名}
~~~

* docker composeファイルのイメージを書き換えてください