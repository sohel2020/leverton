FROM ubuntu:16.04

RUN DEBIAN_FRONTEND=noninteractive apt-get update \
    && apt-get install -y --no-install-recommends apache2 \
    && rm -rf /var/lib/apt/lists/*


# Remove default VirtualHost
RUN rm -rf /etc/apache2/sites-enabled/000-default.conf /var/www/html

RUN a2enmod headers rewrite proxy proxy_ajp proxy_balancer lbmethod_byrequests ssl
ADD 000-default.conf /etc/apache2/sites-enabled/
ADD apache2.conf /etc/apache2/
ADD docker.crt /etc/apache2/ssl/
ADD docker.key /etc/apache2/ssl/
ADD .htaccess /etc/apache2/.htaccess
# Configure Apache2
ENV APACHE_RUN_USER     www-data
ENV APACHE_RUN_GROUP    www-data
ENV APACHE_LOG_DIR      /var/log/apache2
ENV APACHE_PID_FILE     /var/run/apache2.pid
ENV APACHE_RUN_DIR      /var/run/apache2
ENV APACHE_LOCK_DIR     /var/lock/apache2
ENV APACHE_LOG_DIR      /var/log/apache2

# Expose ourselves
EXPOSE 80 443

CMD ["apachectl", "-D", "FOREGROUND"]
