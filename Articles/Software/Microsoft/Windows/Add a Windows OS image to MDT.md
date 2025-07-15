---
tags:
  - windows
  - windows11
  - mdt
  - temple
  - deployment
  - windows10
public: false
---
**EDIT 2025-05-29:** The deployment image is now managed by ITS at main. Adding and modifying images is no longer necessary.

---

The best way to get the latest Enterprise version of Windows is by running the Windows Media Creation Tool with certain switches to ensure it provides an Enterprise edition image.

### Get Enterprise ISO from Media Creation Tool

1. Download the Media Creation tool for your desired version of Windows: [10](https://www.microsoft.com/en-us/software-download/windows10)/[11](https://www.microsoft.com/en-us/software-download/windows11)
2. Open an elevated command prompt and navigate to the location of the executable
3. Run the executable with the options and switches specified below:

> [!warning] 
> The name of the executable will vary. Enter the name of the executable you downloaded in step 1 where `MediaCreationTool22H2.exe` is in the code block below.

```
./MediaCreationTool22H2.exe /Eula Accept /Retail /MediaArch x64 /MediaLangCode en-US /MediaEdition Enterprise
```

4. After the application finishes loading, input the [GVLK License](https://learn.microsoft.com/en-us/windows-server/get-started/kms-client-activation-keys) in the License/Product Key field.

```
NW6C2-QMPVW-D7KKK-3GKT6-VCFB2
```

5. Save the ISO to a location accessible by the deployment server, e.g. `\\server\ISOs\Windows`

### Extract install.wim from ISO

1. On the deployment server, mount the ISO created by the Media Creation Tool.
2. Open an elevated command prompt and navigate to the drive letter of the mounted ISO.
    - To check if a `.wim` file exists in the image:

```
Get-ChildItem <Mounted Drive Letter>:\ -Recurse -Filter "*.wim*"
```

4. Run DISM.exe to find the source index of the Windows 10/11 Enterprise edition in the ISO you downloaded.

```
dism /get-wiminfo /wimfile:<Mounted Drive Letter>:\sources\install.esd
```

5. Run DISM.exe to export the image
    - In this example, the Enterprise image is located at drive letter `D`, and the source index of the Enterprise edition image is `3`. You must replace those values with the results of the previous steps.

```
dism /export-image /sourceimagefile:G:\sources\install.esd /sourceindex:3 /destinationimagefile:"D:\ISOs\Windows\install.wim" /compress:max /checkintegrity
```

### Import .wim to MDT

1. In MDT, start the wizard for importing an operating system and select the `install.wim` file extracted from the Windows ISO.