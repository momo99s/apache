#+++++++++++++++++++++++++++++++++++++++
# Dockerfile for webdevops/php-apache-dev:alpine-php5
#    -- automatically generated  --
#+++++++++++++++++++++++++++++++++++++++

FROM webdevops/php-apache:alpine-php5

ENV WEB_DOCUMENT_ROOT=/app \
    WEB_DOCUMENT_INDEX=index.php \
    WEB_ALIAS_DOMAIN=*.vm \
    WEB_PHP_TIMEOUT=600
ENV WEB_PHP_SOCKET=127.0.0.1:9000
ENV WEB_NO_CACHE_PATTERN="\.(css|js|gif|png|jpg|svg|json|xml)$"

COPY conf/ /opt/docker/

# Install development environment
RUN apk-install \
        # Install tools
        graphviz \
        # Tools
        nano \
        vim \
    && apk-install gcc php5-dev autoconf --virtual .pecl-deps \
    && pecl install xdebug \
    && apk del .pecl-deps \
    # Enable php development services
    && docker-service-enable syslog ssh postfix \
    && /opt/docker/bin/bootstrap.sh \
    && docker-image-cleanup
