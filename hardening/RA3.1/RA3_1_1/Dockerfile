FROM ubuntu:22.04

# Evitar prompts interactivos durante la instalación
ENV DEBIAN_FRONTEND=noninteractive

# 1. Instalación de paquetes
RUN apt-get update && \
    apt-get install -y apache2 openssl && \
    apt-get clean

# 2. Habilitar módulos de Apache
RUN a2enmod headers ssl rewrite

# Forzar ocultación de versión y firma (Hardening Global)
RUN sed -i 's/ServerTokens OS/ServerTokens Prod/' /etc/apache2/conf-enabled/security.conf && \
    sed -i 's/ServerSignature On/ServerSignature Off/' /etc/apache2/conf-enabled/security.conf

# Deshabilitar el módulo autoindex por completo
RUN a2dismod autoindex -f

# 3. Generar certificado SSL autofirmado
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/apache-selfsigned.key \
    -out /etc/ssl/certs/apache-selfsigned.crt \
    -subj "/C=ES/ST=Valencia/L=Valencia/O=IES/OU=PPS/CN=localhost"

# 4. Configuración del sitio (Sobreescribir el original de Ubuntu)
COPY default.conf /etc/apache2/sites-available/000-default.conf
RUN a2ensite 000-default.conf

# 5. Archivo de prueba para comprobar el servidor
RUN echo "<h1>RA3.1.1: Apache Hardening (CSP + HSTS)</h1>" > /var/www/html/index.html

EXPOSE 80 443

CMD ["apachectl", "-D", "FOREGROUND"]
