ARG BUILD_FROM=ghcr.io/hassio-addons/base/aarch64:11.0.1
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

ENV BASE_PATH /app

# Copy root filesystem
COPY rootfs /
# RUN chmod +x /sms-gw/sms-gw.sh

# Setup base
RUN apk update \
    && apk add --no-cache python3 gammu-dev
RUN apk add --no-cache --virtual .build-deps py3-pip gcc musl-dev

WORKDIR $BASE_PATH
# RUN mkdir -p $BASE_PATH /ssl
RUN pip3 install python-gammu paho-mqtt
RUN rm -rf /root/.cache

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Cayetano Sanchez <ha@ha@cayetanosm.es>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Cayetano Sanchez <ha@cayetanosm.es>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
