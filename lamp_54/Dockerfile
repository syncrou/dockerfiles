FROM php:5.4-apache

MAINTAINER Tobias Bähr "tobias.baehr@reinblau.de"

RUN a2enmod rewrite vhost_alias

# install the PHP extensions we need
RUN apt-get update && apt-get install -y libmcrypt-dev libpng12-dev libjpeg-dev libpq-dev imagemagick libxml2-dev libfreetype6-dev\
	&& rm -rf /var/lib/apt/lists/* \
	&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr --with-php-config=/usr/local/bin/php-config --with-freetype-dir=/usr/ --enable-gd-native-ttf \
	&& docker-php-ext-install gd mbstring pdo pdo_mysql zip exif soap mcrypt\
	&& pecl install memcache-3.0.8 && echo "extension=memcache.so" > /usr/local/etc/php/conf.d/docker-php-ext-memcache.ini; \
	rm -rvf /usr/local/etc/php/conf.d/docker-php-ext-pdo.ini; \
	rm -rvf /usr/local/etc/php/conf.d/docker-php-ext-curl.ini; \
	rm -rf /tmp/*

COPY php.ini /usr/local/etc/php/conf.d/custom_php.ini

RUN usermod -u 1000 www-data
