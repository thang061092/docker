FROM php:8-fpm

RUN apt-get update && \
    apt-get install -y supervisor procps && \
    mkdir -p /var/log/supervisor
# Cài đặt Redis
RUN pecl install redis && docker-php-ext-enable redis
RUN docker-php-ext-install pdo_mysql
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
