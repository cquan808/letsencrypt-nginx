# dockerfile for meshington letsencrypt cron
FROM ubuntu:18.04
MAINTAINER Chris Quan

# Install nginx
RUN apt-get update
RUN apt-get install -y nginx
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# Define mountable directories
VOLUME ["/etc/nginx/certs", "/var/www/letsencrypt", "/etc/letsencrypt"]
#VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/conf.d", "/var/log/nginx"]

# Install certbot
RUN apt-get update --fix-missing
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:certbot/certbot
RUN apt-get update
RUN apt-get install -y certbot

# Expose ports.
EXPOSE 80

# Define working directory.
WORKDIR /etc/nginx

# Copy default file to container
COPY . .

# Define default command.
CMD ["nginx"]