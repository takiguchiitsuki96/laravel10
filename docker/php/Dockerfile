FROM php:8.2.3-apache
# php.iniをコピー
COPY ./php.ini /usr/local/etc/php/
# composer インストール (マルチステージビルド)
COPY --from=composer:2.5.4 /usr/bin/composer /usr/bin/composer
# コマンド実行
# apt(Advanced Package Tool) パッケージインストール
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    unzip \
    vim \
    zip \
    npm \
    && apt-get -y clean \
    # PDO driver インストール(mysql)
    && docker-php-ext-install pdo_mysql \
    # mod_rewrite 有効化
    && a2enmod rewrite \
    # DocumentRoot 変更
    && sed -i 's!/var/www/html!/var/www/root/public!g' /etc/apache2/sites-available/000-default.conf
