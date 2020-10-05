# CakePHP3.8
CakePHP3.8環境構築です。

## 前提条件
* macOS環境
* [docker](https://docs.docker.com/get-docker/) をインストールしていること
* [docker-compose](https://docs.docker.com/compose/install/) をインストールしていること

## システム要件
* Apache 2.4.38
* PHP 7.3.22
* mbstring PHP 拡張
* intl PHP 拡張
* simplexml PHP 拡張

## コード配置
必要となるコードをリポジトリからcloneして配置します。

```
$ mkdir -p ~/workspace/cakephp3.8 && cd ~/workspace/cakephp3.8
$ git clone https://github.com/reflet/cakephp3.8.git .
```

## CakePHP環境設定
下記コマンドにてCakePHPの設定ファイルを準備する。

```
$ cp ./src/config/.env.default ./src/config/.env
$ cp ./src/config/app.default.php ./src/config/app.php
$ sed -i '' 's/__SALT__/{長いランダムな文字列}/' ./src/config/app.php
```
※ セキュリティ用の salt は、ハッシュの生成に用いられます。  
※ この値は、ランダムで長い文字列にします。そうすることで推測がより困難になります。

## Dockerイメージ作成 & 起動する
下記コマンドにて、dockerイメージを作成して、コンテナを起動します。

```
$ docker-compose build --no-cache
$ docker-compose up -d
```

## ローカル環境の停止・起動
下記コマンドにて、dockerコンテナの停止・起動を行えます。

```
# 稼働中のコンテナを停止する
$ docker-compose stop
```

```
# 停止中のコンテナを起動する
$ docker-compose start
```

## ローカル環境の破棄
下記コマンドにてDBデータも含めて削除されます。

```
$ docker-compose down -v
```

## composer update
composer.jsonを変更したら下記コマンドを実行する。

```
$ docker-compose run --rm composer update
```

## メール送信について
mailhogを利用しており、下記URLにて送信したメールを確認できます。

```
$ open http://www.example.com:8025/
```

## IDEなどで開発する場合
下記フォルダは、パフォーマンスを向上させるため、host側のフォルダをマウントしていません。

* ./src/vendor

IDEなどで開発する際に不都合がある場合は、下記コマンドにてhost側にコピーすることもできます。

* vendorフォルダ (サーバ起動中に実行)
```
$ rm -rf ./src/vendor
$ docker cp php:/var/www/www.example.com/vendor ./src/
```

## プロジェクトを作り直す
CakePHPのプロジェクトを新規に作成り直す場合は、下記のように実行します。

```
$ rm -rf src && mkdir src
$ docker-compose -f docker-compose.init.yml build --no-cache
$ docker-compose -f docker-compose.init.yml run --rm composer create-project --prefer-dist cakephp/app:3.8.* .
Set Folder Permissions ? (Default to Y) [Y,n]? Y
```

以上
