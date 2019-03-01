FROM php:5.6-cli
ADD https://github.com/phpredis/phpredis/archive/2.2.8.tar.gz /tmp/redis.tar.gz
ADD https://sourceforge.net/projects/mcrypt/files/Libmcrypt/2.5.8/libmcrypt-2.5.8.tar.gz/download /tmp/libmcrypt.tar.gz
ADD http://pecl.php.net/get/zip-1.12.5.tgz /tmp/zip.tgz
RUN mkdir -p /usr/share/man/man1 \
    && apt-get update \
    && apt-get install -y \
        vim \
        mysql-client \
        libssl-dev \
        libfreetype6-dev \
        libpng-dev \
        libjpeg-dev \
        imagemagick \
        iputils-ping \
        procps \
        libreoffice \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install ftp \
    && docker-php-ext-install gd \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install pcntl \
    && cd /tmp && tar zxvf redis.tar.gz && cd phpredis-2.2.8/ && phpize && ./configure && make && make install \
    && cd /tmp && tar zxvf libmcrypt.tar.gz && cd libmcrypt-2.5.8/ && ./configure && make && make install \
    && cd /tmp && tar zxvf zip.tgz && cd zip-1.12.5/ && phpize && ./configure && make && make install \
    && docker-php-ext-enable redis \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install zip \
    && echo "date.timezone = \"Asia/Shanghai\"">>/usr/local/etc/php/conf.d/custom_php.ini \
    && echo "error_reporting = E_ALL">>/usr/local/etc/php/conf.d/custom_php.ini \
    && rm -rf /tmp/phpredis-2.2.8 && rm -f /tmp/redis.tar.gz \
    && rm -rf /tmp/libmcrypt-2.5.8 && rm -f /tmp/libmcrypt.tar.gz \
    && rm -rf /tmp/zip-1.12.5 && rm -f /tmp/zip.tgz
CMD ["ping", "127.0.0.1"]
