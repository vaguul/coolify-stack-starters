FROM php:8.5-apache
RUN apt-get update \
  && apt-get install -y --no-install-recommends curl \
  && docker-php-ext-install pdo_mysql \
  && a2enmod rewrite headers \
  && rm -rf /var/lib/apt/lists/*
WORKDIR /var/www/html
COPY . /var/www/html
EXPOSE 80
