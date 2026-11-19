# NootedRed EFI — Lenovo Xiaoxin Pro 13 2020 (AMD Ryzen Edition)

OpenCore EFI for the Lenovo Xiaoxin Pro 13 2020 Ryzen edition (联想小新 Pro 13 2020 锐龙版), AMD Ryzen 7 4800U, with the NootedRed hardware-decode fork.

## Software

| Item | Value |
|---|---|
| macOS | 14.8.9 (23J631) / Darwin 23.6.0 |
| NootedRed | `org.ChefKiss.NootedRed` 0.9.0 (fork build) |
| Lilu | 1.7.2 |
| SIP | disabled |
| Boot args | `-v revpatch=cpuname,sbvmm ipc_control_port_options=0 revblock=media -vi2c-force-polling -NRedVideoFix -NRedDisplayFix` |

**Important:** the `-NRedVideoFix -NRedDisplayFix` flags are required. Hardware decode and graphics stability depend on these being present in boot-args.

## Hardware support

Verified working on the target machine:

| Component | Status | Detail |
|---|---|---|
| CPU | Working | AMD Ryzen 7 4800U (Renoir), 8 cores |
| iGPU / Metal | Working | AMD Radeon, PCI ID `0x1636`, Metal 3, 2048×1280 |
| Hardware video decode | Working | VCN 2.2 (H.264 / HEVC / VP9) via `-NRedVideoFix` |
| Display / GPU acceleration | Working | via `-NRedDisplayFix` |
| Memory | Working | 16 GB |
| Wi-Fi | Working | AirportItlwm 2.3.0, connected |
| Bluetooth | Working | IntelBluetoothFirmware 2.5.0, On |
| Audio | Working | AppleALC 1.8.8, internal speakers + mic |
| Battery | Working | SMCBatteryManager, 100%, 324 cycles |
| Camera | Working | Integrated UVC camera |
| Keyboard | Working | VoodooPS2Keyboard |
| Trackpad | Working | VoodooI2C / VoodooPS2Trackpad |
| USB | Working | — |
| NVMe | Working | AppleNVMeFamily 2.1.0 |

## SMBIOS

`MacBookPro16,3` (spoofed). You must replace the serial/MLB/UUID/ROM with your own — see below.

## Included

- `OC/` — OpenCore folder (ACPI, Drivers, Kexts, Tools, config.plist, OpenCore.efi)
- Serial number, MLB, SystemUUID and ROM have been **cleared** from config.plist.

## Before you boot — REQUIRED

1. **Generate your own identifiers.** In `OC/config.plist` → `PlatformInfo` → `Generic`, fill in `SystemSerialNumber`, `MLB`, `SystemUUID` and `ROM` (e.g. via ProperTree / OCAT / GenSMBIOS). Booting with empty or someone else's serial will break iMessage/App Store.
2. **Adjust kexts and ACPI for your hardware.** USB mapping, keyboard/trackpad, audio layout and Bluetooth kexts match one specific laptop. Remove or replace anything that does not apply to yours.
3. **Keep the two NRed boot flags** (`-NRedVideoFix -NRedDisplayFix`) — hardware decode and graphics stability depend on them.
4. **Set SIP** according to the NootedRed fork requirements, using `ToggleSipEntry` or `csr-active-config`.
5. Back up your own EFI before replacing anything.

## Known issues

Earlier builds had GPU resets / freezes triggered by layer-compositing operations (e.g. opening popovers). This was resolved in recent builds. If you still see instability, confirm the boot args above are set, and check the tracking issues in `xwe86/NootedRed-dev`.

## Credits

- OpenCore / Lilu by Acidanthera
- NootedRed by ChefKiss and contributors
