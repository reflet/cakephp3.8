# PHP 7.4.11環境
# https://hub.docker.com/layers/composer/library/composer/1.10.13/images/sha256-36e517b3bc9b32c1af5b1a6b66f01c8d1c4f15711a3ecb243200abb5292ce70a?context=explore
FROM composer:1.10.13

# [高速化] Composerの通信を並列化するプラグインのインストールする
# ※ https://qrunch.net/@sogaoh/entries/Z8NnZ1RQK9vbcaIo
RUN composer global require hirak/prestissimo

# [高速化] Packagistのミラーサイトを設定する
# ※ https://packagist.jp/
RUN composer global config repositories.packagist composer https://packagist.jp

# 実行環境のPHPバージョン(7.3.22)を指定する
# https://getcomposer.org/doc/06-config.md#platform
RUN composer global config platform.php 7.3.22

# [CakePHP3 システム要件] PHP拡張(mbstring, intl, sitemapxml)を追加する
# ※ https://book.cakephp.org/3.next/ja/installation.html
# ※ PHP7.4: mbstring -> libonig-dev ( https://github.com/docker-library/php/issues/880 )
# ※ simplexml (libxml-2.0 >= 2.7.6 -> libxml2-dev)
RUN apk add --update --no-cache icu-dev oniguruma-dev libxml2-dev \
    && docker-php-ext-install intl simplexml
