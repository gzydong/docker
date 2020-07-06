FROM php:7.2-fpm

#修改阿里云镜像
ADD sources.list /etc/apt/sources.list

# 设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y \
    libmcrypt-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    librabbitmq-dev \
    wget \
    && rm -r /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && pecl install swoole-4.5.0 \
    && docker-php-ext-enable swoole \
    && pecl install redis-5.0.0 \
    && docker-php-ext-enable redis \
    && pecl install amqp-1.9.3 \
    && docker-php-ext-enable amqp

RUN chown -R www-data: /var/www