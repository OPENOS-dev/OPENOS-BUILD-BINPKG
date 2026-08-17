# OPENOS BUILD BINPKG

OPENOS 各组件子模块的构建产物（binpkg）共享仓库。

## 机制
- 每个组件子模块的 GitHub Actions 在源码变更时自动构建，产出 `<组件>-<架构>.pkg.tar.zst`
- 构建结果推送到本仓库 `bins/<组件>/<架构>/`，并更新 `index.json`
- 主系统（OPENOS 主仓库）构建镜像时直接从本仓库拉取最新 binpkg，**不重复构建**

## 目录结构
```
bins/
  <组件>/<架构>/<组件>-<架构>.pkg.tar.zst
index.json      # 最新产物索引（组件/架构 -> 下载 URL + sha256）
```

## 自动发布
- 各子模块 CI 使用仓库 secret `OPENOS_BINPKG_TOKEN`（PAT，需 `repo` 权限）推送产物到本仓库
- 文件名含 `-DEV2026.1-` 版本与 commit sha，保证可追溯

## 许可证
OPENOS-PROJECT-LICENSE (OPL) v1.2，全文见 [LICENSE](LICENSE)。
