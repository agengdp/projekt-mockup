FROM phpswoole/swoole:4.8.7-php8.1-alpine

# RUN apk update && apk add --no-cache supervisor autoconf

# Install postgres client
# RUN set -ex && apk --no-cache add postgresql-dev
# RUN docker-php-ext-install pdo pdo_pgsql pgsql
# RUN docker-php-ext-install pcntl

RUN mkdir /log

# COPY ./.docker/supervisor/supervisor.ini /etc/supervisor.d/supervisor.ini
# COPY ./.docker/supervisor/octane.ini /etc/supervisor.d/octane.ini
# COPY ./.docker/php.ini /usr/local/etc/php/conf.d/php.ini

COPY . /app
WORKDIR /app

RUN composer install \
  --optimize-autoloader \
  --no-interaction \
  --no-dev
RUN php artisan optimize:clear

EXPOSE 9501

# CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=80", "--workers=auto", "--task-workers=auto"]
