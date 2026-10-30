# Python Image (Rocky Variant)
# Extends snowdreamtech/rocky with additional tooling and configuration.

FROM ghcr.io/snowdreamtech/rocky:10.2.0

# Build-time Configuration
# x-release-please-start-version
ARG PYTHON_VERSION=3.12.13
# x-release-please-end

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
    WORKDIR=/root

# Standard OCI Metadata (https://github.com/opencontainers/image-spec)
LABEL org.opencontainers.image.authors="Snowdream Tech" \
    org.opencontainers.image.title="Python Image Based On Rocky" \
    org.opencontainers.image.description="Docker Images for Python on Rocky. (amd64, arm64, ppc64le, s390x)" \
    org.opencontainers.image.documentation="https://hub.docker.com/r/snowdreamtech/python" \
    org.opencontainers.image.base.name="snowdreamtech/rocky:10.2.0" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.source="https://github.com/snowdreamtech/python" \
    org.opencontainers.image.vendor="Snowdream Tech" \
    org.opencontainers.image.version="${VERSION}" \
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
    WORKDIR=${WORKDIR} \
    PYTHONUNBUFFERED=1 \
    PYTHON_VERSION=${PYTHON_VERSION}

# Additional tooling and configuration for Python image
RUN set -eux \
    && dnf -y --allowerasing update \
    && dnf -y --allowerasing install \
    "python3-${PYTHON_VERSION}*" \
    python3-pip \
    python3-setuptools \
    python3-wheel \
    python3-virtualenv \
    || dnf -y --allowerasing install \
    python3 \
    python3-pip \
    python3-setuptools \
    python3-wheel \
    python3-virtualenv \
    && dnf -y --allowerasing autoremove \
    && dnf -y --allowerasing clean all \
    && rm -rf /var/cache/dnf \
    && rm -rf /tmp/* \
    && rm -rf /var/tmp/*

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
