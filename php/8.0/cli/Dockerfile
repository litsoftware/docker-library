FROM php:8.0-cli

# Install system dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    git \
    wget \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    libzip-dev \
    libmcrypt-dev \
    libwebp-dev \
    libjpeg62-turbo-dev \
    libxpm-dev \
    libfreetype6-dev

# Install freetype
RUN wget "https://download.savannah.gnu.org/releases/freetype/freetype-2.10.0.tar.bz2" && \
    tar jxvf freetype-2.10.0.tar.bz2 && \
    cd freetype-2.10.0 && \
    ./configure --prefix=/usr/local/freetype && make && make install

RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp

RUN pecl install zip && \
    docker-php-ext-enable zip && \
    pecl install mcrypt-1.0.4 && \
    docker-php-ext-enable mcrypt 

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath tokenizer sockets shmop sysvsem soap opcache \
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
