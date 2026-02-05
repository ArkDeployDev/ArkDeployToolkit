# ArkDeploy Toolkit

![GitHub Release](https://img.shields.io/github/v/release/ArkDeployDev/ArkDeployToolkit?include_prereleases&sort=date&display_name=release)
![PowerShell](https://img.shields.io/badge/PowerShell-5.1%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)


A clean, script-driven Windows deployment framework for people who want control, not magic.

ArkDeploy Toolkit is a free, open-source Windows deployment solution built for engineers who want a transparent and repeatable way to deploy and capture Windows images without relying on Microsoft setup or heavyweight enterprise tooling.

It provides a minimal Windows PE environment that deploys Windows images directly, using readable and extensible PowerShell workflows.

---

## Why ArkDeploy Toolkit Exists

Most Windows deployment solutions fall into one of two extremes:

- Large enterprise platforms that are powerful but complex, heavy, and difficult to customise
- Ad-hoc imaging workflows that work temporarily but are hard to reproduce, audit, or maintain

ArkDeploy Toolkit is designed to sit in the middle.

It focuses on clarity, repeatability, and control. Every deployment step is visible, script-driven, and modifiable.

No setup.exe automation layers. No opaque wizards. No hidden behaviour.

---

## What the Toolkit Does

ArkDeploy Toolkit creates a bootable Windows PE deployment environment that can:

- Deploy Windows images in `.wim` or `.esd` format
- Capture running systems into clean WIM images
- Create bootable USB deployment media
- Load images from local storage or SMB network shares
- Execute modular, task-based PowerShell automation

If you understand PowerShell, you can understand and extend the toolkit.

---

## Key Capabilities

### Clean Windows Deployment

- Direct image application from Windows PE
- No Microsoft setup.exe
- No OOBE processing when used with a custom `unattend.xml` file

### Image Deployment and Capture

- Deploy custom or vendor-supplied WIM and ESD images
- Capture reference systems into reusable golden images
- Suitable for labs, rebuild workflows, and controlled environments

### USB and Network Deployment

- Automated USB creation and preparation
- SMB-based network image loading
- No dependency on complex server infrastructure

### Modular PowerShell Architecture

- Task-based PowerShell modules
- Easy to extend and customise
- Designed to be forked and adapted

---

## Who This Is For

- IT deployment administrators
- System engineers
- MSPs and system builders
- Education IT teams
- Homelab users who want full visibility into their tooling

If you care about how Windows is deployed, this toolkit is designed for you.

---

## What This Is and Is Not

**It is:**
- A transparent, script-driven deployment framework
- Lightweight and predictable
- Designed for repeatable imaging workflows

**It is not:**
- A device management platform
- A GUI-heavy enterprise suite
- A post-deployment management solution

---

## Getting Started

Documentation and setup guidance can be found in the repository.

At a high level, the workflow is:

1. Build the Windows PE environment
2. Create deployment media
3. Deploy or capture Windows images
4. Extend the workflow with custom PowerShell modules if required

---

## License

ArkDeploy Toolkit is released under the MIT License.

You are free to use, modify, and redistribute the toolkit.

---

## ArkDeploy Services

ArkDeploy Toolkit is maintained as part of ArkDeploy’s professional Windows imaging and deployment services.

If you need:
- A fully serviced custom Windows image
- A repeatable deployment workflow built for your environment
- Help integrating the toolkit into production use

You can use the toolkit independently or engage ArkDeploy services when you want to save time or reduce risk.

---

## Project Status

The toolkit is actively maintained and used in real deployment workflows.

Issues and contributions are welcome.

