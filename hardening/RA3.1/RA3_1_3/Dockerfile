FROM josea13/pps:pr3.1.2

# 1. Instalación de dependencias y reglas OWASP CRS
RUN apt-get update && apt-get install -y git && apt-get clean
WORKDIR /opt
RUN git clone https://github.com/SpiderLabs/owasp-modsecurity-crs.git

# 2. Despliegue de configuración y reglas
RUN cp owasp-modsecurity-crs/crs-setup.conf.example /etc/modsecurity/crs-setup.conf && \
    cp -r owasp-modsecurity-crs/rules /etc/modsecurity/

# 3. Configuración de carga de módulos y reglas
RUN echo '<IfModule security2_module>\n\
    SecDataDir /var/cache/modsecurity\n\
    SecRuleEngine On\n\
    IncludeOptional /etc/modsecurity/*.conf\n\
    Include /etc/modsecurity/rules/*.conf\n\
</IfModule>' > /etc/apache2/mods-enabled/security2.conf

# 4. Inyección de la REGLA PERSONALIZADA
RUN sed -i '/<\/VirtualHost>/i SecRuleEngine On\nSecRule ARGS:testparam "@contains test" "id:1234,deny,status:403,msg:Cazado_por_Ciberseguridad"' /etc/apache2/sites-available/000-default.conf

WORKDIR /var/www/html
