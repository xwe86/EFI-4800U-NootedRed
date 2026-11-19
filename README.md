# NootedRed EFI — AMD Ryzen 7 4800U (Renoir)

OpenCore EFI for AMD Ryzen 7 4800U laptops, using the NootedRed hard-decode fork.

## Status

Experimental. Verify before daily driving.

- macOS 14.8.9 (23J631) / Darwin 23.6.0
- NootedRed `org.ChefKiss.NootedRed` 0.9.0 (fork build)
- Lilu 1.7.2
- `-NRedVideoFix` (VCN hardware decode) and `-NRedDisplayFix` enabled

## Hardware this was built for

| Item | Value |
|---|---|
| CPU | AMD Ryzen 7 4800U with Radeon Graphics (Renoir) |
| iGPU | AMD Radeon, PCI ID `0x1636`, rev `0x00c1` |
| SMBIOS | MacBookPro16,3 |
| Memory | 16 GB |

## What is included

- `OC/` — OpenCore folder (ACPI, Drivers, Kexts, Tools, config.plist, OpenCore.efi)
- Serial number, MLB, SystemUUID and ROM have been **cleared** from config.plist.

## Before you boot — REQUIRED

1. **Generate your own identifiers.** In `OC/config.plist` → `PlatformInfo` → `Generic`, fill in `SystemSerialNumber`, `MLB`, `SystemUUID` and `ROM` with valid values for your machine (e.g. via ProperTree / OCAT / GenSMBIOS). Booting with empty or someone else's serial will break iMessage/App Store and may cause problems.
2. **Adjust kexts and ACPI for your hardware.** USB mapping, keyboard/trackpad (VoodooI2C / VoodooPS2), audio layout and Bluetooth kexts in this EFI match one specific 4800U laptop. Remove or replace anything that does not apply to yours.
3. **Set SIP.** Boot args intentionally do not force a SIP value. Use the `ToggleSipEntry` tool or set `csr-active-config` yourself according to the NootedRed fork requirements.
4. Back up your own EFI before replacing anything.

## Known issues

See the tracking issues in `xwe86/NootedRed-dev`. Graphics stability under heavy layer/compositing workloads is still being debugged on this hardware.

## Credits

- OpenCore / Lilu by Acidanthera
- NootedRed by ChefKiss and contributors
