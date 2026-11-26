[![Build Pixel 8 Pro (shusky) - NetHunter + KernelSU-Next (v1.36)](https://github.com/stoag/shusky-nethunter-builder/actions/workflows/build-kernel.yml/badge.svg)](https://github.com/stoag/shusky-nethunter-builder/actions/workflows/build-kernel.yml)

# Tweaker Kernel (`v1.36`) — Pixel 8 Pro (`shusky`)

Custom GKI kernel for the **Google Pixel 8 Pro (`husky` / `shusky`)** on **Android 16**, built directly from official Google AOSP kernel sources (`android-gs-shusky-6.1-android16`) using Bazel/Kleaf.

> **Device Note:** Built and verified on the **Pixel 8 Pro (`husky`)**. Because both devices share the `shusky` Tensor G3 platform tree, it should also be compatible with the **Pixel 8 (`shiba`)**, though it has only been tested on the 8 Pro.

---

## Key Features

- **Automated Cloud Compilation:** Syncs official Google `android-gs-shusky-6.1-android16` kernel sources and builds the full kernel and matching DLKM partitions via Bazel (`build_shusky.sh`).
- **Inline KernelSU-Next (`CONFIG_KSU=y`):** Root hooks are compiled directly into the kernel binary (`Image.lz4`), leaving `init_boot` untouched.
- **Monitor Mode & Packet Injection (`mac80211` / `cfg80211`):** Verified external USB Wi-Fi monitor mode and frame injection support.
- **Dual Out-of-Tree & Modular Wi-Fi Drivers:**
  - **Realtek `RTL8812AU` (`8812au.ko`):** Built with GKI File I/O macro bypasses (`stoag/8812au-20210820`) for adapters such as the Alfa AWUS036ACH.
  - **MediaTek `MT76` / `MT7612U` (`mt76x2u.ko` & stack):** Built with verified KMI symbol CRCs and automatic `/dev/twk_firmware` SELinux staging (`vendor_fw_file`) + USB interface reprobing on boot.
- **Additional Hardware & Dongle Modules:** Includes support for USB Bluetooth (`btusb`, `btintel`, `btrtl`), USB Serial (`cdc-acm`, `ch341`, `cp210x`, `ftdi_sio`), USB Gigabit Ethernet (`ax88179_178a`, `r8152`), and SocketCAN (`can`, `can-raw`, `slcan`, `gs_usb`).
- **USB Arsenal & ConfigFS:** Native USB Gadget support for HID attacks (DuckHunter), Mass Storage, ECM, ACM, RNDIS, and NCM.
- **Network, Filesystem & Container Enhancements:** WireGuard, BBR TCP congestion control, `iptables`/`ip6tables` TTL & Hop Limit mangling, NTFS3 / ISO9660 / UDF / SquashFS support, and PID/User/UTS/IPC namespaces.
- **Non-Shadowing AnyKernel3 + KernelSU Module Packaging:** Automatically bundles `Image.lz4`, firmware blobs, `.ko` modules, and boot-time loader scripts into a single AnyKernel3 flashable ZIP alongside matched `vendor_kernel_boot`, `vendor_dlkm`, and `system_dlkm` images.

---

## Disclaimer

**Use at your own risk.** Flashing custom kernels and partition images can cause bootloops or soft-bricks if flashed out of order or on an incompatible OS build.

- **Tested On:** Android 16 (`CP1A.260505.005` / May security patch).
- **DO NOT DOWNGRADE YOUR DEVICE:** Updating past an Android anti-rollback boundary (such as moving to Android 17) and attempting to downgrade back to Android 16 can trigger hardware anti-rollback protection and hard-brick the device.
- Always download the matching Google factory image for your current build and know how to restore stock `boot`, `vendor_kernel_boot`, `vendor_dlkm`, and `system_dlkm` images before flashing.

---

## Flashing Instructions (Kernel Flasher)

### Prerequisites
- Unlocked bootloader
- Pixel 8 Pro (`husky`) running Android 16
- Root access with **Kernel Flasher** installed (and **KernelSU-Next Manager** for module management)
- https://github.com/capntrips/KernelFlasher/releases/download/v1.0.0-alpha20/KernelFlasher-v1.0.0-alpha20.apk

### Installation
1. Download the `twk-v1.36-release-package` archive from Releases and extract it to a folder on your phone's internal storage. You will have four files:
   - `twk-v1.36-system_dlkm.img`
   - `twk-v1.36-vendor_dlkm.img`
   - `twk-v1.36-vendor_kernel_boot.img`
   - `twk-v1.36-anykernel3.zip`
2. Open **Kernel Flasher**.
3. Flash the three matched partition images **first** (do **not** reboot between steps):
   - Flash `twk-v1.36-system_dlkm.img` → **`system_dlkm`** partition
   - Flash `twk-v1.36-vendor_dlkm.img` → **`vendor_dlkm`** partition
   - Flash `twk-v1.36-vendor_kernel_boot.img` → **`vendor_kernel_boot`** partition
4. Go back in Kernel Flasher, tap **Flash AK3**, and select **`twk-v1.36-anykernel3.zip`** (this flashes `Image.lz4` to `boot` and installs the `/data/adb/modules/twk_nethunter_adapters` boot loader).
5. Once all four steps complete successfully, **reboot** your device.

---

## Changelog

- **`v1.36`:** Verified working monitor mode and packet injection on Android 16; added automated SELinux-labeled firmware staging (`/dev/twk_firmware`), ordered module loading, and `MT7612U` USB reprobing on boot.
- **`v1.07`:** Initial working Realtek `rtl8812au` integration for the Alfa AWUS036ACH USB wireless adapter.
