# 🚀 SideLinker (Advanced) - 无头 Mac mini 的 iPad 随航终极方案

[English](./README.md) | **简体中文**

> **专为 Headless Mac mini / Mac Studio 用户打造。**
> 「挎斗之桥」：基于 `SidecarCore` 私有框架，实现 iPad 有线/无线自动重连、盲连（自动识别）及系统原生通知反馈。

---

## 🌟 为什么选择这个版本？

相较于传统的 AppleScript 脚本或早期 Sidecar 启动器，本项目针对 **M4 Mac mini** 等无头主机进行了深度优化：

* **🔌 独家“盲连模式”**：无需在脚本中指定 iPad 名称，程序会自动扫描并强制连接插线设备。
* **🔄 智能重试机制**：内置 10 次重试逻辑，解决开机时系统服务加载慢的问题。
* **⚖️ 双模自动切换**：优先通过 **有线直连 (`-wired`)** 以确保 0 延时，失败后自动转为无线。
* **🚀 权限地狱终结者**：通过 Automator App 封装，完美避开 SSH 远程调用时的 `Operation not permitted` 报错。

---

## 🖥️ 第一步：前置准备 - 配置虚拟屏幕 (BetterDisplay)

> **⚠️ 极重要：此步骤必须在连接【物理显示器】的情况下完成。**
> 否则 Mac 拔掉 HDMI 后 GPU 可能会停止输出，导致 Sidecar 闪退。

我们需要使用 **BetterDisplay** 创建一个虚拟主显示器。

1.  **下载**：[BetterDisplay 官方 Release](https://github.com/waydabber/BetterDisplay/releases)。
2.  **创建虚拟屏**：在菜单中选择 `Create New Virtual Screen`。
3.  **核心配置**：
    * 勾选 **"Start at login"**。
    * 设置该虚拟屏为 **"Connect on startup"** 并作为 **"Main Display"**。
    * 开启 **HiDPI** 以获得细腻画质。

---

## 🛠️ 第二步：安装脚本

本项目提供编译好的二进制文件。

1.  **下载**：从 Release 页面下载 `SidecarLauncher`。
2.  **手动编译**：
    ```bash
    swiftc main.swift -o SidecarLauncher
    ```

---

## 📦 第三步：封装为 App (核心权限修复)

1.  打开 **自动操作 (Automator)** -> 新建 **应用程序 (Application)**。
2.  添加 **运行 Shell 脚本**：
    ```bash
    /你的路径/SidecarLauncher connect
    ```
3.  保存为 `ConnectiPadWired.app` 并放入 `/Applications`。
4.  在 `系统设置 -> 隐私与安全性` 中授予该 App **蓝牙** 和 **本地网络** 权限。

---

## 📱 第四步：iPad 快捷指令配置

在 iPad 上创建快捷指令：
* **操作**：通过 SSH 运行脚本
* **脚本**：`open -a ConnectiPadWired`

---

## 🔌 进阶玩法：无网直连

只需一根 USB 线连接 iPad 与 Mac，在 iPad 上运行快捷指令。由于开启了“盲连模式”，脚本会自动识别 USB 链路并瞬间点亮屏幕。