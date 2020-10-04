# -----------------------------------------------------
# PHP Dependencies
FROM my/composer as vendor
COPY ./src/ /app/
RUN composer install \
    --ignore-platform-reqs \
    --no-interaction \
    --no-plugins \
    --no-scripts \
    --prefer-dist

# -----------------------------------------------------
# Application
FROM php:7.3.22-fpm

ARG USER="www-data"
ARG UID="1000"
ARG GROUP="www-data"
ARG GID="1000"

# timezone (Asia/Tokyo)
ENV TZ JST-9
ENV TERM xterm

# tools
RUN apt-get update -y \
    && apt-get install -y vim less libicu-dev libzip-dev libpq-dev \
    && apt-get clean

# php options
RUN docker-php-ext-install mysqli pdo_mysql mbstring zip intl

# php.ini
COPY ./docker/php/php.ini /usr/local/etc/php/php.ini

# application directory
ARG APP_DIR="/var/www/www.example.com"
RUN mkdir -p $APP_DIR
WORKDIR $APP_DIR

# user setting
RUN usermod -u $UID $USER && groupmod -g $GID $GROUP
RUN chown -R $UID:$GID $APP_DIR

# copy codes.
COPY --chown=${USER}:${USER} ./src ./
COPY --chown=${USER}:${USER} --from=vendor /app/vendor/ ./vendor/

USER $USER
