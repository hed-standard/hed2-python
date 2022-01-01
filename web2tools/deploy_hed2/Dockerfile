FROM python:3.8-slim-buster
COPY ./requirements.txt /root/
WORKDIR /root
RUN apt-get update && apt-get install -y gcc \
musl-dev \
openrc \
libxslt-dev \
libxml2-dev \
apache2 \
apache2-dev && \
pip3 install --upgrade pip && \
pip3 install --no-cache-dir -r requirements.txt && \
mkdir -p /var/www/localhost/htdocs && \
cp /etc/mime.types /var/www/mime.types && \
mkdir -p /var/log/hed2tools && \
chown -R www-data:www-data /var/log/hed2tools && \
mkdir -p /var/cache/schema_cache && \
chown -R www-data:www-data /var/cache/schema_cache
COPY ./httpd.conf /etc/apache2/apache2.conf
COPY ./hed2tools /var/www/hed2tools/
COPY ./hed2tools/hedweb /var/www/hed2tools/hed/hedweb/
ENTRYPOINT /usr/sbin/apache2 -D FOREGROUND -f /etc/apache2/apache2.conf
ENV HEDTOOLS_CONFIG_CLASS=config.ProductionConfig
