FROM eu.gcr.io/bienenwanderung/basic-docker-php:0b87b29

# Prepare dummy SSL certificates (local only)
RUN make-ssl-cert generate-default-snakeoil --force-overwrite

# site available configurations files
RUN rm -rf /etc/nginx/sites-available/*
ADD ./files/etc/nginx/sites-available/default.conf /etc/nginx/sites-available/default.conf
ADD ./files/etc/nginx/sites-available/default-ssl.conf /etc/nginx/sites-available/default-ssl.conf
RUN sudo mkdir -p /etc/nginx/sites-enabled
RUN ln -s /etc/nginx/sites-available/default.conf /etc/nginx/sites-enabled/default.conf
RUN ln -s /etc/nginx/sites-available/default-ssl.conf /etc/nginx/sites-enabled/default-ssl.conf

# Copy the nginx config
RUN rm -rf /etc/nginx/nginx.conf
ADD ./files/etc/nginx/conf-available/nginx.conf /etc/nginx/nginx.conf

### Copy Cronjob Files ###
#COPY ./files/etc/cron.daily /etc/cron.daily
#COPY ./files/etc/cron.hourly /etc/cron.hourly
#COPY ./files/etc/cron.weekly /etc/cron.weekly

# Copy the anacron job file (anacron start command got changed
COPY ./files/etc/cron.d/anacron /etc/cron.d/anacron
# COPY ./files/etc/cron.d /etc/cron.d
#RUN chmod -R +x /etc/cron.daily
#RUN chmod -R +x /etc/cron.hourly
#RUN chmod -R +x /etc/cron.weekly
RUN chmod -R 644 /etc/cron.d

RUN mkdir -p /var/www/html

COPY ./project-root/ /var/www/html/

# Set working directory
RUN chown -R www-data:www-data /var/www/html/*

# ensure www-data has access to file from volume if file are mapped as uid/gid 1000/1000 = usermod -u 1000 www-data
RUN usermod -G users www-data

# Clean
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 80 443 9000

CMD ["/usr/bin/supervisord"]
