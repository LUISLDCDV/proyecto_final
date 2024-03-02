# Utiliza una imagen oficial de PHP
FROM php:7.4-apache

# Instala extensiones de PHP necesarias
RUN docker-php-ext-install pdo pdo_mysql

# Habilita el módulo de Apache para reescritura de URL
RUN a2enmod rewrite

# Establece el directorio de trabajo en el directorio de la aplicación Laravel
WORKDIR /var/www/html

# Copia los archivos del proyecto al contenedor
COPY . .

# Configura permisos adecuados para el directorio de almacenamiento de Laravel
RUN chown -R www-data:www-data storage

# Instala Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Instala las dependencias de Composer
RUN composer install --no-scripts --no-interaction --no-autoloader

# Genera la carga automática de Composer
RUN composer dump-autoload --no-scripts --optimize

# Expone el puerto 80 para la aplicación Laravel
EXPOSE 80

# Ejecuta el servidor Apache al iniciar el contenedor
CMD ["apache2-foreground"]