ARG UPSTREAM_IMAGE=moefurina/ncm-api:4.41.1
FROM ${UPSTREAM_IMAGE}

ARG BUILD_ARCH=amd64
ARG BUILD_VERSION=4.41.1

LABEL io.hass.type="addon" \
      io.hass.version="${BUILD_VERSION}" \
      io.hass.arch="${BUILD_ARCH}"

# 上游镜像已经具备：
# - 以非 root 的 `node` 用户运行
# - 监听 PORT（默认 3000）
# - 用 tini 作为 PID 1，命令为 `node app.js`
#
# 这里刻意保持薄封装。config.yaml 的 version 与 UPSTREAM_IMAGE 的 tag 必须同步。
