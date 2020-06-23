FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive
# version 1:4.2.8-0ubuntu2

RUN apt-get update && apt-get -y -q install libreoffice libreoffice-writer ure libreoffice-java-common libreoffice-core libreoffice-common openjdk-8-jre fonts-opensymbol hyphen-fr hyphen-de hyphen-en-us hyphen-it hyphen-ru fonts-dejavu fonts-dejavu-core fonts-dejavu-extra fonts-noto fonts-dustin fonts-f500 fonts-fanwood fonts-freefont-ttf fonts-liberation fonts-lmodern fonts-lyx fonts-sil-gentium fonts-texgyre fonts-tlwg-purisa && apt-get -q -y remove libreoffice-gnome
EXPOSE 8997

RUN adduser --home=/opt/libreoffice --disabled-password --gecos "" --shell=/bin/bash libreoffice

RUN apt-get update && apt-get install -y apache2

RUN apt-get install -y software-properties-common

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 6494C6D6997C215E

RUN apache2 -v

RUN apt-get update && apt-get install -y php7.2 apt-utils

RUN apt-get install -y php7.2-mbstring php7.2-curl php7.2-cli php7.2-mysql php7.2-gd php7.2-intl php7.2-xsl php7.2-zip libapache2-mod-php7.2

RUN apt-get install -y php7.2-pdo php7.2-xml php7.2-xmlrpc php7.2-xmlreader php7.2-xmlwriter php7.2-soap


ENV APACHE_CONFDIR /etc/apache2
ENV APACHE_ENVVARS $APACHE_CONFDIR/envvars

RUN set -ex \
    && . "$APACHE_ENVVARS" \
	&& ln -sfT /dev/stderr "$APACHE_LOG_DIR/error.log" \
	&& ln -sfT /dev/stdout "$APACHE_LOG_DIR/access.log" \
	&& ln -sfT /dev/stdout "$APACHE_LOG_DIR/other_vhosts_access.log"


# Copy config-config sites yang dimau
COPY config/apache2.config /etc/apache2/apache2.conf
COPY config/ports.config /etc/apache2/ports.conf

RUN a2enmod rewrite
COPY config/php.ini /etc/php/7.2/cli/php.ini

WORKDIR /var/www/html
COPY apache2-foreground /usr/local/bin/
EXPOSE 80
EXPOSE 8080
RUN service apache2 restart
RUN chmod 755 /usr/local/bin/apache2-foreground
COPY module/jsignpdf /home/jsignpdf
CMD ["apache2-foreground"]
