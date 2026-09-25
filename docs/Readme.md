# ArkDeploy Toolkit Documentation

Welcome to the ArkDeploy Toolkit documentation. This directory contains detailed guides and walkthroughs for building, configuring, and deploying Windows using the toolkit.

---

## Guides & Walkthroughs

- **[Creating a Bootable ArkDeploy Toolkit USB](ArkDeploy_Bootable_USB_Guide.md)**  
  Step-by-step walkthrough covering ADK requirements, configuration (`config.json`), running `Build-WinPE.ps1`, and formatting single or dual-partition USB drives with `Write-BootableUSB.ps1`.

---

## Deployment & Image Formats

ArkDeploy Toolkit supports multiple image deployment formats:

- **WIM / ESD:** Modular file-based deployment with automated UEFI GPT partitioning and `bcdboot` configuration.
- **SWM (Split WIM):** Multi-part split image deployment for FAT32 USB media, overcoming the 4 GB file size limit.
- **FFU (Full Flash Update):** High-speed, bit-for-bit physical disk capture and sector-level deployment.

---

## Related Repositories & Resources

- **[Main Toolkit Repository & Releases](https://github.com/ArkDeployDev/ArkDeployToolkit)**
- **[Security Policy & Best Practices](../SECURITY.md)**
- **[ArkDeploy PXE Server](https://github.com/ArkDeployDev/ArkDeployPXE/)** — Network boot companion for PXE/TFTP booting ArkDeploy WinPE media over the local network.
- **[Official Website](https://arkdeploy.com)** — Articles, custom imaging advice, and documentation.
