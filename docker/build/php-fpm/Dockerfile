FROM php:8.0-fpm-alpine

RUN apk add --no-cache --update git bash

RUN apk add --no-cache --update --virtual phpize_deps ${PHPIZE_DEPS}
RUN docker-php-ext-install pdo_mysql
RUN pecl install xdebug-3.0.3 && docker-php-ext-enable xdebug
RUN apk del phpize_deps

ARG UID
RUN adduser --uid ${UID} --disabled-password docker

ENV COMPOSER_HOME /composer
ADD https://getcomposer.org/composer-1.phar /usr/bin/composer
RUN chmod +rwx /usr/bin/composer \
    && composer global require hirak/prestissimo \
    && chown -R docker:docker $COMPOSER_HOME
VOLUME $COMPOSER_HOME

WORKDIR /app
