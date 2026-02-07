# Creating a Bootable ArkDeploy Toolkit USB

This walkthrough explains how to create a bootable USB drive using the
ArkDeploy Toolkit.

The USB can be used to deploy Windows images locally or from a network
share.

------------------------------------------------------------------------

## Prerequisites

### Windows ADK & Windows PE Add-on

Download and install the Windows Assessment and Deployment Kit (ADK) and
the Windows PE add-on.\
Current version: **10.1.26100.2454 (December 2024)**

-   ADK download (x64):\
    https://go.microsoft.com/fwlink/?linkid=2289980

-   Windows PE add-on:\
    https://go.microsoft.com/fwlink/?linkid=228998

### ADK Installation Notes

1.  Install the ADK first.
2.  During installation, only select **Deployment Tools**.
3.  Then install the Windows PE add-on.

------------------------------------------------------------------------

## ArkDeploy Toolkit

Download the latest release from:

https://github.com/ArkDeployDev/ArkDeployToolkit/releases

Extract the ZIP file into a working directory.

------------------------------------------------------------------------

## Configure Toolkit Settings

Before running the script, review and configure the toolkit settings.

1.  Open `settings.json` in a text editor.
2.  Review the following options:

### Key Settings Explained

**ProjectName**\
Used to name generated files.\
Can be left as default or changed if managing multiple configurations.

**Updates**\
Can usually be left as-is.\
Only required when Microsoft releases updates for Windows PE.

**Language**\
Set your required language(s).\
Reference:
https://learn.microsoft.com/windows-hardware/manufacture/desktop/available-language-packs-for-windows

**Timezone**\
Set your required timezone.\
Reference:
https://learn.microsoft.com/windows-hardware/manufacture/desktop/default-time-zones

**OptionalPEComponents**\
Can be left unchanged unless required by a custom script.\
Full list:
https://learn.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference

------------------------------------------------------------------------

## Network Deployment (Optional)

If deploying Windows images from a network share, complete the Server
settings section.

> ⚠️ **Warning:** Credentials are stored in plain text and are not
> secure.\
> Use only in trusted environments.

Save `settings.json` once complete.

You are now ready to build your deployment image.

------------------------------------------------------------------------

## Build the Deployment Image

1.  Open an elevated PowerShell window.
2.  Change directory to where you extracted the ArkDeploy Toolkit:

``` powershell
cd <ArkDeployToolkitDirectory>
```

3.  Run the script:

``` powershell
.\ArkDeployPE.ps1
```

The script will:

-   Build the Windows PE environment\
-   Apply your configured settings\
-   Create a bootable ISO file in the `BootImages` directory

------------------------------------------------------------------------

## Create the Bootable USB

After the ISO is created, the script will ask if you want to create a
USB drive.

You have two options:

-   Manually copy the ISO to a USB drive\
-   Let the toolkit create the USB automatically (**recommended**)

### Creating the USB Automatically

Press **Y** when prompted.

This launches the USB Drive Maker script.\
(You can also run this script later to convert an existing ISO.)

> ⚠️ Insert a USB drive now --- all data on the drive will be erased.

------------------------------------------------------------------------

## USB Partition Options

You will be prompted to choose how the USB drive is configured:

### Option 1 -- Single Partition

-   Small FAT32 boot partition\
-   Suitable for network-only deployments

### Option 2 -- Dual Partition (Recommended)

-   Small FAT32 boot partition\
-   Large NTFS partition for:
    -   WIM files
    -   Drivers
    -   Tools
    -   Offline deployments

For most use cases, select **Option 2** to support both USB and network
deployments.

------------------------------------------------------------------------

## Completion

The script will:

-   Partition and format the USB drive\
-   Mount the ISO\
-   Copy all required files

Once complete, you will have a fully bootable ArkDeploy Toolkit USB
ready for deployment.

------------------------------------------------------------------------

## Next Steps

-   Adding Images (.WIM or .ESD files)
-   Adding an unattended.xml
-   Network deployment walkthrough
-   Capturing images
