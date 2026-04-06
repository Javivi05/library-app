FROM php:8.2-cli

RUN apt-get update && apt-get install -y \
    unzip \
    curl \
    libzip-dev \
    && docker-php-ext-install zip pdo pdo_mysql

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

COPY . /var/www

RUN composer install --no-dev --optimize-autoloader

RUN touch /var/www/database/database.sqlite && php artisan migrate --force

EXPOSE 8000

CMD php artisan serve --host 0.0.0.0 --port $PORT