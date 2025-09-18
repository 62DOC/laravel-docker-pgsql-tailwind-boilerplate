# .docker/php/Dockerfile - VERSÃO CORRIGIDA

FROM php:8.2-fpm

# Instalar dependências do sistema e do PHP
RUN apt-get update && apt-get install -y \
    build-essential \
    libpq-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    unzip \
    git \
    curl \
    libonig-dev

# ---- NOVAS LINHAS PARA INSTALAR NODE.JS E NPM ----
RUN curl -sL https://deb.nodesource.com/setup_20.x | bash -
RUN apt-get install -y nodejs
# --------------------------------------------------

# Limpar cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Instalar extensões PHP
RUN docker-php-ext-install pdo_pgsql pgsql mbstring exif pcntl bcmath gd

# Instalar Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Definir diretório de trabalho
WORKDIR /var/www

# Alterar o dono do diretório para o usuário www-data
RUN chown -R www-data:www-data /var/www

# Expor a porta 9000 e iniciar o servidor PHP-FPM
EXPOSE 9000
CMD ["php-fpm"]