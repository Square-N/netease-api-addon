ARG UPSTREAM_IMAGE=moefurina/ncm-api:4.41.1
FROM ${UPSTREAM_IMAGE}

ARG BUILD_ARCH=amd64
ARG BUILD_VERSION=4.41.1

LABEL io.hass.type="addon" \
      io.hass.version="${BUILD_VERSION}" \
      io.hass.arch="${BUILD_ARCH}"

# The upstream image already:
# - runs as the non-root `node` user
# - listens on PORT (default 3000)
# - uses tini as PID 1 and `node app.js` as its command
#
# Keep this wrapper intentionally thin. The add-on version and the upstream
# image tag in config.yaml / UPSTREAM_IMAGE must stay in sync.
