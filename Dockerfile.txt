FROM ubuntu:latest
RUN apt-get update &&  DEBIAN_FRONTEND="noninteractive" TZ="TZ=Europe/Moscow"  apt-get install -y \
 libapache2-mod-php7.4 \
 libapache2-mod-php \
 php-common php-gd \
 php-igbinary \
 php-mbstring \
 php-mysql \
 php-redis \
 php-xml \
 php7.4-cli \
 php7.4-common \
 php7.4-fpm \
 php7.4-gd \
 php7.4-json \
 php7.4-mbstring \
 php7.4-mysql \
 php7.4-opcache \
 php7.4-readline \
 php7.4-xml \
 apache2 \
 nginx \
 mysql-server \
 redis \
 && rm -rf /var/lib/apt/lists/*
 ADD https://www.1c-bitrix.ru/download/files/scripts/bitrixsetup.php  /var/www/html/
 ADD https://raw.githubusercontent.com/102289045/verysimple/main/nginx%20default%20sites.cfg  /etc/nginx/sites-enabled/default
 ADD https://raw.githubusercontent.com/102289045/verysimple/main/php.ini  /etc/php/7.4/apache2/
 RUN  addgroup  bitrix ; useradd -s /usr/sbin/nologin  -d /var/www/html/ -m -g bitrix bitrix  ;sed -i 's/80/127\.0\.0\.1\:88/g'  /etc/apache2/ports.conf ;  sed -i 's/www\-data/bitrix/g' /etc/apache2/envvars ;  sed -i 's/www\-data/bitrix/g' /etc/nginx/nginx.conf  ;  ln -s  ;systemctl enable apache2 ;  systemctl enable nginx
 EXPOSE 8000
