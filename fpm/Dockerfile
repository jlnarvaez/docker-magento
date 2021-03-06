FROM php:7.1-fpm
RUN apt-get update && apt-get install -y \
	sudo \
	git \
	bzip2 \
	cron \
	wget \
  acl \
  procps \
	libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        libxml2-dev \
        libcurl4-openssl-dev \
	libxslt-dev \
	libicu-dev \
	nano \
	vim \
    gnupg \
    && docker-php-ext-install -j$(nproc) iconv mcrypt curl dom hash pdo pdo_mysql mysqli simplexml soap xsl intl zip opcache bcmath \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# ssmtp
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y ssmtp

# mysql-client
RUN apt-get update && apt-get install -y mysql-client && rm -rf /var/lib/apt

# Xdebug
RUN pecl install xdebug-2.6.1 \
  &&  docker-php-ext-enable xdebug
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
RUN chmod 777 /usr/local/etc/php/conf.d/xdebug.ini

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Node.js
RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
RUN apt-get install -y nodejs

#npm
RUN npm install -g npm@latest

# Grunt
RUN npm install -g grunt-cli

# Magerun 2
RUN wget https://files.magerun.net/n98-magerun2.phar \
&& chmod +x ./n98-magerun2.phar \
&& mv ./n98-magerun2.phar /usr/local/bin/

# Pestle
RUN curl -LO http://pestle.pulsestorm.net/pestle.phar \
&& chmod +x ./pestle.phar \
&& mv ./pestle.phar /usr/local/bin/

# Mage2tv Cache Clean
RUN composer global require --dev mage2tv/magento-cache-clean \
&& export PATH="$PATH:$HOME/.composer/vendor/bin" \
&& echo 'alias cache-clean="$HOME/.composer/vendor/bin/cache-clean.js"' >> ~/.bashrc
