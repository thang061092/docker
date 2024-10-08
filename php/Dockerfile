FROM php:7.4-fpm

ENV MSSQL_VERSION=18
ENV ACCEPT_EULA=Y
# Install package
RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    gnupg \
    libltdl-dev \
    libpng-dev \
    libzip-dev \
    librabbitmq-dev \
    libicu-dev \
    openssl

RUN apt-get update && apt-get install -y libzip-dev zip && docker-php-ext-install zip
RUN pecl install redis && docker-php-ext-enable redis
# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd mysqli

# Cài đặt Homebrew
# Install Homebrew without sudo check
# RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh --no-sudo)"
# Thêm Microsoft repository
# RUN brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release

# Cập nhật Homebrew
# RUN brew update

# Chấp nhận EULA và cài đặt ODBC Driver và SQL Server tools
# RUN HOMEBREW_ACCEPT_EULA=Y brew install msodbcsql${MSSQL_VERSION} mssql-tools${MSSQL_VERSION}

# RUN apt-get update && apt-get -y install unixodbc unixodbc-dev libltdl-dev
# Install Microsoft ODBC Driver
# RUN apt-get update && \
#     apt-get install -y \
#         curl \
#         lsb-release \
#         ca-certificates \
#         apt-transport-https && \
#     curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
#     curl -fsSL https://packages.microsoft.com/config/ubuntu/20.04/prod.list | tee /etc/apt/sources.list.d/mssql-release.list && \
#     apt-get update && \
#     apt-get install -y \
#         msodbcsql${MSSQL_VERSION} && \
#     apt-get install -y --no-install-recommends mssql-tools${MSSQL_VERSION} && \
#     echo "export PATH=\$PATH:/opt/mssql-tools${MSSQL_VERSION}/bin" >> /root/.bashrc && \
#     apt-get clean && \
#     rm -rf /var/lib/apt/lists/*

# RUN pecl install sqlsrv-5.9.0 pdo_sqlsrv-5.9.0 && docker-php-ext-enable sqlsrv pdo_sqlsrv
RUN apt-get update && apt-get install -y cron
RUN echo "upload_max_filesize = 10M" >> /usr/local/etc/php/conf.d/uploads.ini
RUN echo "post_max_size = 10M" >> /usr/local/etc/php/conf.d/uploads.ini
# RUN echo "extension = sqlsrv.so" >> /usr/local/etc/php/conf.d/sqlsrv.ini
# RUN echo "extension = pdo_sqlsrv.so" >> /usr/local/etc/php/conf.d/sqlsrv.ini
# RUN echo "openssl.cafile=/etc/ssl/certs/ca-certificates.crt" >> /usr/local/etc/php/php.ini
# RUN echo "\n[default_conf]\nssl_conf = ssl_sect\n\n[ssl_sect]\nsystem_default = system_default_sect\n\n[system_default_sect]\nMinProtocol = TLSv1\nCipherString = DEFAULT@SECLEVEL=0" >> /etc/ssl/openssl.cnf

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Permission
RUN chmod -R 777 /var/www/

WORKDIR /var/www

CMD ["php-fpm"]


EXPOSE "9000"
