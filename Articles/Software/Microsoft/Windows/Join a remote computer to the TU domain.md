---
tags:
  - internal
  - access
public: false
---
### Requirements

- Zoom
    - A meeting with host privileges for both participants
- Citrix Gateway Plugin
    - If not installed, should be installed from remote.temple.edu during process.

### Activate Windows Over VPN

1. Access Temple network over VPN.
2. Enter an elevated command prompt.

>[!warning] 
>Remote control users cannot interact with admin interfaces on the device they are remote-controlling. All further input needs to be done by the local user

3. The local user has to click "Yes" to allow the app to run.
4. Have the user type `slmgr /ato` in the CMD window and wait up to 30 seconds
5. A message should appear stating that Windows is activated
6. Optional: run `gpupdate /force`
    - This will update the user's profile information with the latest on file with Temple. If the user was using an old password to log in to Windows, from now on they will need to use their latest password.

### Remote Domain Join

1. Over Zoom, join [Temple VPN](https://remote.temple.edu)
2. Open PowerShell
3. Store Super User credential in an XML file[1](#05c65106-bcc7-4367-9d46-59ae6aaec0f1)

```powershell
Get-Credential | Export-CliXML -Path ~/cred.xml
```

4. Create a script to import the credential and join the domain:

```powershell
echo '$cred = Import-CliXML -Path ~/cred.xml' >> ~/join.ps1
echo 'Add-Computer -Domain tu.temple.edu -DomainCredential $cred' >> ~/join.ps1
# use single quotes to prevent the $cred variable from being interpolated
```

5. Launch an elevated PowerShell instance that executes the script:

```powershell
Start-Process powershell -Verb runas -Argumentlist "/noexit","/c","cd ~",".\join.ps1"
```

6. Delete credential after run

```powershell
Remove-Item ~/cred.xml
```