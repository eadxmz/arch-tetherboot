# Custom iPXE Arch Linux Netboot (USB Tethering Edition)

A fully automated, GitHub Actions-driven build pipeline that compiles custom **iPXE** binaries with native USB host controller drivers (`xHCI`/`EHCI`) and USB Ethernet class drivers (`CDC-ECM` / `CDC-NCM`). 

This setup enables netbooting the official Arch Linux installer over **Android/iOS USB Tethering** or supported USB-to-Ethernet adapters without needing a motherboard LAN port or native Wi-Fi drivers.

---

## Features

- **USB Tethering Ready**: Compiles the `ecm--ncm` driver profile to communicate with smartphones and USB network cards directly.
- **Dual Boot Architecture**: Builds both **UEFI** (`x86_64.efi`) and **Legacy BIOS** (`.iso` / `.usb`) boot targets.
- **Embedded Script**: Embeds a zero-configuration iPXE script that initializes USB hardware, negotiates DHCP, and chainloads Arch's HTTPS endpoint.
- **MediCat / Ventoy Native**: Easily drop the output ISO or EFI files straight onto multi-boot drives without altering partition tables.
- **Automated Releases**: Generates ready-to-flash binaries via GitHub Actions on demand.

---

## Repository Structure

```text
.
├── .github/
│   └── workflows/
│       └── build.yml       # GitHub Actions automated compiler & release engine
├── boot.ipxe               # Embedded boot script executed by iPXE
└── README.md
