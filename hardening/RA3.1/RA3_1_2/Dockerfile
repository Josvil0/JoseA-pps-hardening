FROM josea13/pps:pr3.1.1

RUN apt-get update && \
    apt-get install -y libapache2-mod-security2 php libapache2-mod-php && \
    apt-get clean

RUN cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf

RUN sed -i 's/SecRuleEngine DetectionOnly/SecRuleEngine On/' /etc/modsecurity/modsecurity.conf

COPY test.php /var/www/html/test.php
