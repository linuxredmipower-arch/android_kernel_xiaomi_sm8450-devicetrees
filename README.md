# Xiaomi SM8450 Devicetrees — marble/ukee 裁剪版

基于 LineageOS `android_kernel_xiaomi_sm8450-devicetrees`（`lineage-23.2`）的 fork，为 Miku UI TDA（Android 16, marble/POCO F5, SM7475/ukee）裁剪 dtb 编译列表。

## 平台声明

- **平台**: Android 16（Blooming_v2 = android-16.0.0_r4 + LineageOS 23.2, userdebug）
- **适配分支**: `miku-a16`（当前线）
- **版本标记**: tag `a16`（2026-09-27 打标）
- **基线**: LineageOS `lineage-23.2` @ `2e649a7`
- **A15 线**: `miku-a15` 已冻结（A15 出包验证通过）。两线**已分叉**——`miku-a16` 自上游另开，不是从 `miku-a15` 接续（领先 13 个提交 / 落后 4 个）

## 分支

- `miku-a16` — 裁剪分支（当前线）
- `miku-a15` — Android 15 裁剪分支（已冻结）
- `lineage-23.2` — LineageOS 官方跟踪

## 相对上游的适配（全部独立 commit，可回退）

| commit | 内容 |
|--------|------|
| `ea25a9c` | **dtb 裁剪配方移植**（对应 A15 `fd5a327` + `8925020`）：`arch/arm64/boot/dts/vendor/qcom/Makefile` 中 WAIPIO / DIWALI 整块注释、CAPE 只留 `ukee-*` + `marble` |

移植后与 A16 基线**有效内容等价（diff 0 行）**——A16 基线在 dtb 列表上已与 A15 裁剪后一致，本 commit 保留配方意图。

> **为什么必须裁剪**（来自 A15 线实测）：无关平台的 dtb 自身有 dts bug，会让 `merge_dtbs.py` 的 ufdt 验证失败；且全量 dtbo 达 29MB，超过 25MB 分区（`avbtool hash_footer` 失败）。裁剪后 dtbo ≈ 2MB（17 条目），配 `TARGET_MERGE_DTBS_WILDCARD := ukee*`（BoardConfig.mk）。
>
> ⚠️ `arch/arm64/boot/dts/vendor` 是指向本仓库的 symlink——内核 dts 改动必须提交在这里。

## 使用

```shell
git remote add miku16 https://github.com/linuxredmipower-arch/android_kernel_xiaomi_sm8450-devicetrees.git
git fetch miku16 miku-a16 && git checkout miku-a16
# repo sync 后默认是 LineageOS 官方，需手动切到本分支
```
