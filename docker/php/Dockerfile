# Image PHP 8.5 + Apache pour le projet Symfony (dev)
FROM php:8.5-apache

# Extensions PHP nécessaires à Symfony + MariaDB (OPcache est intégré à PHP 8.5)
COPY --from=mlocati/php-extension-installer:2 /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions pdo_mysql intl zip gd

# Composer
COPY --from=composer:2 /usr/bin/composer /usr/local/bin/composer

# Apache : racine web sur public/, toutes les URL vers index.php (routes Symfony)
ENV APACHE_DOCUMENT_ROOT=/var/www/html/public
RUN sed -ri 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf \
    && printf '<Directory ${APACHE_DOCUMENT_ROOT}>\n    AllowOverride None\n    FallbackResource /index.php\n</Directory>\n' > /etc/apache2/conf-available/symfony.conf \
    && a2enconf symfony \
    && a2enmod rewrite

# www-data prend l'UID de l'utilisateur WSL : var/cache et var/log restent modifiables des deux côtés
ARG UID=1000
RUN usermod -u ${UID} www-data && groupmod -g ${UID} www-data

WORKDIR /var/www/html
