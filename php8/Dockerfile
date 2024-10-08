FROM php:8.1-fpm

# Install package
RUN apt-get update
RUN apt-get install vim git zip unzip libpng-dev libzip-dev librabbitmq-dev libicu-dev cron -y

RUN docker-php-ext-install pdo_mysql zip bcmath gd

# Imap
RUN apt-get install libkrb5-dev libc-client-dev -y
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN docker-php-ext-install imap

# Intl
RUN apt-get install zlib1g-dev libicu-dev -y
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl

# gnupg
RUN apt-get install -y gnupg2 gnupg gnupg1 libgpgme11-dev
RUN pecl install gnupg
RUN docker-php-ext-enable gnupg

# Excel
RUN apt-get install zlib1g-dev libpng-dev libxml2-dev -y
RUN docker-php-ext-install zip
RUN docker-php-ext-install gd
RUN docker-php-ext-install xml

# Timezone
RUN echo "date.timezone = Asia/Ho_Chi_Minh" >> /usr/local/etc/php/php.ini
RUN echo "upload_max_filesize = 1024M" >> /usr/local/etc/php/php.ini
RUN echo "post_max_size = 1024M" >> /usr/local/etc/php/php.ini
RUN echo "error_log = /var/log/php/php-fpm.log" >> /usr/local/etc/php/php.ini
RUN echo "log_errors = On" >> /usr/local/etc/php/php.ini
RUN echo "log_level = alert" >> /usr/local/etc/php/php.ini
RUN echo "output_buffering = 4096" >> /usr/local/etc/php/php.ini
RUN echo "memory_limit = 4096M" >> /usr/local/etc/php/php.ini

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Permission
RUN chmod -R 777 /var/www/

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE "9000"
