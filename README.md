# ChronoFrame 懒猫微服包

自托管照片库：时间线浏览、地点标注、相册与存储管理。

- 上游：<https://github.com/HoshinoSuzumi/chronoframe>
- 镜像：`ghcr.io/hoshinosuzumi/chronoframe`（Docker Hub 亦有同源镜像）
- 许可：AGPL-3.0（全文见 content/licenses/LICENSE）

## 组成

单容器，监听 3000 端口；数据库、设置、会话密钥与照片都在同一个数据目录里。

## 关键配置说明

- **管理员用环境变量预置**（`CFRAME_ADMIN_EMAIL` / `CFRAME_ADMIN_PASSWORD`），
  因此无需再走浏览器里的 setup wizard。
- **`NUXT_STORAGE_PROVIDER=local`**：上游 `.env.example` 默认值是 `s3`，
  若不覆盖会把照片往 S3 送（而我们没有 S3）→ 必须显式设为 `local`，
  并把 `NUXT_PROVIDER_LOCAL_PATH` 指向挂载目录下的 `./data/storage`。
- 挂载 `/app/data` 一处即可：上游 README 明确该目录包含数据库、设置、会话密钥与本地照片。
- 镜像保留在 ghcr（`source` 写完整注册表路径，避免静默回退 Docker Hub）。
- 应用自带账号体系，因此开放 `public_path`，由应用自己鉴权。

## 未验证部分

未在真机上实测：登录、上传与浏览照片、标注地点、管理相册、重启后数据留存。
