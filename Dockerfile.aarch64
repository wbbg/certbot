FROM arm64v8/python:alpine

COPY qemu-aarch64-static /usr/bin

ENTRYPOINT [ "certbot" ]
EXPOSE 80 443
VOLUME /etc/letsencrypt /var/lib/letsencrypt
WORKDIR /opt/certbot

COPY CHANGELOG.md README.rst setup.py src/
COPY acme src/acme
COPY certbot src/certbot

RUN apk add --no-cache --virtual .certbot-deps \
        libffi \
	openssl \
        ca-certificates \
        binutils
RUN apk add --no-cache --virtual .build-deps \
        gcc \
        linux-headers \
        openssl-dev \
        musl-dev \
        libffi-dev \
    && pip install --no-cache-dir \
        --editable /opt/certbot/src/acme \
        --editable /opt/certbot/src \
    && apk del .build-deps
