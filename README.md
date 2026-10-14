# Xiaomi SM8450 Devicetrees — marble/ukee 裁剪版（A17）

基于 LineageOS `android_kernel_xiaomi_sm8450-devicetrees`（`lineage-24.0`）的 fork，为 Miku UI TDA / Clover（A17, marble/POCO F5, SM7475/ukee）裁剪 dtb 编译列表。

## 平台声明

- **平台**: Android 17（`Cinderella` = android-17.0.0_r1，LineageOS 24.0 基线铺底）
- **适配分支**: `miku-a17`（当前线）、`clover-a17`（初始 = 同款裁剪）
- **基线**: LineageOS `lineage-24.0` @ `2e649a7f`（实查 `qcom/Makefile` 与 23.2 逐位一致）
- **A16 线**: `miku-a16`（已收工、刷机验证通过）；**A15 线**: `miku-a15` 已冻结

## 分支

- `miku-a17` / `clover-a17` — A17 裁剪分支
- `miku-a16` / `miku-a15` — 历史线（A15 冻结）
- `lineage-24.0` — LineageOS 官方跟踪（**只读**）

## 相对上游的适配（独立 commit，可回退）

| 内容 |
|------|
| **dtb 裁剪配方**（重放 A16 `ea25a9c`；基线逐位一致 → 等效 cherry-pick）：`qcom/Makefile` 中 WAIPIO / DIWALI 整块注释、CAPE 只留 `ukee-*` + `marble` |

> **为什么必须裁剪**（A15 线血泪）：无关平台的 dtb 自身有 dts bug，会让 `merge_dtbs.py` 的 ufdt 验证失败；且全量 dtbo 达 29MB，超过 25MB 分区（`avbtool hash_footer` 失败）。裁剪后 dtbo ≈ 2MB（17 条目），配 `TARGET_MERGE_DTBS_WILDCARD := ukee*`（BoardConfig.mk）。
>
> ⚠️ `arch/arm64/boot/dts/vendor` 是指向本仓库的 symlink——内核 dts 改动必须提交在这里。

## 使用

```shell
git remote add miku-fork https://github.com/linuxredmipower-arch/android_kernel_xiaomi_sm8450-devicetrees.git
git fetch miku-fork miku-a17 && git checkout -B miku-a17 miku-fork/miku-a17
# repo sync 后默认是 LineageOS 官方，需手动切到本分支
```
