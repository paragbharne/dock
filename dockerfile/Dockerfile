FROM ubuntu:14.04
MAINTAINER Parag Bharne<pari.bharne>


RUN apt-get -y update && apt-get -y upgrade 
RUN apt-get -y install apache2 
RUN apt-get install -y nano  php5 libapache2-mod-php5 php5-mysql php5-curl php5-gd php5-intl php-pear 
RUN apt-get install -y php5-imagick php5-imap php5-mcrypt php5-memcache php5-ming php5-ps php5-pspell php5-recode php5-sqlite 
RUN apt-get install -y php5-tidy php5-xmlrpc php5-xsl 
RUN apt-get install -y git openssl  && apt-get install -y supervisor
RUN apt-get install -y mysql-client


ADD 000-default.conf /etc/apache2/sites-enabled
ADD /wordpress /var/www/
ADD wp-config.php /var/www/
#RUN mkdir /var/www/html/wp-content/uploads
#RUN chown -R :www-data /var/www/html 
#ADD /word /var/www/html


EXPOSE 80
ENTRYPOINT ["apachectl"]
CMD ["-D" , "FOREGROUND"]
