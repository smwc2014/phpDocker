FROM php:5.6-cli
ADD https://github.com/phpredis/phpredis/archive/2.2.8.tar.gz /tmp/redis.tar.gz
ADD https://sourceforge.net/projects/mcrypt/files/Libmcrypt/2.5.8/libmcrypt-2.5.8.tar.gz/download /tmp/libmcrypt.tar.gz
RUN apt-get update \
    && apt-get install -y \
        # vim \
        mysql-client \
        libssl-dev \
        libfreetype6-dev \
        libpng-dev \
        libjpeg-dev \
        imagemagick \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install ftp \
    && docker-php-ext-install gd \
    && cd /tmp && tar zxvf redis.tar.gz && cd phpredis-2.2.8/ && phpize && ./configure && make && make install \
    && cd /tmp && tar zxvf libmcrypt.tar.gz && cd libmcrypt-2.5.8/ && ./configure && make && make install \
    && docker-php-ext-enable redis \
    && docker-php-ext-install mcrypt \
    && echo "date.timezone = \"Asia/Shanghai\"">>/usr/local/etc/php/conf.d/custom_php.ini \
    && rm -rf /tmp/phpredis-2.2.8 && rm -f /tmp/redis.tar.gz \
    && rm -rf /tmp/libmcrypt-2.5.8 && rm -f /tmp/libmcrypt.tar.gz
CMD ["/bin/bash"]
