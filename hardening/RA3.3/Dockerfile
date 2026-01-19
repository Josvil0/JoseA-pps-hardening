FROM debian:latest

# 1. Instalar Apache
RUN apt-get update && apt-get install -y apache2 && apt-get clean

# 2. Activar módulos necesarios
RUN a2enmod headers

# 3. Aplicar tu configuración de Hardening
COPY hardening.conf /etc/apache2/conf-available/hardening.conf
RUN a2enconf hardening

# --- EL CAMBIO CLAVE AQUÍ ---
# Desactivamos el archivo de seguridad por defecto de Debian que sobreescribe tus cambios
RUN a2disconf security
# ----------------------------

# 4. Forzar las directivas globales al final del archivo principal
RUN echo "ServerTokens Prod" >> /etc/apache2/apache2.conf
RUN echo "ServerSignature Off" >> /etc/apache2/apache2.conf
RUN echo "TraceEnable Off" >> /etc/apache2/apache2.conf

# 5. Permisos y archivos de prueba
RUN chown -R www-data:www-data /var/www/html
RUN mkdir -p /var/www/html/secreto
RUN touch /var/www/html/secreto/archivo_privado.txt

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
