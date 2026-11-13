# NetEase Cloud Music API add-on

本 add-on 封装 [NeteaseCloudMusicApiEnhanced](https://github.com/NeteaseCloudMusicApiEnhanced/api-enhanced)
的官方多架构 Docker 镜像，供 Music Assistant 使用。

- 上游 release：**4.41.1**（已锁定）
- 容器端口：`3000`
- 主机端口：默认 `3000`
- 无持久化数据：匿名 token 和密钥存放在 `/tmp`，启动时自动重建

## 为什么只做薄封装

上游已经提供干净的 Node.js Docker 镜像。本仓库只补充 Home Assistant add-on 元数据，
不 fork 上游业务代码，减少后续维护成本。升级时只需改两处：

1. `config.yaml`：`version`
2. `Dockerfile`：`ARG UPSTREAM_IMAGE`

## 安装

1. 在 Home Assistant 添加本仓库：
   **设置 → 加载项 → 加载项商店 → ⋮ → 仓库**
   填写：

   ```text
   https://github.com/Square-N/netease-api-addon
   ```

2. 安装 **NetEase Cloud Music API**。
3. 启动后验证：

   ```bash
   curl http://<HA_HOST>:3000/inner/version
   ```

   预期返回：`{"code":200,"data":{"version":"4.41.1"}}`

## Music Assistant

在 Music Assistant 中，把网易云 provider 的 **API base URL** 设为：

```text
http://<HA_HOST>:3000
```

如果测试时临时映射到 `3001`，则先填 `3001`，验证后再切回 `3000`。

## 端口冲突

旧版 `NetEase Cloud Music API` add-on 默认占用 `3000`。可以：

- 先停止旧 add-on，再启动本 add-on；或
- 在 add-on 的 **网络** 标签里把本 add-on 临时映射到 `3001`，验证通过后切回 `3000`。

## 更新策略

本仓库锁定上游 **release tag**，不使用 `latest`。升级时只改：

- `config.yaml` 的 `version`
- `Dockerfile` 的 `ARG UPSTREAM_IMAGE`

然后 commit + push。不配置自动更新，升级由人工确认。

## 已知提示

启动日志中可能出现上游的非致命警告：

- `xeapi public key is missing`
- `zstd` 解压相关错误

目前不影响基础接口和播放；如果后续高级接口异常，再排查。

## Vibe Coding 说明

> **本 add-on 是 Vibe Coding 产物。**
>
> 封装、配置与文档由 AI 生成并经人工确认；所用模型为 **ds4.1flash（max 档）**。
>
> 已在真实 HAOS 环境完成安装、接口检查和试播验证；生产使用前建议自行复核。
