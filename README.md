# NootedRed EFI — Lenovo Xiaoxin Pro 13 2020 (AMD Ryzen Edition)

OpenCore EFI for the Lenovo Xiaoxin Pro 13 2020 Ryzen edition (联想小新 Pro 13 2020 锐龙版), AMD Ryzen 7 4800U, with the NootedRed hardware-decode fork.

## Status

Working: hardware video decode and GPU acceleration are both functioning.

- macOS 14.8.9 (23J631) / Darwin 23.6.0
- NootedRed `org.ChefKiss.NootedRed` 0.9.0 (fork build)
- Lilu 1.7.2
- `-NRedVideoFix` (VCN hardware decode) and `-NRedDisplayFix` enabled
- Hardware decode (H.264 / HEVC / VP9 via VCN 2.2) working; GPU acceleration working

## Target hardware

| Item | Value |
|---|---|
| Laptop | Lenovo Xiaoxin Pro 13 2020 Ryzen edition (联想小新 Pro 13 2020 锐龙版) |
| CPU | AMD Ryzen 7 4800U with Radeon Graphics (Renoir) |
| iGPU | AMD Radeon, PCI ID `0x1636`, rev `0x00c1` |
| Memory | 16 GB |
| SMBIOS | MacBookPro16,3 (spoofed) |

## What is included

- `OC/` — OpenCore folder (ACPI, Drivers, Kexts, Tools, config.plist, OpenCore.efi)
- Serial number, MLB, SystemUUID and ROM have been **cleared** from config.plist.

## Before you boot — REQUIRED

1. **Generate your own identifiers.** In `OC/config.plist` → `PlatformInfo` → `Generic`, fill in `SystemSerialNumber`, `MLB`, `SystemUUID` and `ROM` with valid values for your machine (e.g. via ProperTree / OCAT / GenSMBIOS). Booting with empty or someone else's serial will break iMessage/App Store and may cause problems.
2. **Adjust kexts and ACPI for your hardware.** USB mapping, keyboard/trackpad (VoodooI2C / VoodooPS2), audio layout and Bluetooth kexts in this EFI match one specific laptop. Remove or replace anything that does not apply to yours.
3. **Set SIP.** Boot args intentionally do not force a SIP value. Use the `ToggleSipEntry` tool or set `csr-active-config` yourself according to the NootedRed fork requirements.
4. Back up your own EFI before replacing anything.

## Credits

- OpenCore / Lilu by Acidanthera
- NootedRed by ChefKiss and contributors
