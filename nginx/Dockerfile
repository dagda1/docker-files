FROM ubuntu:14.04

RUN echo "Europe/London" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata 

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get install -y nginx
RUN apt-get install -y supervisor
RUN apt-get install -y nginx
RUN apt-get install -y supervisor
RUN apt-get update && apt-get -q -y install lsof
RUN apt-get install net-tools
RUN apt-get install psmisc
RUN apt-get -y install curl

RUN rm -Rf /etc/nginx/conf.d/*
RUN rm /etc/nginx/sites-enabled/default

RUN mkdir /etc/nginx/logs/
RUN touch /etc/nginx/logs/error.log

RUN mkdir /usr/share/nginx/logs/
RUN touch /usr/share/nginx/logs/error.log

ADD ./conf/nginx.conf /etc/nginx/sites-available/default
RUN ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled/default

ADD supervisor.nginx.conf /etc/supervisor.d/nginx.conf

EXPOSE 80
CMD /usr/bin/supervisord -n