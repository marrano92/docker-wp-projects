FROM wordpress

# Arguments defined in docker-compose.yml
ARG user
ARG uid

# Install packages under Debian
RUN apt-get update && \
    apt-get -y install git

# Install xdebug and active on container
RUN pecl channel-update pecl.php.net
RUN pecl install xdebug-2.8.0
RUN docker-php-ext-enable xdebug

# Create system user to run Composer and Artisan Commands
RUN useradd -G www-data,root -u $uid -d /home/$user $user
RUN mkdir -p /home/$user/.composer && \
    chown -R $user:$user /home/$user

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

USER $user