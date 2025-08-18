---
tags:
  - internal
  - it
---
This article goes over the basic steps for provisioning a workstation for official Temple use.

### Imaging a Device

#### Prerequisites

- The device's MAC address must be registered with the staff VLAN on [Telecom::Bridge](https://telecom.temple.edu/tcbridge/main.php)
- The device must be connected to an active port enabled with the staff VLAN.

#### Access device boot menu

1. Follow device manufacturer's instructions for launching BIOS boot menu
    - On Lenovo ThinkPads, the BIOS options can be accessed by pressing `Enter` on the splash screen or `F12` to access boot options directly.
2. Boot from PXE over IPv4.

##### Troubleshooting PXE boot

1. PXE requires Legacy (BIOS) functionality. Most device firmware is now UEFI, so if you don't see PXE booting as an option or PXE booting is failing to load the preboot environment, you have to enable Legacy (BIOS) booting in the device firmware.
2. The firmware's Safe Boot setting may prevent you from PXE booting. You will need to disable it in the firmware settings.

#### Entering WinPE (Windows preboot environment)

1. PXE booting will begin when a loading screen begins downloading `Deployment-Share-(*)` from the IP address pointing to the on-premises deployment server.

##### Troubleshooting in WinPE

- If the device repeatedly fails to connect to the preboot environment, then there may be no network drivers in the environment that support that device's network card. You will need to find and download the device's network drivers and include them in the preboot environment in MDT.
- `Shift + F10` launches cmd.exe

#### Initiating deployment

1. Launch the task sequence with the desired Operating System

### Joining the computer to the Domain

2024-08-02 : This process is subject to change while ITS transitions away from on-prem management to Microsoft Entra.

1. After Windows OS boots, search for 'workgroup' in the windows search bar; Or, from Settings, go to `System > About > Device specifications > Domain or workgroup > Computer Name > Change...`
2. Switch the "Member of" option from 'Workgroup' to 'Domain'
3. Enter 'tu.temple.edu' in the Domain field
4. Log in with your superuser credentials
5. Accept changes, but do not restart until the task sequence is complete and restarts on its own.

### Additional Setup

- If the device is intended for use by a staff member, it saves trouble down the line to add their domain account as a local admin to that device. See How to add a domain user as a local admin.

### Read More
- [[Add a Windows OS image to MDT]]
- [[Add a domain user as a local admin]]
