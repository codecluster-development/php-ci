FROM php:7.3-stretch
MAINTAINER "Bence Gazder"
LABEL maintainer="bence.gazder@codecluster.io"

# install dependencies
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" && \
    apt update && apt install -y \
    supervisor \
    cron \
    ca-certificates \
    libfreetype6 \
    libfreetype6-dev \
    libssl1.0 \
    libpng16-16 \
    libjpeg62-turbo \
    libjpeg62-turbo-dev \
    mcrypt \
    libcurl4-openssl-dev \
    libpng-dev \
    libicu-dev \
    zip \
    libzip-dev \
    $PHPIZE_DEPS \
    sudo \
# configure extensions
    && docker-php-ext-configure intl --enable-intl \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
# install extensions
    && docker-php-ext-install \
    mbstring \
    intl \
    curl \
    json \
    pdo_mysql \
    exif \
    zip \
    gd \
    bcmath \
    opcache \
    pcntl \
    sockets \
# cleanup
    && docker-php-source delete \
    && apt purge -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libcurl4-openssl-dev \
    libpng-dev \
    libicu-dev \
    $PHPIZE_DEPS \
    && apt autoclean -y \
    && apt autoremove -y \
    && rm -rf /usr/src/ \
    && rm -rf /usr/local/lib/php/test/ \
    && rm -rf /usr/local/bin/phpdbg \
    && echo "Installed packages:" \
    && apt list --installed \
    && php -i \
    && php -v

CMD ["php", "-v"]
