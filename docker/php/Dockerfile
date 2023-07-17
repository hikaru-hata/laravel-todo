FROM php:8.2-rc-fpm-alpine3.16
 
# install system dependencies
RUN apk update && echo "y" | apk upgrade
RUN apk add curl libpng-dev libjpeg-turbo-dev freetype-dev zlib-dev oniguruma-dev libxml2-dev zip unzip libzip-dev certbot nano sudo git nodejs npm

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# install php extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath zip gd mysqli
RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/user/include
RUN docker-php-ext-install -j$(nproc) gd
 
# set working directory
WORKDIR /var/www/html
RUN chown -R www-data:www-data /var/www/html