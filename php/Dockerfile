FROM php:7.2-apache
ENV APACHE_DOCUMENT_ROOT /var/www/html/public

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN a2enmod rewrite

RUN apt-get update && \
    apt-get install -y git zip unzip gzip

EXPOSE 80

workdir /var/www/

COPY init.sh .
COPY lista_relevancia_1.txt .
COPY lista_relevancia_2.txt .
RUN chmod +x init.sh

RUN curl --output users.csv.gz https://s3.amazonaws.com/careers-picpay/users.csv.gz

#COPY ./users.csv.gz /var/www/

CMD ./init.sh
