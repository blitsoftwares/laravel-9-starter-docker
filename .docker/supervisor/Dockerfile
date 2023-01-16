FROM php:8.1-fpm

WORKDIR /var/www

RUN rm -rf /var/www/html
RUN ln -s public html

ADD programs.conf /etc/supervisor/conf.d/programs.conf
ADD manage-supervisord /usr/local/bin/manage-supervisord

RUN docker-php-ext-install pdo_mysql \
    && docker-php-ext-install bcmath \
    && apt-get update \
    && apt-get install -y supervisor

RUN mkdir -p /var/log/supervisor
RUN chmod 777 /var/log/supervisor

COPY . /var/www

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/programs.conf"]
