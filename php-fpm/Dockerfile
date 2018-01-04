FROM laradock/php-fpm:2.0-71
MAINTAINER niming175@qq.com

## Install Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod -R +x /usr/local/bin/composer && \
    echo "" >> ~/.bashrc && \
    echo 'export PATH="~/.composer/vendor/bin:$PATH"' >> ~/.bashrc

## install ext
RUN apt-get update && apt-get install -y zlib1g-dev
RUN docker-php-ext-install zip
RUN docker-php-ext-install pdo_mysql

## redis
RUN printf "\n" | pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis



