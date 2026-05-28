# syntax=docker/dockerfile:1.7

ARG BUILD_FROM=ghcr.io/usetrmnl/terminus:0.60.0@sha256:48f78aec134e67c121c703b79cc6d15f722fa3a00d1438934817a61d4daab5c1
FROM ${BUILD_FROM}

ARG BUILD_ARCH=local
ARG BUILD_VERSION=0.1.6

USER root

SHELL ["/bin/bash", "-o", "errexit", "-o", "nounset", "-o", "pipefail", "-c"]

RUN <<'STEPS'
  export DEBIAN_FRONTEND=noninteractive
  apt-get update -qq
  apt-get install --no-install-recommends -y \
    ca-certificates \
    gosu \
    jq \
    postgresql-18 \
    procps \
    valkey-server
  rm -rf /var/lib/apt/lists /var/cache/apt/archives
  rm -rf /var/lib/postgresql/18/main /var/lib/valkey
STEPS

COPY rootfs /

RUN chmod 0755 /usr/local/bin/terminus-app-run

WORKDIR /app

ENTRYPOINT ["/usr/local/bin/terminus-app-run"]

LABEL \
  org.opencontainers.image.title="Home Assistant App: TRMNL Terminus" \
  org.opencontainers.image.description="Self-hosted Terminus server for TRMNL BYOS devices." \
  org.opencontainers.image.source="https://github.com/kaffolder7/ha-app-terminus" \
  org.opencontainers.image.licenses="MIT" \
  io.hass.type="app" \
  io.hass.arch="${BUILD_ARCH}" \
  io.hass.version="${BUILD_VERSION}"
