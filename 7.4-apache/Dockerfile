FROM almalinux:10

RUN dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-10.noarch.rpm \
    https://rpms.remirepo.net/enterprise/remi-release-10.rpm && \
    dnf module reset php -y && \
    dnf module enable php:remi-7.4 -y && \
    dnf install -y httpd php php-mysqlnd php-gd php-mbstring php-xml && \
    dnf clean all

RUN sed -i 's/Listen 80/Listen 8080/' /etc/httpd/conf/httpd.conf && \
    sed -i 's#DocumentRoot "/var/www/html"#DocumentRoot "/app"#' /etc/httpd/conf/httpd.conf && \
    sed -i 's#<Directory "/var/www/html">#<Directory "/app">#' /etc/httpd/conf/httpd.conf && \
    sed -i 's/AllowOverride None/AllowOverride All/' /etc/httpd/conf/httpd.conf && \
    sed -i 's#^ErrorLog "logs/error_log"#ErrorLog "/dev/stderr"#' /etc/httpd/conf/httpd.conf
COPY 10-php.conf /etc/httpd/conf.modules.d/10-php.conf

RUN echo "log_errors = On" >> /etc/php.d/99-legacy.ini && \
    echo "error_log = /dev/stderr" >> /etc/php.d/99-legacy.ini

RUN groupadd -g 10001 php && \
    useradd -u 10001 -g php -s /sbin/nologin php && \
    mkdir -p /app && \
    chown -R php:php /app /etc/httpd /run/httpd /var/log/httpd

USER 10001
EXPOSE 8080

CMD ["httpd", "-D", "FOREGROUND"]