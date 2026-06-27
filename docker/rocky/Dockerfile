# Base Image (Rocky Variant)
# Extends snowdreamtech/rocky with additional tooling and configuration.

FROM snowdreamtech/rocky:9.5

# Build-time Configuration
ARG BUILDTIME \
    VERSION \
    REVISION \
    KEEPALIVE=0 \
    CAP_NET_BIND_SERVICE=0 \
    LANG=en_US.UTF-8 \
    UMASK=022 \
    DEBUG=false \
    PASSWORDLESS_SUDO=false \
    PGID=0 \
    PUID=0 \
    USER=root \
    WORKDIR=/root \
    PYTHON_VERSION=3.12.11-3.el10

# Standard OCI Metadata (https://github.com/opencontainers/image-spec)
LABEL org.opencontainers.image.authors="Snowdream Tech" \
    org.opencontainers.image.title="Python Image Based On Rocky" \
    org.opencontainers.image.description="Docker Images for Python on Rocky. (i386, amd64, arm32v6, arm32v7, arm64, ppc64le, riscv64, s390x)" \
    org.opencontainers.image.documentation="https://hub.docker.com/r/snowdreamtech/python" \
    org.opencontainers.image.base.name="snowdreamtech/rocky:9.5" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.source="https://github.com/snowdreamtech/python" \
    org.opencontainers.image.vendor="Snowdream Tech" \
    # x-release-please-start-version
    org.opencontainers.image.version="${VERSION:-3.12.11}" \
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

RUN dnf update -y \
    && dnf install -y \
    python3=${PYTHON_VERSION} \
    python3-pip \
    python3-setuptools \
    python3-wheel \
    python3-virtualenv \
    && dnf clean all \
    && rm -rf /var/cache/dnf

# Container Orchestration Files
COPY entrypoint.d /usr/local/bin/entrypoint.d

RUN chmod +x /usr/local/bin/entrypoint.d/*

# Standard Healthcheck (Verification of core system responsiveness)
HEALTHCHECK NONE

# Process Execution
USER root
WORKDIR /root
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["/bin/bash"]
