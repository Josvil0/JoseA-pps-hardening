FROM ubuntu:22.04

# 1. Instalación de paquetes
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y apache2 openssl ca-certificates && \
    apt-get clean

# 2. ACTIVACIÓN Y DESACTIVACIÓN
RUN a2enmod headers ssl rewrite
RUN yes "Yes, do as I say!" | a2dismod autoindex || a2dismod -f autoindex

# 3. Generar certificado SSL
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/apache-selfsigned.key \
    -out /etc/ssl/certs/apache-selfsigned.crt \
    -subj "/C=ES/ST=Castellon/L=Valencia/O=IES/OU=PPS/CN=localhost"

# 4. Copiar configuración
COPY default.conf /etc/apache2/sites-available/default.conf
RUN a2ensite default.conf

# 5. Index de prueba
RUN echo "<h1>Servidor Apache Hardened - PR 3.1.1</h1>" > /var/www/html/index.html

EXPOSE 80 443

CMD ["apachectl", "-D", "FOREGROUND"]
