# easytier-server-web

专为无ssh权限的arm设备制作构建的ET组网镜像

## 背景

- 原作者【jaycq/easytier-server-web已删除源码】  旧版本内核断更  二开继续更新

- 本仓库只做一件小事：用官方新版本二进制**覆盖**镜像内的旧二进制，得到一个「内核已升级、结构完全一致」的新镜像。

## 使用方法

1. 打开本仓库 Actions 页面，选择 **Rebuild easytier-server-web (kernel upgrade)** 工作流。
2. 手动触发（Run workflow），填入官方版本号，例如 `v2.6.4`。
3. 等待构建完成，在 Artifacts 下载构建产物（docker save tar）。
4. 在拾光坞 Web UI 导入镜像即可。

## 手动（本机离线）流程

见 `AGENTS.md` 记忆中的流程：使用 node 脚本生成 ustar 替换层覆盖三个二进制 + 重写 OCI 元数据 + 打包 tar.gz（对应本仓库 `.github/workflows/rebuild.yml` 的离线版）。

## 校验

binary 替换后必须全层 merge + sha256 与官方发布包逐一比对，确认：

- `easytier-core`
- `easytier-web-embed`
- `easytier-cli`

三个文件 hash 与官方 `easytier-linux-aarch64-<VER>.zip` 内完全一致。
