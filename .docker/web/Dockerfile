# has php 7.4
FROM bitnami/symfony:6.0
# COPY prepare-command.sh /prepare-command.sh
RUN apt-get update > /dev/null \
    && apt-get install -y rsync procps net-tools acl > /dev/null \
    && apt-get install -y wget \
    # install symfony installer
    && wget https://get.symfony.com/cli/installer -O - | bash \
    # move installer to bin
    && mv /root/.symfony/bin/symfony /usr/local/bin/symfony

# install mysqldump which is needed for laravel `php artisan schema:dump` command
# RUN apt-get install -y default-mysql-client

# install nodejs
#RUN curl -sL https://deb.nodesource.com/setup_11.x | bash - && \
#    apt-get update && apt-get install -y nodejs

# Install yarn
#RUN apt-get install apt-transport-https && \
#    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
#    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
#    apt-get update && apt-get install --no-install-recommends yarn

ENV PHP_IDE_CONFIG "serverName=application"

# Node
# RUN curl -sL https://deb.nodesource.com/setup_16.x | bash -
# RUN apt-get install -y nodejs

# Remove default xdebug ini
# /etc/php/7.4/cli/conf.d/20-xdebug.ini
COPY my-php-ini/php.ini /etc/php/7.4/cli/conf.d/20-xdebug.ini
COPY my-php-ini/php.ini /etc/php/7.4/fpm/conf.d/20-xdebug.ini

COPY my-php-ini/90-development.ini /etc/php/7.4/cli/conf.d/90-development.ini
COPY my-php-ini/90-development.ini /etc/php/7.4/fpm/conf.d/90-development.ini

# symlink /dev/stdout to xdebug log
# RUN ln -s /dev/stdout /var/log/xdebug.log
# RUN ln -s /var/www/html /app

WORKDIR /app
