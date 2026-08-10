 · · · Tweaker Kernel · · · 
Made for Pixel 8 Pro (shusky)
It should work on both the Pixel 8 (shiba) and Pixel 8 Pro (husky) but I've only tested on the 8 Pro.

This kernel integrates NetHunter & KernelSU next with native support for wireless packet
injection drivers, USB Arsenal and ConfigFS into the official Google AOSP kernel sources via Bazel.


## Key Features

- **Automated Cloud Compilation:** Syncs official Google `android-gs-shusky-6.1-android16` source code and 
- **builds the kernel in isolated runner environments using Bazel (`build_shusky.sh`).
- **Inline KernelSU Next (`CONFIG_KSU=y`):** Core root hooks are compiled directly into the C kernel binary,
- **keeping the `init_boot` ramdisk 100% factory stock for stealth and stability.
- **Wireless Injection (mac80211):** Patched `mac80211` subsystem allowing frame injection and 
- **monitor mode on external USB Wi-Fi adapters.
- **USB Arsenal & ConfigFS:** Native support for USB HID Gadget attacks (DuckHunter),
- **Mass Storage emulation, ECM, and ACM serial interfaces.
- **Out-of-Tree Driver Modules:** Pre-compiles and packages kernel modules for Atheros (`ath9k_htc`), 
- **Realtek (`rtl8187`), and Bluetooth USB dongles (`btusb`).
- **Filesystem & Network Optimizations:** BBR TCP congestion control, WireGuard VPN support, 
- **TTL/HL override capabilities, and NTFS3/exFAT filesystem support.


 · · · Disclaimer · · · 
 
 Use at your own risk. Flashing custom kernels carries inherent risks of bootloops or soft-bricks if not done properly. 
 This kernel was built for and tested on CP1A.260505.505, which is the May security patch on Android 16. 
 DO NOT DOWNGRADE YOUR DEVICE IF YOU FLASH THIS BUILD. It can cause the hard brick that I'm sure you've read about in
 other threads on XDA. 

 · · · Flashing Instructions · · · 


## Flashing Instructions

### Prerequisites
* Unlocked bootloader.
* Pixel 8 Pro running Android 16.
* KernelFlasher



Shout out to [ShorterKing](https://github.com/ShorterKing) for his Android optimized drivers.

work in progress

zZZzzZzZZzZzzz.....
