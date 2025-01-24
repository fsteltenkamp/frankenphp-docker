FROM docker.io/dunglas/frankenphp:php8.3

ENV ACCEPT_EULA=Y

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
		gnupg \
	&& \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

# Install MsSQL Driver:
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
	&& curl https://packages.microsoft.com/config/debian/11/prod.list > /etc/apt/sources.list.d/mssql-release.list \
	&& echo "Package: unixodbc\nPin: origin \"packages.microsoft.com\"\nPin-Priority: 100\n" >> /etc/apt/preferences.d/microsoft \
	&& echo "Package: unixodbc-dev\nPin: origin \"packages.microsoft.com\"\nPin-Priority: 100\n" >> /etc/apt/preferences.d/microsoft \
	&& echo "Package: libodbc1:amd64\nPin: origin \"packages.microsoft.com\"\nPin-Priority: 100\n" >> /etc/apt/preferences.d/microsoft \
	&& echo "Package: odbcinst\nPin: origin \"packages.microsoft.com\"\nPin-Priority: 100\n" >> /etc/apt/preferences.d/microsoft \
	&& echo "Package: odbcinst1debian2:amd64\nPin: origin \"packages.microsoft.com\"\nPin-Priority: 100\n" >> /etc/apt/preferences.d/microsoft \
	&& apt-get update \
	&& apt-get install -y msodbcsql18 mssql-tools18 unixodbc-dev \
	&& rm -rf /var/lib/apt/lists/*

# install Nodejs
RUN curl -sL https://deb.nodesource.com/setup_22.x | bash - && \
	apt-get install -y nodejs

# add additional extensions here:
RUN install-php-extensions \
	pdo_mysql \
	gd \
	intl \
	zip \
	redis \
	sqlsrv \
	pdo_sqlsrv

# Add Bashrc
COPY .bashrc /root/.bashrc
COPY .bashrc /var/www/.bashrc

# Set permissions
RUN chown -R 33:33 /var/www

# Install Composer
COPY --from=docker.io/composer:latest /usr/bin/composer /usr/local/bin/composer
