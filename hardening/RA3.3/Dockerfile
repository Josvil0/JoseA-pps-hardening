FROM debian:latest

RUN apt-get update && apt-get install -y apache2 openssl && apt-get clean

# Habilitar módulos necesarios para el hardening
RUN a2enmod ssl && a2enmod rewrite && a2enmod headers

# Aplicar configuración de Hardening
COPY hardening.conf /etc/apache2/conf-available/security-hardening.conf
RUN a2enconf security-hardening

# Reutilizamos el certificado de la práctica anterior para que sea HTTPS
RUN mkdir -p /etc/apache2/ssl && \
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/apache2/ssl/apache.key \
    -out /etc/apache2/ssl/apache.crt \
    -subj "/C=ES/ST=Castellon/L=Castellon/O=Caminas/OU=Web/CN=www.caminas.com"

# Configuración del VirtualHost (copia el que ya tenías de la 3.2)
COPY default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
RUN a2dissite 000-default.conf && a2ensite default-ssl.conf
RUN echo "ServerTokens Prod" >> /etc/apache2/apache2.conf
RUN echo "ServerSignature Off" >> /etc/apache2/apache2.conf
EXPOSE 80 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
