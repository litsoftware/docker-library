FROM php:7.4-cli

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    wget \
    curl \
    libpng-dev \
    libwebp-dev \
    libjpeg62-turbo-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    libzip-dev \
    libmcrypt-dev \
    libxpm-dev \
    libfreetype6-dev

RUN set -eux; \
    docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp; \
    docker-php-ext-configure intl; \
    docker-php-ext-configure mysqli --with-mysqli=mysqlnd; \
    docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd; \
    docker-php-ext-configure zip; \
    docker-php-ext-install -j "$(nproc)" \
    gd \
    intl \
    mysqli \
    opcache \
    pdo_mysql \
    zip

RUN pecl install zip && \
    docker-php-ext-enable zip && \
    pecl install mcrypt-1.0.3 && \
    docker-php-ext-enable mcrypt 

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd tokenizer sockets xmlrpc shmop sysvsem soap opcache \
    && pecl install mongodb \
    igbinary \
    redis \
    && docker-php-ext-enable redis \
    mongodb \
    igbinary 

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www
