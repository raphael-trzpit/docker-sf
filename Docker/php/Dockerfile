FROM php:5.6-fpm

COPY docker-php-pecl-install /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-php-pecl-install
RUN apt-get update

# Install useful extensions
RUN apt-get install -y \
      libfreetype6-dev \
      libjpeg62-turbo-dev \
      libmcrypt-dev \
      libpng12-dev \
  && docker-php-ext-install \
      mcrypt \
      mysqli \
      pdo_mysql \
      mbstring \
  && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install gd

RUN docker-php-pecl-install uploadprogress
RUN docker-php-pecl-install mongo
RUN docker-php-pecl-install xdebug

RUN apt-get install -y zlib1g-dev libicu-dev g++ && \
    docker-php-ext-configure intl && \
    docker-php-ext-install intl && \
    apt-get purge -y g++

# Include composer
RUN apt-get install -y git zlib1g-dev && \
    docker-php-ext-install zip

WORKDIR /var/www
CMD ["php-fpm"]
