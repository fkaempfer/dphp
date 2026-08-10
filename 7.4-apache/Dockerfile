FROM almalinux:10

RUN dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-10.noarch.rpm \
  https://rpms.remirepo.net/enterprise/remi-release-10.rpm && \
  dnf module reset php -y && \
  dnf module enable php:remi-7.4 -y && \
  dnf install -y httpd php php-mysqlnd php-gd php-mbstring php-xml && \
  dnf clean all


COPY 10-php.conf /etc/httpd/conf.modules.d/10-php.conf

RUN rm /etc/httpd/conf.modules.d/00-mpm.conf 

RUN sed -i 's/Listen 80/Listen 8080/' /etc/httpd/conf/httpd.conf \
    sed -i -E 's/^([[:space:]]*)(CustomLog|ErrorLog)[[:space:]]+"?logs\//\1# \2 logs\//g' /etc/httpd/conf/httpd.conf

COPY 99-httpd-docker.conf /etc/httpd/conf.d/99-httd-docker.conf

COPY 99-php-docker.ini /etc/php/conf.d/99-php-docker.ini

RUN groupadd -g 10001 php && \
  useradd -u 10001 -g php -s /sbin/nologin php && \
  mkdir -p /app /var/lib/php/session && \
  chown -R php:php /app /etc/httpd /run/httpd /var/log/httpd /var/lib/php/session


USER 10001
EXPOSE 8080

CMD ["httpd", "-D", "FOREGROUND"]