FROM josea13/pps:pr3.1.3

# 1. Instalamos el módulo mod_evasive
RUN apt-get update && apt-get install -y libapache2-mod-evasive && apt-get clean

# 2. Creamos el directorio de bloqueo (Obligatorio para que funcione)
RUN mkdir -p /var/log/mod_evasive && chown -R www-data:www-data /var/log/mod_evasive

# 3. Configuración agresiva para testeo:
# Bloquea si pide la misma página más de 2 veces por segundo (DOSPageCount 2)
RUN echo '<IfModule mod_evasive24.c>\n\
    DOSHashTableSize    3097\n\
    DOSPageCount        2\n\
    DOSSiteCount        50\n\
    DOSPageInterval     1\n\
    DOSSiteInterval     1\n\
    DOSBlockingPeriod   10\n\
    DOSLogDir           "/var/log/mod_evasive"\n\
</IfModule>' > /etc/apache2/mods-available/evasive.conf

# 4. Activamos el módulo
RUN a2enmod evasive

WORKDIR /var/www/html
