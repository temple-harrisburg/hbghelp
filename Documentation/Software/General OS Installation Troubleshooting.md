---
public: true
---
## Disable Secure Boot
Secure Boot is a BIOS feature which restricts what software can be loaded by the computer before the operating system boots. This can prevent customized images of Windows or Linux from installing. 

Refer to the manual for the target machine's BIOS for instructions on disabling Secure Boot

## Ensure Internet Connection is established
Even for installations of Windows or Linux from a USB, an internet connection will be needed to download updates and packages.
- If the target machine has LED indicators near the ethernet port, visually confirm they're lighting up before continuing with an installation.
- Confirm the target machine's MAC is registered with [telecom.temple.edu](https://telecom.temple.edu). 

## Clean target machine disk
When trying to install a Windows image over PXE, the state or contents of the target machine's main disk can cause installation to fail. 

In WinPE:
1. Press `F8` to launch the `cmd` prompt
2. Enter a DiskPart session with `diskpart`
3. Select the target disk for installation with `select disk #` where `#` is the number of the disk
4. Clean disk with `clean`
5. Attempt installation again