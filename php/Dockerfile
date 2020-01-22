FROM php:7.4-fpm-alpine

ENV TZ Asia/Jakarta

# Install dev dependencies
RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    curl-dev \
    imagemagick-dev \
    libtool \
    libxml2-dev

# Install production dependencies
RUN apk add --no-cache \
    bash \
    curl \
    freetype-dev \
    g++ \
    gcc \
    git \
    imagemagick \
    libc-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libzip-dev \
    make \
    mysql-client \
    nodejs \
    nodejs-npm \
    oniguruma-dev \
    yarn \
    openssh-client \
    rsync \
    zlib-dev

# Install PECL and PEAR extensions
RUN pecl install \
    imagick \
    xdebug \
    redis

# Enable PECL and PEAR extensions
RUN docker-php-ext-enable \
    imagick \
    xdebug \
    redis

# Configure php extensions
RUN docker-php-ext-configure gd --with-freetype --with-jpeg

# Install php extensions
RUN docker-php-ext-install \
    bcmath \
    calendar \
    curl \
    exif \
    gd \
    iconv \
    mbstring \
    pdo \
    pdo_mysql \
    pcntl \
    tokenizer \
    xml \
    zip

# Install composer
ENV COMPOSER_HOME /composer
ENV PATH ./vendor/bin:/composer/vendor/bin:$PATH
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

# Cleanup dev dependencies
RUN apk del -f .build-deps

# Setup working directory
WORKDIR /var/www/html