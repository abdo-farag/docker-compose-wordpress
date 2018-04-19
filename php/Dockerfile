FROM php:7.0-fpm

WORKDIR /var/www/html
RUN apt-get update \
 && apt-get install -y --no-install-recommends sendmail \
 && rm -rf /var/lib/apt/lists/* \
 && echo "sendmail_path=sendmail -t -i" >> /usr/local/etc/php/conf.d/sendmail.ini \

RUN rm -Rf /usr/local/bin/docker-php-entrypoint
ADD docker-php-entrypoint /usr/local/bin/docker-php-entrypoint

RUN docker-php-ext-install pdo pdo_mysql mysqli
