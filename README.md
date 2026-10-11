# Custom iPXE Arch Linux Netboot (USB Tethering Edition)

A GitHub Actions build pipeline that compiles custom **iPXE** binaries with embedded USB host controllers (`xHCI`/`EHCI`) and USB networking drivers (`CDC-ECM` / `CDC-NCM`). 

This allows you to netboot the official Arch Linux installer over **Android or iOS USB Tethering**—no Ethernet jack or native Wi-Fi drivers required.

---

## 1. What Each Release File Is

When the build finishes under your repo's **Releases** tab, you get three files:

| Release File | What's Inside | What It's Used For |
| :--- | :--- | :--- |
| `ipxe-uefi-tether.zip` | Contains `EFI/BOOT/BOOTX64.EFI` | Modern UEFI boot (MediCat or standalone USB) |
| `ipxe-bios-tether.iso` | A bootable CD/ISO image | Older BIOS machines via MediCat, Ventoy, or CD |
| `ipxe-bios-tether.usb` | A raw byte-for-byte disk image | Older BIOS machines written to a dedicated USB stick |

---

## 2. Setup: Method A — MediCat USB / Ventoy (Recommended)

Since MediCat runs on Ventoy, you do not format your drive or alter partitions. You just place the files into your payload folders.

### Step 1: Download & Extract
1. Download `ipxe-uefi-tether.zip` and `ipxe-bios-tether.iso` from your GitHub **Releases** page.
2. Unzip `ipxe-uefi-tether.zip`. Inside the `EFI/BOOT/` folder, you will find `BOOTX64.EFI`.
3. Rename the files so they are easy to find in the menu:
   - Rename `BOOTX64.EFI` → `arch-netboot-tether.efi`
   - Rename `ipxe-bios-tether.iso` → `arch-netboot-tether.iso`

### Step 2: Copy to Your MediCat Drive
Plug in your MediCat flash drive and copy the two files into any payload directory (for example, inside `/Live_Operating_Systems/` or the drive root):

```text
MediCat_Drive/
└── Live_Operating_Systems/
    ├── arch-netboot-tether.efi     <-- Use this when booting UEFI
    └── arch-netboot-tether.iso     <-- Use this when booting Legacy BIOS
