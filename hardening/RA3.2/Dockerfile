FROM debian:latest

RUN apt-get update && apt-get install -y apache2 openssl && apt-get clean

RUN a2enmod ssl && a2enmod rewrite

# Crear carpeta y generar certificado
RUN mkdir -p /etc/apache2/ssl
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/apache2/ssl/apache.key \
    -out /etc/apache2/ssl/apache.crt \
    -subj "/C=ES/ST=Castellon/L=Castellon/O=Caminas/OU=Web/CN=www.caminas.com"

# Contenido de prueba
RUN echo "<h1>Bienvenido a Caminas Web Projects (Seguro)</h1>" > /var/www/html/index.html

# Configuración de sitio
COPY default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
RUN a2dissite 000-default.conf && a2ensite default-ssl.conf
RUN echo "ServerName www.caminas.com" >> /etc/apache2/apache2.conf

EXPOSE 80 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
