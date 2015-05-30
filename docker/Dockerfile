FROM ubuntu:trusty
MAINTAINER Sergiy Dragunov <rjhdsy@gmail.com>

# Install packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
  	apt-get --assume-yes --quiet install \
  		supervisor \
  		git \
  		mc \
  		vim \
  		pwgen \
      curl \
      wget \
      mysql-client \
  		mysql-server \
      apache2 \
      php5 \
      libapache2-mod-php5 \
      php5-curl \
      php5-mysql \
      php-apc \
      php5-dev \
      php5-gd \
      php5-imagick

RUN	echo "ServerName localhost" >> /etc/apache2/apache2.conf
RUN echo 'alias ll="ls -lah --color=auto"' >> /etc/bash.bashrc


# It is needed for mc
ENV TERM=xterm

# Add image configuration and scripts
ADD start-apache2.sh /start-apache2.sh
ADD start-mysqld.sh /start-mysqld.sh
ADD run.sh /run.sh
RUN chmod 755 /*.sh
ADD my.cnf /etc/mysql/conf.d/my.cnf
ADD supervisord-apache2.conf /etc/supervisor/conf.d/supervisord-apache2.conf
ADD supervisord-mysqld.conf /etc/supervisor/conf.d/supervisord-mysqld.conf

# Remove pre-installed database
RUN rm -rf /var/lib/mysql/*

# Add MySQL utils
ADD create_mysql_admin_user.sh /create_mysql_admin_user.sh
RUN chmod 755 /*.sh

# config to enable .htaccess
ADD vhost.conf /etc/apache2/sites-available/000-default.conf
RUN a2enmod rewrite

# Configure some folders
#RUN mkdir -p /var/www/html/upload
#RUN chmod 777 /var/www/html/upload
#RUN chown www-data:www-data /var/www/html/upload

#Enviornment variables to configure php
ENV PHP_UPLOAD_MAX_FILESIZE 10M
ENV PHP_POST_MAX_SIZE 10M

# Cleanup
RUN apt-get clean -y; \
    apt-get autoclean -y; \
    apt-get autoremove -y; \
    rm -rf /var/lib/{apt,dpkg,cache,log}/

# Add volumes for MySQL 
VOLUME  ["/etc/mysql", "/var/lib/mysql", "/var/www/html", "/var/www/logs"]
EXPOSE 80 3306
CMD ["/run.sh"]
