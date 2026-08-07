FROM almalinux:10

RUN dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-10.noarch.rpm \
    https://rpms.remirepo.net/enterprise/remi-release-10.rpm && \
    dnf module reset php -y && \
    dnf module enable php:remi-7.4 -y && \
    dnf install -y php-cli php-mysqlnd php-gd php-mbstring php-xml && \
    dnf clean all

RUN groupadd -g 10001 php && \
    useradd -u 10001 -g php -s /sbin/nologin php

RUN mkdir -p /app  && chown -R php:php /app

USER 10001
EXPOSE 8080

CMD ["php", "-S", "0.0.0.0:8080", "-t", "/app"]