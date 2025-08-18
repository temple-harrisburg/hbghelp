---
tags:
  - internal
  - temple
  - campus
  - cashiering
  - network
  - hardware
  - software
public: false
---
TUH's operations manager requires special software for financial operations. This software can only run successfully on a workstation that has a whitelisted hostname and static IP address. Only a workstation with the whitelisted IP and hostname can install the finance software.

### Prerequisites

1. Open a ticket with network services containing the new computer's MAC address and hostname to reserve the following IPv4 address: `155.247.100.150`

### 1. Download Files

Legacy software installers are available in the [Harrisburg SharePoint](https://tuprd.sharepoint.com/:f:/r/sites/hbg/Shared%20Documents/Technology/Software/Cashiering?csf=1&web=1&e=WVpuGX).

- "TM USB 800d" Driver for Epson TM-H6000III
- POS for .NET 1.12
- Epson EPOS 1.12
- Crystal Reports Basic Runtime for VS 2008 x64
- "Cashiering Training" and "Cashiering" software

### 2. Install Software

1. Install driver software for the Epson TM-H6000III
2. Install POS for .NET 1.12
3. Install Crystal Reports Basic Runtime for VS 2008 x64
4. Install Nelnet Cashiering software

### 3. Install Epson EPOS 1.12

1. Run the Epson EPOS 1.12 Installer
2. Agree to EULA and select "User" setup method

![](/assets/images/user.png)

3. Select "USB" as the communication method.
4. Finish installation

![](/assets/images/usb12.png)

### 4. Set up Epson EPOS

1. Launch Epson SetupPOS from the start menu.
2. Click "Add"
3. Add a PosPrinter with Device Name "TM-H6000III" (III, not II).
4. Use "USB" as the Port Type
5. Accept all default settings

![](https://sites.temple.edu/hbghelp/files/2024/12/landing.png)

![](https://sites.temple.edu/hbghelp/files/2024/12/tmh6000iii.png)

6. Repeat steps 2-5, adding CheckScanner and Micr devices.

![](https://sites.temple.edu/hbghelp/files/2024/12/checkscanner.png)

![](https://sites.temple.edu/hbghelp/files/2024/12/micr.png)

7. The completed hierarchy should imitate the screenshot below:

![](https://sites.temple.edu/hbghelp/files/2024/12/result.png)

### 5. Launch Cashiering Software

1. Launch the Telnet cashiering software and have the operations manager log in.

### Troubleshooting

#### Nelnet cashiering software fails to install, network inaccessible

The IP address hasn't been reserved. The Nelnet software installer will be able to download the content needed once the static IP address is in use.

#### "Method not found: 'Microsoft.PointOfService.PosCommonOposDevice.get_PosDevice()'"

![A digital photo of a computer screen displaying an error message: "Receipt printer UniLink.OneStop.AddIns.Printers.OPOS.OPOS failed to open. Please fix the problem and then reopen the register. Details: Method not found: 'Microsoft.PointOfService.posCommonOposDevice.get_PosDevice()'."](https://sites.temple.edu/hbghelp/files/2024/12/method_not_found-1024x768.jpg)

1. Make sure the latest and correct driver are install for the model of check scanner/printer, i.e. **Epson TM-H6000III**
2. Nelnet cashiering software requires POS for .NET **1.12** and Epson EPOS 1.12. **Newer versions of .NET will not work.**
