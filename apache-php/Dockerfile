FROM rflorent/apache
MAINTAINER Ed Boraas <robson.florentino.silva@gmail.com>

RUN apt-get update && apt-get -y install php php-mysql libapache2-mod-php && apt-get clean && rm -rf /var/lib/apt/lists/* 

RUN /usr/sbin/a2enmod mpm_prefork

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
