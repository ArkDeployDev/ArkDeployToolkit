# 🛠️ ArkDeploy: Windows Deployment Toolkit

A streamlined solution for creating bootable USB drives that lets you deploy Windows images directly to a PC without relying on the Microsoft setup application. Built entirely in PowerShell and leveraging Windows Preinstallation Environment (Windows PE), the toolkit also supports image capture for backup and mass deployment scenarios. Windows images can be stored locally on the USB drive or accessed over a network via SMB shares.

---

## 📚 Table of Contents
- [Why Use This Toolkit?](#-why-use-this-toolkit)
- [Personal Use](#-personal-use)
- [Business\Educational Use](#-businesseducational-use)
- [Features](#-features)
- [Ideal For](#-ideal-for)
- [Requirements](#-requirements)
- [Documentation](#-documentation)

---

## 🧠 Why Use This Toolkit?

Whether you're a power user, IT admin, or educator, this toolkit simplifies the process of building a customized Windows PE boot drive. Written in PowerShell and designed to be fully moddable, it offers a clean, maintainable foundation for personalized deployments, system recovery, or mass imaging workflows.


---

## 👤 Personal Use

- Create a bootable USB with your preferred Windows version  
- Slipstream updates, drivers, and tweaks  
- Automate setup with answer files (coming soon) 
- Avoid bloat and unwanted OEM software

---

## 🏢 Business\Educational Use

- Standardize deployments across machines  
- Integrate domain join, policies, and provisioning packages  
- Save time with repeatable, documented processes  
- Reduce support overhead with clean installs

---

## ✨ Features

- Modular PowerShell scripts with verbose logging  
- Support for `.wim` and `.esd` images  
- Optional driver and update integration  
- Answer file automation  
- USB formatting and bootloader setup  
- Clean, readable code with comments and error handling

---

## 🎯 Ideal For

- IT professionals  
- System builders  
- Educators managing labs  
- Enthusiasts who love clean installs

---

<details>
  <summary>🧰 Requirements</summary>

  - Windows image file (.wim or .esd)  
  - USB drive (8GB or larger)  
  - Basic command-line knowledge  
  - PowerShell 5.1 or later  
  - Administrator privileges  
  - Windows ADK with Windows PE add-on  
  - Windows LCU (optional)  
  - Drivers (optional)  
</details>

---

## 📖 Documentation

Setup instructions, usage examples, and troubleshooting tips coming soon!  
Stay tuned or check the [docs folder](./docs) for updates.

---

## 🏷️ Badges

![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)

---
