# CakePHP3.8
CakePHP3.8環境構築です。

## 前提条件
* dockerをインストールしていること
* docker-composeをインストールしていること

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
$ git clone git@github.com:reflet/cakephp3.8.git .
```

## ローカル環境を起動する

```
$ docker-compose build --no-cache
$ docker-compose up -d
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
