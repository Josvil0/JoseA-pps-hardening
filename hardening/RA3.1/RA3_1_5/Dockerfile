FROM owasp/modsecurity-crs:nginx

USER root

RUN echo "<?php phpinfo(); ?>" > /usr/share/nginx/html/index.php
USER nginx
