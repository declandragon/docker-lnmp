FROM php:7.2-fpm

LABEL declandragon="https://github.com/declandragon"

# set Ali mirror
COPY sources.list /etc/apt/sources.list

# set timezome
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install package and PHP Core extensions
RUN apt-get update && apt-get install -y \
        libssl-dev -y \
        git \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install opcache \
    && docker-php-ext-install mysqli \
    && rm -r /var/lib/apt/lists/*

# Copy extensions had downloaded
COPY ./pkg/redis.tgz /home/redis.tgz
COPY ./pkg/swoole-4.3.0.tgz /home/swoole.tgz
COPY ./pkg/rabbitmq.tar.gz /home/rabbitmq.tar.gz
COPY ./pkg/amqp-1.9.0.tgz /home/amqp.tgz

# Install PECL extensions (Redis)
RUN pecl install /home/redis.tgz && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini
# Install PECL extensions (swoole-2.2.0)
RUN pecl install /home/swoole.tgz && echo "extension=swoole.so" > /usr/local/etc/php/conf.d/swoole.ini
# Install PECL extensions (amqp-1.9.0 rabbitmq-c-0.7.1.tar) (yiliabao)
RUN cd /home \
    && tar -zxf rabbitmq.tar.gz \
    && mv rabbitmq-* rabbitmq \
    && cd rabbitmq/ \
    && ./configure --prefix=/usr/local/rabbitmq \
    && make \
	&& make install
RUN cd /home \
    && tar -zxvf amqp.tgz \
    && mv amqp-* amqp \
    && cd amqp/ \
	&& phpize \
    && ./configure  --with-amqp --with-librabbitmq-dir=/usr/local/rabbitmq \
    && make \
	&& make install \
    && echo "extension=amqp.so" > /usr/local/etc/php/conf.d/amqp.ini

RUN rm -f /home/redis.tgz \
	rm -f /home/swoole.tgz \
	rm -f /home/amqp.tgz \
	rm -f /home/rabbitmq.tar.gz

# Install Composer   1.84
COPY ./pkg/composer.phar /usr/local/bin/composer
RUN chmod 755 /usr/local/bin/composer
RUN composer config -g repo.packagist composer https://packagist.laravel-china.org

WORKDIR /data
#WORKDIR /var/www

# Write Permission
RUN usermod -u 1000 www-data