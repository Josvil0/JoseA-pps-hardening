FROM owasp/modsecurity-crs:nginx

USER root

RUN apt-get update && apt-get install -y php-fpm apache2-utils && apt-get clean

RUN mkdir -p /var/www/html/protegido && \
    echo "<?php phpinfo(); ?>" > /var/www/html/index.php && \
    echo "<h1>Area Protegida</h1>" > /var/www/html/protegido/index.html

RUN htpasswd -bc /etc/nginx/.htpasswd jose pps

# Copiamos tu config limpia a la carpeta de templates
COPY default.conf /etc/nginx/templates/conf.d/default.conf.template

RUN mkdir -p /var/run/php && chown www-data:www-data /var/run/php && \
    PHP_VERSION=$(ls /etc/php/) && \
    sed -i "s|listen = /run/php/php${PHP_VERSION}-fpm.sock|listen = /var/run/php/php-fpm.sock|" /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf

CMD ["sh", "-c", "service $(ls /etc/init.d/ | grep php) start && /docker-entrypoint.sh nginx -g 'daemon off;'"]
