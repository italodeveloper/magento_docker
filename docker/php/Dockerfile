FROM php:7.2-fpm

# Install required librairies
RUN apt-get update \
    && apt-get install -y -q --no-install-recommends \
    bison \
    libxml2-dev \
    libicu-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libcurl4-gnutls-dev \
    libbz2-dev \
    libssl-dev \
    libmcrypt-dev \
    libmagickwand-dev \
    apt-transport-https \
    build-essential \
    ca-certificates \
    curl \
    python \
    rsync \
    cron \
    supervisor \
    wget \
    locales \
    software-properties-common \
    zlib1g-dev \
    haproxy \
    telnet
#      && rm -rf /var/lib/apt/lists/*

# Install php extensions
RUN docker-php-ext-install pdo_mysql \
    pdo \
    opcache \
    calendar \
    bcmath \
    gd \
    zip \
    curl \
    soap \
    bz2 \
    intl

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Configure PHP extensions
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

RUN docker-php-ext-configure opcache --enable-opcache \
    && docker-php-ext-install opcache

RUN apt-get update \ 
    && pecl channel-update pecl.php.net \
    && pecl install mongodb 

RUN apt-get update \ 
    && pecl install redis \
    && docker-php-ext-enable redis

RUN apt-get update \
    && apt-get install -y -q --no-install-recommends \
    gcc \
    make \
    autoconf \
    libc-dev \
    pkg-config

RUN pecl install mcrypt-1.0.1


# Install PHP extensions
RUN docker-php-ext-install pdo pdo_mysql zip gd intl curl soap

# Import custom php.ini
COPY ./php.ini /usr/local/etc/php/

WORKDIR /var/www