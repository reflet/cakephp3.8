# cakephp3.8

## システム要件
* Apache 2.4.38
* PHP 7.3.22
* mbstring PHP 拡張
* intl PHP 拡張
* simplexml PHP 拡張

## 新規インストール
CakePHPのプロジェクトを新規に作成する場合は、下記のように実行します。

```
$ rm -rf src
$ mkdir src
$ docker-compose -f docker-compose.init.yml build --no-cache
$ docker-compose -f docker-compose.init.yml run --rm composer create-project --prefer-dist cakephp/app:3.8.* .
Set Folder Permissions ? (Default to Y) [Y,n]? Y
```

以上
