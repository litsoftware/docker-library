FROM php:7.4-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd tokenizer ctype sockets json xmlrpc shmop sysvsem soap opcache \
    && pecl install mongodb \
    igbinary \
    redis \
    && echo yes | pecl install memcached \
    && docker-php-ext-enable redis \
    mongodb \
    igbinary \
    memcached

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www