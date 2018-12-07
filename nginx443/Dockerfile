# dockerfile for meshington nginx + cron (release)
FROM ubuntu:18.04
MAINTAINER Chris Quan

# Install nginx
RUN apt-get update
RUN apt-get install -y nginx
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# Define mountable directories.
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx", "/var/www/letsencrypt", "/var/log/cron/"]

# Install certbot
RUN apt-get update --fix-missing
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:certbot/certbot
RUN apt-get update
RUN apt-get install -y certbot

# Install Cron
RUN apt-get update
RUN apt-get install -y cron
RUN apt-get install nano

# Expose ports.
EXPOSE 80
EXPOSE 443

# Cron for certbot renew check every week 
# Wednesday at 5:45pm GMT (Calgary: Wednesday 1:30PM)
RUN echo '\n45 19 * * 1 root printf "\%s: " "$(date "+\%F \%T")" >> /var/log/cron/certbot-renewal.log 2>&1' >> /etc/crontab 2>&1
RUN echo '45 19 * * 1 root certbot renew >> /var/log/cron/certbot-renewal.log 2>&1 && sudo service nginx reload\n' >> /etc/crontab 2>&1

# Create log file
RUN touch /var/log/cron/certbot-renewal.log

# Define working directory.
WORKDIR /etc/nginx

# Copy default file to container
COPY . .

# Entrypoint for cron
RUN chmod +x cron-entrypoint.sh
ENTRYPOINT [ "/etc/nginx/cron-entrypoint.sh" ]

# Define default command.
CMD ["nginx" ]