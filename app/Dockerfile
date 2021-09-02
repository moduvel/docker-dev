# syntax=docker/dockerfile:1

FROM docker.io/ahabid/base-php-nginx-phpfpm:n1.21.1-p8.0.10-1

LABEL maintainer="Ahmedul Haque Abid <a_h_abid@hotmail.com>"

ARG HTTP_PROXY=""
ARG HTTPS_PROXY=""
ARG NO_PROXY="localhost,127.0.0.1"
ARG TIMEZONE="UTC"

# Proxy
ENV http_proxy="${HTTP_PROXY}" \
    https_proxy="${HTTPS_PROXY}" \
    no_proxy="${NO_PROXY}" \
    TZ="${TIMEZONE}"

USER root

RUN --mount=type=cache,target=/var/cache/apt \
    echo "-- Configure Timezone --" \
        && echo "${TIMEZONE}" > /etc/timezone \
        && dpkg-reconfigure -f noninteractive tzdata \
    && echo "-- Install PHP Extensions --" \
        && install-php-extensions \
            redis \
            uuid

WORKDIR /var/www/html

RUN chown -R www-data:www-data /var/www

# Unset proxy, timezone ENVs
ENV http_proxy="" \
    https_proxy="" \
    no_proxy="" \
    TZ=""
