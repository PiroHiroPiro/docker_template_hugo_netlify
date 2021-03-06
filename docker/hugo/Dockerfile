# FROM alpine:3.11
FROM golang:1.13-alpine3.11

ENV HUGO_VERSION="0.62.2"
ENV HUGO_NAME="hugo_extended_${HUGO_VERSION}_Linux-64bit"
ENV HUGO_BASE_URL="https://github.com/gohugoio/hugo/releases/download"
ENV HUGO_URL="${HUGO_BASE_URL}/v${HUGO_VERSION}/${HUGO_NAME}.tar.gz"
ENV HUGO_CHECKSUM_URL="${HUGO_BASE_URL}/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_checksums.txt"

SHELL ["/bin/ash", "-eo", "pipefail", "-c"]
RUN cd /tmp \
    && apk add --no-cache \
    git \
    ca-certificates \
    libc6-compat \
    libstdc++ \
    && apk add --no-cache --virtual .build-deps wget \
    && wget --quiet "${HUGO_URL}" \
    && wget --quiet "${HUGO_CHECKSUM_URL}" \
    && grep "${HUGO_NAME}.tar.gz" "./hugo_${HUGO_VERSION}_checksums.txt" | sha256sum -c - \
    && tar -zxvf "${HUGO_NAME}.tar.gz" \
    && mv ./hugo /usr/bin/hugo \
    && cd / \
    && apk del .build-deps \
    && rm -rf /hugo

CMD [ "hugo", "server", "--bind=0.0.0.0", "--buildDrafts" ]
