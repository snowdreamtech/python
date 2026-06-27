# Base Image (Alpine Variant)
# Extends snowdreamtech/alpine with additional tooling and configuration.

FROM snowdreamtech/alpine:3.24.0

# Build-time Configuration
ARG BUILDTIME \
    VERSION \
    REVISION \
    KEEPALIVE=0 \
    CAP_NET_BIND_SERVICE=0 \
    LANG=C.UTF-8 \
    UMASK=022 \
    DEBUG=false \
    PASSWORDLESS_SUDO=false \
    PGID=0 \
    PUID=0 \
    USER=root \
    WORKDIR=/root \
    PYTHON_VERSION=3.12.12-r0

# Standard OCI Metadata (https://github.com/opencontainers/image-spec)
LABEL org.opencontainers.image.authors="Snowdream Tech" \
    org.opencontainers.image.title="Python Image Based On Alpine" \
    org.opencontainers.image.description="Docker Images for Python on Alpine. (i386, amd64, arm32v6, arm32v7, arm64, ppc64le, riscv64, s390x)" \
    org.opencontainers.image.documentation="https://hub.docker.com/r/snowdreamtech/python" \
    org.opencontainers.image.base.name="snowdreamtech/alpine:3.24.0" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.source="https://github.com/snowdreamtech/python" \
    org.opencontainers.image.vendor="Snowdream Tech" \
    # x-release-please-start-version
    org.opencontainers.image.version="${VERSION:-3.12.12}" \
    # x-release-please-end
    org.opencontainers.image.created="${BUILDTIME}" \
    org.opencontainers.image.revision="${REVISION}" \
    org.opencontainers.image.url="https://github.com/snowdreamtech/python"

# Runtime Environment Configuration
ENV KEEPALIVE=${KEEPALIVE} \
    CAP_NET_BIND_SERVICE=${CAP_NET_BIND_SERVICE} \
    LANG=${LANG} \
    UMASK=${UMASK} \
    DEBUG=${DEBUG} \
    PASSWORDLESS_SUDO=${PASSWORDLESS_SUDO} \
    PGID=${PGID} \
    PUID=${PUID} \
    USER=${USER} \
    WORKDIR=${WORKDIR}

ENV PYTHONUNBUFFERED=1 \
    PYTHON_VERSION=${PYTHON_VERSION}

RUN apk update \
    && apk add --no-cache \
    python3=${PYTHON_VERSION} \
    py3-pip \
    py3-setuptools \
    py3-wheel \
    py3-virtualenv

# Container Orchestration Files
COPY entrypoint.d /usr/local/bin/entrypoint.d

RUN chmod +x /usr/local/bin/entrypoint.d/*

# Standard Healthcheck (Verification of core system responsiveness)
HEALTHCHECK NONE

# Process Execution
USER root
WORKDIR /root
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["/bin/sh"]
