FROM php:7.3-fpm
RUN apt-get update
RUN docker-php-ext-install pdo pdo_mysql
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer
RUN apt-get update \
&& apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    zlib1g-dev \
    libpq-dev \
    libxslt-dev \
    libicu-dev \
    wget \
    vim \
    git \
    locales \
    zip \
    unzip \
    gzip \
    libzip-dev \
    libwebp-dev \
    libxpm-dev \
    libssh-dev \
    --no-install-recommends && rm -r /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-gd --with-webp-dir --with-jpeg-dir --with-png-dir --with-zlib-dir --with-xpm-dir \
    && docker-php-ext-install -j$(nproc) \
    sockets \
    bcmath \
    gd \
    iconv \
    intl \
    json \
    mysqli \
    pdo_pgsql \
    pcntl \
    soap \
    xsl \
    zip \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /tmp/ /var/tmp/ ~/.pearrc \
    ;

RUN yes | pecl install xdebug-2.9.2 \
    && docker-php-ext-enable xdebug

ADD ./php.ini /usr/local/etc/php/php.ini

RUN chmod 777 -R /var/www