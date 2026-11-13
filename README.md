# NetEase Cloud Music API — Home Assistant Add-on 仓库

这是 [NeteaseCloudMusicApiEnhanced](https://github.com/NeteaseCloudMusicApiEnhanced/api-enhanced)
的 Home Assistant 薄封装仓库，供 Music Assistant 在 HAOS 虚拟机内直接使用。

本仓库不复制、不修改上游 API 业务代码，只把上游官方多架构 Docker 镜像包成 HA add-on，
并锁定 release tag，避免 `latest` 漂移。

## 当前版本

- 上游版本：**4.41.1**
- 支持架构：`amd64` / `aarch64`
- 容器端口：`3000`
- 默认主机端口：`3000`
- 无持久化数据：匿名 token 和密钥写入 `/tmp`，重启后自动重建

## 目录结构

```text
repository.yaml
netease_cloud_music_api/
├── config.yaml
├── Dockerfile
└── README.md
```

## 安装

1. 在 Home Assistant 中添加本仓库：
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

## Music Assistant 配置

Music Assistant 的网易云 provider **API base URL** 填：

```text
http://<HA_HOST>:3000
```

如果测试时把主机端口映射到 `3001`，则暂时填 `3001`，切换回 `3000` 后再改回。

## 端口冲突

旧的 `NetEase Cloud Music API` add-on 默认也占用 `3000`。可以：

- 先停止旧 add-on，再启动本 add-on；或
- 在 add-on 的 **网络** 标签里把本 add-on 临时映射到 `3001`，验证通过后再切回 `3000`。

## 更新策略

本仓库锁定上游 **release tag**，不使用 `latest`。升级时只改两处：

- `netease_cloud_music_api/config.yaml`：`version`
- `netease_cloud_music_api/Dockerfile`：`ARG UPSTREAM_IMAGE` 的 tag

然后 commit + push，在 HA 刷新加载项商店后手动更新。

不配置自动更新，避免上游 WIP 或 breaking change 直接进入运行环境。

## 已知提示

新 add-on 启动日志中可能出现上游的非致命警告，例如：

- `xeapi public key is missing`
- `zstd` 解压相关错误

目前不影响 `/inner/version`、搜索、歌曲地址和基础播放。若后续高级接口异常，再排查这两项。

## Vibe Coding 说明

> **本仓库是 Vibe Coding 产物。**
>
> add-on 封装、配置与文档由 AI 生成并经人工确认；所用模型为 **ds4.1flash（max 档）**。
>
> 关键步骤已在真实 HAOS 环境完成安装、接口检查和试播验证，但用于生产前仍建议自行复核配置与上游版本。

## 许可证

本仓库的封装文件使用 MIT License。上游 NeteaseCloudMusicApiEnhanced 同样使用 MIT License。
