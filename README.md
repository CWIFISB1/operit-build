# operit-build

Operit 专用构建仓库。只跑 CI 出 APK，不存源码。

## 用法

Actions → Build APK → Run workflow

| 参数 | 说明 |
|---|---|
| repo | 源码仓库，默认 `CWIFISB1/Operit` |
| ref | 分支或 commit，默认 `main` |
| build_type | `assembleDebug` / `assembleRelease` |

## 产物

`operit-apk-<build_type>`，保留 7 天。

## 必填 Secret

`GH_PAT` —— 有 repo 读权限的 Personal Access Token，用于 clone 源码。

## 为什么单开这个仓库

旧仓库 `CWIFISB1/Operit` 的 artifacts 堆到 10.3 GB（46 个 421 MB 的 APK），
导致 GitHub 托管 runner 在 Gradle 阶段报 `No space left on device`。

本仓库只保留最近 7 天的产物，构建前先释放 runner 磁盘，从根上避免该问题。