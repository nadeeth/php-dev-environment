FROM php:7.2.2-apache

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "copy('https://composer.github.io/installer.sig', 'composer-setup.sig');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === trim(file_get_contents('composer-setup.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); unlink('composer-setup.sig'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && mv composer.phar /usr/local/bin/composer \
    && php -r "unlink('composer-setup.php');"

RUN apt-get -y update \
    && apt-get install -y mysql-client

RUN apt-get -y update \
    && apt-get install -y libicu-dev sendmail libpng-dev zlib1g-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install gd

RUN apt-get -y update \
    && apt-get install -y zip \
    && apt-get install -y unzip

RUN apt-get -y update \
    && apt-get -y install git-core

RUN a2enmod rewrite