FROM php:7.4-apache

RUN sed -i -e 's/deb.debian.org/archive.debian.org/g' \
           -e 's/security.debian.org/archive.debian.org/g' \
           -e 's/security-cdn.debian.org/archive.debian.org/g' \
           -e '/-updates/d' \
           -e '/debian-security/d' \
           /etc/apt/sources.list /etc/apt/sources.list.d/*.list 2>/dev/null || true \
    && apt-get update -o Acquire::Check-Valid-Until=false -o Acquire::AllowInsecureRepositories=true && apt-get install -y \
    libonig-dev \
    libzip-dev \
    git \
    vim \
    unzip \
    && docker-php-ext-install pdo_mysql mysqli mbstring zip \
    && a2enmod rewrite

WORKDIR /var/www/src

COPY --from=composer:2.2.5 /usr/bin/composer /usr/bin/composer