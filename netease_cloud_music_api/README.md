本项目为 [NeteaseCloudMusicApiEnhanced](https://github.com/NeteaseCloudMusicApiEnhanced/api-enhanced) 的 HAOS 薄封装仓库，可作为HAOS的应用（原加载项/add-on）安装。未复制或修改上游 API 业务代码，仅作封装工作。

本仓库不复制、不修改上游 API 业务代码，只把上游官方多架构 Docker 镜像包成 HA add-on，锁定了 release tag，以便版本管理。

## 当前版本
- 上游版本：**4.41.1**
- 支持架构：`amd64` / `aarch64`
- 容器端口：`3000`
- 默认主机端口：`3000`

## 安装
1. 在 Home Assistant 中添加本仓库：在 **设置 → 应用 → 应用商店 → ⋮ → 仓库→ 添加** 填写本仓库地址；
2. 安装 **NetEase Cloud Music API**。

## 说明
本项目是 Vibe Coding 产物，所用模型为 deepseek v4.1 flash。已经过实际部署验证，但用于生产环境仍建议复核配置与上游版本。
