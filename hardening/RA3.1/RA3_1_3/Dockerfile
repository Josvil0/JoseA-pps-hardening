FROM josea13/pps:pr3.1.2

# Instalamos git y preparamos OWASP
RUN apt-get update && apt-get install -y git && apt-get clean
WORKDIR /opt
RUN git clone https://github.com/SpiderLabs/owasp-modsecurity-crs.git
RUN cp owasp-modsecurity-crs/crs-setup.conf.example /etc/modsecurity/crs-setup.conf && \
    cp -r owasp-modsecurity-crs/rules /etc/modsecurity/

# Configuración de carga sin duplicados
RUN echo '<IfModule security2_module>\n\
    SecDataDir /var/cache/modsecurity\n\
    SecRuleEngine On\n\
    Include /etc/modsecurity/modsecurity.conf\n\
    Include /etc/modsecurity/crs-setup.conf\n\
    Include /etc/modsecurity/rules/*.conf\n\
</IfModule>' > /etc/apache2/mods-enabled/security2.conf




RUN a2ensite default.conf

WORKDIR /var/www/html
