FROM centos:centos6.6
MAINTAINER Ömer ÜCEL <omerucel@gmail.com>

# Add remi repository
RUN rpm -qa | grep -q epel-release || rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
RUN rpm -qa | grep -q remi-release || rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm

RUN sed -i "s|enabled=1|enabled=0|" /etc/yum/pluginconf.d/fastestmirror.conf

# Configure supervisord
RUN yum --enablerepo=remi install -y supervisor

# Configure PHP
RUN yum --enablerepo=remi-php56,remi install -y \
    gcc \
    make \
    php \
    php-opcache \
    php-apc \
    php-devel \
    pcre-devel \
    php-pear \
    php-pecl-xdebug \
    php-pecl-xhprof \
    php-pecl-memcached \
    php-pecl-mongo \
    php-xml \
    php-gd \
    php-mbstring \
    php-mcrypt \
    php-fpm \
    php-soap \
    php-json

# Install NGINX
RUN yum --enablerepo=remi install -y nginx
RUN rm -rf /etc/nginx/conf.d/default.conf
RUN rm -rf /etc/nginx/conf.d/ssl.conf
RUN rm -rf /etc/nginx/conf.d/virtual.conf

# Install Memcached
RUN yum --enablerepo=remi install -y memcached

# Configure Solo
RUN curl --silent "http://timkay.com/solo/solo" -o /usr/bin/solo
RUN chmod +x /usr/bin/solo

# Configure Mongodb
RUN curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.0.4.tgz
RUN yum install -y tar
RUN tar -zxvf mongodb-linux-x86_64-3.0.4.tgz

# Configure composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

RUN TMPDIR=/tmp yum clean metadata
RUN TMPDIR=/tmp yum clean all