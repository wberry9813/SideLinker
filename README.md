# 🚀 SideLinker (Advanced) - The Ultimate Sidecar Solution for Headless Mac mini

**English** | [简体中文](./README.zh-CN.md)

> **Designed for Headless Mac mini / Mac Studio Users.**
> "The Sidecar Bridge": Based on the `SidecarCore` private framework, featuring automatic wired/wireless reconnection, blind device detection, and native system notifications.

---

## 🌟 Key Features

* **🔌 Exclusive "Blind Connect" Mode**: Auto-detects and connects to the wired iPad without needing a device name.
* **🔄 Smart Retry Mechanism**: Built-in 10-loop retry logic to handle slow system service boot-up.
* **⚖️ Dual-Mode Switching**: Prioritizes **Wired Connection (`-wired`)** for zero latency, falling back to wireless automatically.
* **🚀 Permission Fix**: Wrapped in an Automator App to bypass SSH `Operation not permitted` errors.

---

## 🖥️ Step 1: Prerequisite - Configure Virtual Display (BetterDisplay)

> **⚠️ CRITICAL: This step MUST be completed while connected to a [Physical Monitor].**
> Otherwise, the GPU might not output correctly after unplugging HDMI, causing Sidecar to crash.

We use **BetterDisplay** to create a virtual "Primary Display".

1.  **Download**: [BetterDisplay Release](https://github.com/waydabber/BetterDisplay/releases).
2.  **Create Virtual Screen**: Choose `Create New Virtual Screen` from the menu.
3.  **Key Settings**:
    * Enable **"Start at login"**.
    * Set virtual screen to **"Connect on startup"** and as **"Main Display"**.
    * Enable **HiDPI** for Retina-grade clarity.

---

## 🛠️ Step 2: Installation

Pre-compiled binary is available.

1.  **Download**: Get `SidecarLauncher` from the Releases page.
2.  **Manual Compile**:
    ```bash
    swiftc main.swift -o SidecarLauncher
    ```

---

## 📦 Step 3: Wrap as an App (The Permission Fix)

1.  Open **Automator** -> New **Application**.
2.  Add **Run Shell Script**:
    ```bash
    /your/path/to/SidecarLauncher connect
    ```
3.  Save as `ConnectiPadWired.app` in `/Applications`.
4.  Ensure the App has **Bluetooth** and **Local Network** permissions in `System Settings`.

---

## 📱 Step 4: iPad Shortcuts Setup

Create a Shortcut on your iPad:
* **Action**: Run Script Over SSH
* **Script**: `open -a ConnectiPadWired`

---

## 🔌 Advanced: Direct Connection

Connect your iPad directly to the Mac via USB and run the shortcut. With **Blind Connect** enabled, the script identifies the USB link and ignites the screen instantly.