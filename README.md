# GildedMod NativeLibrary

> GildedMod 的 C++ 原生组件（闭源）

---

## 这是什么

这是 [GildedMod](https://github.com/Ndkdl12qwert/GildedMod) 的 **C++ 原生部分**，
以**编译后的二进制**形式发布。源码不开源。

包含：

| 文件 | 说明 | 大小 |
|---|---|---|
| `liu_jvmti.dll` | JVMTI Agent + JNI 秒杀 | ~665 KB |
| `liu_armor_core.dll` | 护甲 DLL | ~12 KB |

---

## 下载

从 [Releases](https://github.com/Ndkdl12qwert/GildedMod-Native/releases) 下载最新版本。

---

## 安装

### 1. 把本仓库的 2 个 DLL 放入 `.minecraft/mods/`
liu_jvmti.dll
liu_armor_core.dll


### 2. 安装 MinGW-w64 UCRT64 runtime

**本 DLL 依赖以下 MinGW runtime**（**本仓库不附带**）：

| DLL | 说明 |
|---|---|
| `libgcc_s_seh-1.dll` | GCC 运行时 |
| `libstdc++-6.dll` | C++ 标准库 |

**两个 DLL 必须和 `liu_jvmti.dll` 放在同一目录（`mods/`）。**

#### 从哪获取

**方式 A：安装 MSYS2（推荐）**

1. 下载 [MSYS2](https://www.msys2.org/)
2. 安装到 `D:\msys64\`
3. 从 `D:\msys64\ucrt64\bin\` 复制：
libgcc_s_seh-1.dll
libstdc++-6.dll
4. 放进 `.minecraft/mods/`

**方式 B：安装 MinGW-w64**

1. 下载 [MinGW-w64](https://www.mingw-w64.org/downloads/)
2. 选 **UCRT64** 版本
3. 从 `bin/` 目录复制：
libgcc_s_seh-1.dll
libstdc++-6.dll


**方式 C：从其他 Mod 里找**

部分用 MinGW 编译的 Mod 也带这两个 DLL —— 可以从它们的 `mods/` 里复制。

### 3. 启动

启动游戏，看 `logs/latest.log`：

- 搜到 `[LIU-JVMTI] Agent_OnLoad` → 依赖齐全 ✅
- 报 `Can't find dependent libraries` → 缺 DLL ❌

---

## 依赖检查

**用 `objdump` 检查**：

```bash
objdump -p liu_jvmti.dll | grep "DLL Name"
```

输出：

text
DLL Name: libgcc_s_seh-1.dll      ← 必须自己提供
DLL Name: libstdc++-6.dll         ← 必须自己提供
DLL Name: KERNEL32.dll            ← 系统自带
DLL Name: api-ms-win-crt-*.dll    ← 系统自带（Windows 10+）
或者用 Dependencies —— 拖 liu_jvmti.dll 进去 —— 红色 = 缺失。

## 许可

**专有（Proprietary）** —— Copyright (C) 2026 Onicox, All Rights Reserved.

本仓库的 DLL 是**闭源二进制**，**仅授权在 GildedMod 中使用**。

### ✅ 你可以

- 在 **GildedMod Mod** 里使用这些 DLL
- 从 **GildedMod 的 Java 组件**动态链接调用
- 备份 / 保留一份本地副本

### ❌ 你不可以

- 反编译、逆向、反汇编、试图获取源码
- 修改、衍生、翻译
- 复制、分发、转售
- 去除或修改版权声明
- 用于其他项目
- 任何商业用途
- 违反 Minecraft EULA

### 📄 完整条款

[LICENSE](LICENSE) —— 完整法律文本。

---

## 免责

**仅供技术研究 / 单机使用。**

- 请勿在公开服务器使用
- 作者不对任何后果负责

详见 [LICENSE](LICENSE) 第 4、5 条。
