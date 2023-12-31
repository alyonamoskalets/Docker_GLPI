# syntax=docker/dockerfile:1

FROM debian:latest
RUN apt-get update -y && apt-get install -y nginx \
    && apt-get install -y libnginx-mod-stream-geoip libnginx-mod-http-geoip libnginx-mod-stream libnginx-mod-mail libnginx-mod-http-xslt-filter libnginx-mod-http-image-filter
COPY /etc/ssl /etc/ssl
COPY /etc/nginx /etc/nginx
COPY /var/www/html /var/www/html
COPY --chown=www-data:www-data --chmod=777 /var/www/glpi /var/www/glpi
RUN chown www-data:www-data /var/www/html/marketplace && chmod 755 /var/www/html/marketplace
RUN apt-get update -y && apt-get install -y --no-install-recommends php php-fpm php-curl php-cli php-zip php-mysql php-xml php-ldap php-xmlrpc php-gd php-intl php-bz2 php-mbstring \
    && sed -i 's/max_execution_time = 30/max_execution_time = 600/' /etc/php/8.2/cli/php.ini \
    && sed -i 's/;session.cookie_secure =/session.cookie_secure = on/' /etc/php/8.2/cli/php.ini \
    && sed -i 's/session.cookie_httponly =/session.cookie_httponly = on/' /etc/php/8.2/cli/php.ini \
    && sed -i 's/session.cookie_httponly =/session.cookie_httponly = on/' /etc/php/8.2/fpm/php.ini \
    && sed -i 's/session.cookie_httponly =/session.cookie_httponly = on/' /etc/php/8.2/fpm/php.ini \
    && rm /var/www/html/index.nginx-debian.html
COPY ["start.sh", "/glpi/start.sh"]
RUN chmod +x /glpi/start.sh
EXPOSE 80 443
CMD ["/glpi/start.sh"]