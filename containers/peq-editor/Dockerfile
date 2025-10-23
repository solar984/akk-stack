######################################################
# 8.2 Apache
######################################################

FROM php:8.2-apache

RUN apt-get update && apt-get install -y \
	libbz2-dev \
#	libc-client-dev \
	libcurl4-gnutls-dev \
	libkrb5-dev \
	libmcrypt-dev \
	libpng-dev \
	libreadline-dev \
	libssl-dev \
	libxml2-dev \
	libxslt-dev \
	git \
	libdbi-perl \
	libdbd-mysql-perl

######################################################
# Enable / Compile PHP modules
######################################################
RUN docker-php-ext-install -j$(nproc) bcmath
RUN docker-php-ext-install -j$(nproc) calendar
RUN docker-php-ext-install -j$(nproc) curl
RUN docker-php-ext-install -j$(nproc) dba
RUN docker-php-ext-install -j$(nproc) exif
RUN docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install -j$(nproc) gettext
RUN pecl install mcrypt && docker-php-ext-enable mcrypt
RUN docker-php-ext-install -j$(nproc) mysqli
RUN docker-php-ext-install -j$(nproc) opcache
RUN docker-php-ext-install -j$(nproc) pdo_mysql
RUN docker-php-ext-install -j$(nproc) soap
RUN docker-php-ext-install -j$(nproc) sockets
RUN docker-php-ext-install -j$(nproc) xsl

RUN echo "opcache.enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini && \
    echo "opcache.memory_consumption=512" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini && \
    echo "opcache.interned_strings_buffer=64" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini && \
    echo "opcache.max_accelerated_files=32531" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini && \
    echo "opcache.save_comments=1" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini && \
    echo "opcache.fast_shutdown=0" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini && \
    echo "opcache.revalidate_freq=600000" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini && \
    echo "opcache.validate_timestamps=0" >> /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini

RUN cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini && \
    sed "s/short_open_tag = Off/short_open_tag = On/" < /usr/local/etc/php/php.ini > /usr/local/etc/php/php.ini.tmp && mv /usr/local/etc/php/php.ini.tmp /usr/local/etc/php/php.ini

######################################################
# Apache modules
######################################################
RUN a2enmod deflate
RUN a2enmod expires
RUN a2enmod file_cache
RUN a2enmod headers
RUN a2enmod rewrite
