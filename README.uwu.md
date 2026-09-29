# sm8450 设备树 (dtb/dtbo)（`kernel/xiaomi/sm8450-devicetrees`） — uwuAOSP 适配版

> 上游说明见同目录 `README.md`（未改动）。本文件是 **uwuAOSP（uwu-16.2）** 的适配声明。

sm8450 设备树 (dtb/dtbo)（`kernel/xiaomi/sm8450-devicetrees`），供 **uwuAOSP uwu-16.2**（Android 16）使用。

## 平台声明

- **平台**: Android 16（uwuAOSP `uwu-16.2` = `android-16.0.0_r4` + LineageOS 23.2，**user**）
- **适配分支**: `uwu-a16`（当前线，HEAD `e671c26`）
- **版本标记**: tag `uwu-a16`（2026-09-30 打标）
- **基线**: LineageOS `lineage-23.2` @ `2e649a7f`
- **与 miku 线的关系**: 同一套设备栈，两条 ROM 线（`miku-a16`（Miku UI，本仓库 default）与 `uwu-a16`（uwuAOSP）**平行**，不是接续）

## 分支

- `uwu-a16` — uwuAOSP（uwu-16.2）适配分支（**当前线**）
- `miku-a16` — Miku UI Blooming_v2 适配分支（本仓库的 **default**）
- `lineage-23.2` — LineageOS 官方跟踪（**只读基线**）

## 相对上游的适配（全部独立 commit，可回退）

| commit | 内容 |
|---|---|
| `e671c26` | **dtb 裁剪**（移植 A15 的 `fd5a327` + `8925020`）：dtbo 29MB 塞不进 25MB 分区，必须裁 |

配套改动在相邻仓库：
- 上游真 fork，基线不会自动跟走，**起分支前要先核对**是否落后上游
- 属 `lineage.dependencies` 闭包

## 验证

✅ **2026-09-30 出包 + 刷机验证通过**：`uwuAOSP_marble-bamberga-20260929.zip`
（2.7G，sha256 `3d165d053baeac38e0bf167b468a4567e49ae881d5272f104770f73ad7a55d26`）。

配方级总结见 `~/miku_docs/verified_experiences.md` **§十一**；全过程见
`~/miku_docs/archive/round12/round12_operation.md`。
