FROM dunglas/frankenphp:php8.3

# Metadata
LABEL org.opencontainers.image.title = "FrankenPHP Docker"
LABEL org.opencontainers.image.description = "FrankenPHP Docker image"
LABEL org.opencontainers.image.url = "https://github.com/fsteltenkamp/frankenphp-docker"
LABEL org.opencontainers.image.source = "https://github.com/fsteltenkamp/frankenphp-docker"

# Install additional packages
RUN apt-get update && \
	apt-get -y --no-install-recommends install \
		git \
		zip \
		unzip \
		libnss3-tools \
	&& \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

# install Nodejs
RUN curl -sL https://deb.nodesource.com/setup_22.x | bash - && \
	apt-get install -y nodejs

# add additional extensions here:
RUN install-php-extensions \
	pdo_mysql \
	gd \
	intl \
	zip \
	redis

# Add Bashrc
COPY .bashrc /root/.bashrc
COPY .bashrc /var/www/.bashrc

# Set permissions
RUN chown -R 33:33 /var/www

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer