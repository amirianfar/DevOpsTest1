FROM ubuntu:latest
MAINTAINER Milad

# RUN echo "nameserver 8.8.8.8" > /etc/resolv.conf 
RUN apt-get update \
 && apt-get install -y locales \
 && apt-get install -y apache2 \
 && apt-get install -y apache2-utils \
 && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 

RUN rm -rf /var/lib/apt/lists/* \
 && apt clean 

ENV LANG en_US.utf8
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]


