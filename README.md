 · · · **Tweaker Kernel** · · · 
 **Made for Pixel 8 Pro (shusky)**
 
 It should work on both the Pixel 8 (shiba) and Pixel 8 Pro (husky) but I've only tested on the 8 Pro.
 
 This kernel integrates NetHunter & KernelSU Next with native support for wireless packet injection
 drivers, USB Arsenal and ConfigFS into the official Google AOSP kernel sources via Bazel.


 · · · Key Features · · · 

- **Automated Cloud Compilation:** Syncs official Google `android-gs-shusky-6.1-android16` source code
- and builds the kernel in isolated runner environments using Bazel (`build_shusky.sh`).
- **Inline KernelSU Next (`CONFIG_KSU=y`):** Core root hooks are compiled directly into the C kernel binary,
- keeping the `init_boot` ramdisk 100% factory stock for stealth and stability.
- **Wireless Injection (mac80211):** Patched `mac80211` subsystem allowing frame injection and
- monitor mode on external USB Wi-Fi adapters.
- **Advanced Out-of-Tree Wi-Fi Drivers:** Pre-compiles and packages kernel modules for Atheros (`ath9k_htc`),
- older Realtek (`rtl8187`), and Bluetooth USB dongles (`btusb`).
- **Modern Realtek Injection & GKI Bypass:** Features native integration of **RTL8812AU** and **RTL88x2BU**
- (RTL8822BU, RTL8812BU, RTL8822CU) drivers. Includes a custom C-source macro bypass to get around Google's
- strict GKI File I/O security blocks. 
- **USB Arsenal & ConfigFS:** Native support for USB HID Gadget attacks (DuckHunter), Mass Storage emulation,
- ECM, and ACM serial interfaces.
- **Filesystem & Network Optimizations:** BBR TCP congestion control, WireGuard VPN support, TTL/HL override
- capabilities, and NTFS3/exFAT filesystem support.
- **Clean AnyKernel3 Packaging:** Automatically packages the compiled `Image.lz4` and custom `.ko` modules
- into a flashable AK3 zip for easy installation.

 · · · Disclaimer · · · 
 
 Use at your own risk!!!
 Flashing custom kernels carries inherent risks of bootloops or soft-bricks if not done properly. 
 This kernel was built for and tested on CP1A.260505.505, which is the May security patch on Android 16.
 **DO NOT DOWNGRADE YOUR DEVICE IF YOU FLASH THIS BUILD.**
 It can trigger Android's Anti-Rollback protection and cause a hard brick as documented in various threads
 on XDA. I strongly suggest reading as many threads as is necessary to familiarize yourself with the various
 methods for restoring your device from a bootloop state and downloading the factory image for your device
 prior flashing any custom kernel. 
 
 · · · Flashing Instructions · · · 
 
 ### Prerequisites
* Unlocked bootloader.
* Pixel 8 / 8 Pro running the required Android 16 build.
* Root access (to use Kernel Flasher / FKM) or a custom recovery.

### Installation
1. Download the `Tweaker-Kernel-twk.v1.02-AK3-Boot.zip` file from the repository Releases / Actions tab.
2. Open **Kernel Flasher** (or Franco Kernel Manager).
3. Select "Flash AK3 zip" and choose the downloaded file.
4. Let the script flash the kernel and inject the NetHunter modules.
5. Reboot and enjoy!


## Credit should go to [ShorterKing](https://github.com/ShorterKing) for his Android optimized Realtek drivers!

Woot!! twk.v1.02!
Successfully added Realtek rtl8812au drivers for my AWUS036ACH usb wireless adapter. 
:D

and now... 

zZZzzZzZZzZzzz...
