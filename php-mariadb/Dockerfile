FROM php:8.5-apache
RUN apt-get update \
  && apt-get install -y --no-install-recommends curl \
  && docker-php-ext-install pdo_mysql \
  && a2enmod rewrite headers \
  && sed -ri 's/Listen 80/Listen 8080/' /etc/apache2/ports.conf \
  && sed -ri 's/<VirtualHost \*:80>/<VirtualHost *:8080>/' /etc/apache2/sites-available/000-default.conf \
  && rm -rf /var/lib/apt/lists/*
WORKDIR /var/www/html
COPY . /var/www/html
RUN chown -R www-data:www-data /var/www/html /var/run/apache2 /var/lock/apache2 /var/log/apache2
USER www-data
EXPOSE 8080
