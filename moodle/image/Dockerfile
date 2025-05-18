FROM php:8.3.21-apache

RUN apt-get update \
    && apt-get install -y libpng-dev libjpeg-dev libpq-dev \
                          graphviz aspell libpspell-dev git-core \
    && apt-get install -y libicu-dev libxml2-dev libcurl4-openssl-dev \
                          libldap2-dev \
    && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu \
#    && docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
    && docker-php-ext-install intl pdo curl ldap pgsql gd opcache soap \
    && docker-php-ext-enable opcache 

RUN apt-get install -y git


RUN apt-get install -y libzip-dev
RUN docker-php-ext-install zip exif

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

RUN sed -i 's/;max_input_vars = 1000/max_input_vars = 5000/' "$PHP_INI_DIR/php.ini"

RUN git clone -b MOODLE_500_STABLE --depth 1 https://github.com/moodle/moodle /var/www/html

RUN chown -R www-data:www-data /var/www/html
RUN mkdir /var/www/moodledata && chmod 2775 /var/www/moodledata && chown -R www-data:www-data /var/www/moodledata

COPY config.php /var/www/html

RUN a2enmod rewrite
