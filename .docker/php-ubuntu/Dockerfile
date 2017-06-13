FROM ubuntu:16.04

RUN apt-get update -y --fix-missing

# Install tools
RUN apt-get install -y \
    software-properties-common \
    python-software-properties \
    build-essential \
    language-pack-en-base \
    net-tools \
    vim \
    curl sudo

# Add nodejs repository
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
RUN sudo apt-get install -y nodejs

# Add ondrej's php repository
RUN LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php
RUN apt-get update -y

# Install php7
RUN apt-get install -y --force-yes \
    php7.0 \
    php7.0-cli \
    php7.0-fpm \
    php7.0-bcmath \
    php7.0-curl \
    php7.0-gd \
    php7.0-intl \
    php7.0-mbstring \
    php7.0-mcrypt \
    php7.0-xml \
    php7.0-xsl \
    php7.0-soap \
    php7.0-zip \
    php7.0-mysql \
    php7.0-json \
    php7.0-iconv \
    php7.0-xdebug

# Configure php-fpm
RUN mkdir /run/php && \
    ln -s /usr/sbin/php-fpm7.0 /usr/sbin/php-fpm

# Install php-fpm pool
COPY config/www.conf /etc/php/7.0/fpm/pool.d/
COPY config/uploads.ini /etc/php/7.0/fpm/conf.d/
RUN chmod 777 /etc/php/7.0/fpm/conf.d/uploads.ini

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --install-dir=/usr/bin/ --filename=composer
RUN php -r "unlink('composer-setup.php');"

# Install composer auth
RUN mkdir -p /root/.composer

# Install magento cron jobs
COPY cron-magento /etc/cron.d/

RUN usermod -u 1000 www-data

ENTRYPOINT ["php-fpm","-F","-R"]

EXPOSE 9000
