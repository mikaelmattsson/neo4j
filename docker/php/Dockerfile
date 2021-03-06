FROM php:7.0-fpm

# install the PHP extensions we need
RUN apt-get update && apt-get install -y libpng12-dev libjpeg-dev ssmtp && rm -rf /var/lib/apt/lists/* \
	&& docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr \
	&& docker-php-ext-install gd opcache bcmath mbstring

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=60'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

COPY php.ini /usr/local/etc/php/conf.d/php.ini
COPY ssmtp.conf /etc/ssmtp/ssmtp.conf
COPY revaliases /etc/ssmtp/revaliases
