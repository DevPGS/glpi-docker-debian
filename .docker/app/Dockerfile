#Scarico debian
FROM debian:12.12

#Install php repo
ARG PHP_VERSION=8.4
RUN apt update \
&& apt install --yes --no-install-recommends \
apt-transport-https \
lsb-release \
ca-certificates \
software-properties-common \
wget

RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'

#Install apache and php with extensions
RUN apt update \
&& apt install --yes --no-install-recommends \
apache2 \
php${PHP_VERSION} \
php${PHP_VERSION}-mysql \
php${PHP_VERSION}-ldap \
php${PHP_VERSION}-xmlrpc \
php${PHP_VERSION}-imap \
curl \
php${PHP_VERSION}-curl \
php${PHP_VERSION}-gd \
php${PHP_VERSION}-mbstring \
php${PHP_VERSION}-xml \
php-cas \
php${PHP_VERSION}-intl \
php${PHP_VERSION}-zip \
php${PHP_VERSION}-bz2 \
php${PHP_VERSION}-bcmath \
cron \
jq \
libldap-common \
libsasl2-2 \
libsasl2-modules \
libsasl2-modules-db \
&& rm -rf /var/lib/apt/lists/*

RUN sed -ri -e 's/(CipherString\s*=\s*DEFAULT)@SECLEVEL=2/\1/' /etc/ssl/openssl.cnf

RUN sed -i "s/session.cookie_httponly =.*/session.cookie_httponly = On/" /etc/php/${PHP_VERSION}/apache2/php.ini

RUN mkdir /var/www/html/error_pages/
COPY 404-internal.html /var/www/html/error_pages/

#Copy and execute GLPI installer and init script
COPY glpi-start.sh /opt/
RUN chmod +x /opt/glpi-start.sh
ENTRYPOINT ["/opt/glpi-start.sh"]

#Expose ports
EXPOSE 80 443
