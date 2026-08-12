# Xiaomi SM8450 Devicetrees — marble/ukee 裁剪版

基于 LineageOS `android_kernel_xiaomi_sm8450-devicetrees`（lineage-22.2）的 fork，为 Miku UI TDA（Android 15, marble/POCO F5, SM7475/ukee）裁剪。

## 平台声明

- **平台**: Android 15（trunk_staging / Baklava, userdebug）
- **适配分支**: `miku-a15`（本仓库主分支，原 `miku-marble` 改名）
- **版本标记**: tag `a15`（2026-08-12 打标）
- **基线**: LineageOS 22.2 + Miku UI Vampire v3（A15 线）
- **A16 迁移**: 下一轮切 Android 16 时本分支冻结，新平台另建 `miku-a16` 分支

## 分支

- `miku-a15` — 裁剪分支（本仓库主分支）
- `lineage-22.2` — LineageOS 官方跟踪

## 裁剪内容（相对上游）

`arch/arm64/boot/dts/vendor/qcom/Makefile` 大幅裁剪 dtbo/dtb 编译列表：

| 平台块 | 处理 | 原因 |
|--------|------|------|
| CAPE | 只留 ukee-* + marble | merge_dtbs.py ufdt 验证失败（无关平台 dtb 自身 dts bug） |
| waipio + diwali | 整块注释 | dtbo 29MB 超 25MB 分区（avbtool hash_footer 失败） |

裁剪后 dtbo ≈ 2MB（17 条目），`TARGET_MERGE_DTBS_WILDCARD := ukee*` 配对（BoardConfig.mk）。

> 注意：`arch/arm64/boot/dts/vendor` 是指向本仓库的 symlink——内核 dts 改动必须提交在这里。

## 使用

```shell
git remote add miku https://github.com/linuxredmipower-arch/android_kernel_xiaomi_sm8450-devicetrees.git
# repo sync 后默认是 LineageOS 官方，需 fetch 本 fork 分支：
git fetch miku miku-a15 && git checkout miku-a15
```
