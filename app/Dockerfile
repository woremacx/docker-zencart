FROM php:5.6.31-apache

RUN apt-get update && apt-get install -y \
       curl \
       unzip \
       apt-utils \
       zlib1g-dev \
       libpng12-dev \
       libmcrypt-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-source extract \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo pdo_mysql \
    && docker-php-ext-install zip \
    && docker-php-ext-install gd \
    && docker-php-ext-install mcrypt \
    && docker-php-ext-install opcache
RUN a2enmod rewrite

WORKDIR /tmp
RUN curl -LO https://jaist.dl.sourceforge.net/project/zencart/CURRENT%20-%20Zen%20Cart%201.5.x%20Series/zen-cart-v1.5.5e-03082017.zip \
    && unzip zen-cart-v1.5.5e-03082017.zip \
    && rm -f zen-cart-v1.5.5e-03082017.zip \
    && rm -rf /var/www/html \
    && mv zen-cart-v1.5.5e-03082017 /var/www/html \
    && cd /var/www/html \
    && cp includes/dist-configure.php includes/configure.php \
    && cp admin/includes/dist-configure.php admin/includes/configure.php \
    && chown -R www-data:www-data /var/www/html

RUN echo '[Date]' > /usr/local/etc/php/conf.d/timezone.ini \
 && echo 'date.timezone = "Asia/Tokyo"' >> /usr/local/etc/php/conf.d/timezone.ini \
