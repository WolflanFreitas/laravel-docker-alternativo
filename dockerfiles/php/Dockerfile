FROM 8.3.20-fpm-alpine3.20

# Instalar dependências do sistema
RUN apk add --no-cache \
  bash \
  curl \
  libpng-dev \
  libzip-dev \
  zlib-dev \
  postgresql-dev \
  libmemcached-dev \
  oniguruma-dev \
  linux-headers

# Instalar extensões PHP
RUN docker-php-ext-install gd \
  && docker-php-ext-install zip \
  && docker-php-ext-install pdo_mysql \
  && docker-php-ext-install pdo_pgsql

# Instalar extensões PECL
RUN pecl install redis \
  && pecl install memcached \
  && docker-php-ext-enable redis memcached

# Instalar Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Instalar Node.js e npm
RUN apk add --no-cache nodejs npm

# Configurar healthcheck
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 \
  CMD php-fpm -t || exit 1

# Definir diretório de trabalho
WORKDIR /var/www

EXPOSE 9000
