本文件是为后续项目更新所写的维护手册，解释了锁定上游镜像版本的原因及如何修改。

## 1. 为什么锁定 release tag

1. **对应明确**：同一个程序（原加载项/add-on）版本，任何时候都对应同一个上游版本，避免出现“封装版本号没变但镜像内容变了”的情况；
2. **便于回滚**：新的上游出现问题时可方便回到上一个版本；

## 2. 修改锁定的版本

需同步修改两处代码：

- `netease_cloud_music_api/config.yaml` 的 `version`
- `netease_cloud_music_api/Dockerfile` 的 `ARG UPSTREAM_IMAGE`

## 3. 典型修改流程

1. 到上游仓库查看新的 release tag，确认是否有接口或运行环境变化；
2. 把 `config.yaml` 的 `version` 和 `Dockerfile` 的 `ARG UPSTREAM_IMAGE` 改成对应的 tag；
3. 于HA中更新/重建程序（原加载项/add-on）。
