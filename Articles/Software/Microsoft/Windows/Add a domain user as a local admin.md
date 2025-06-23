---
tags:
  - windows
  - microsoft
  - windows11
  - internal
public: false
---
This article goes over adding a domain user account as a local admin in order to elevate the domain user's privileges on a workstation. Parts of these directions are specific to the Temple University domain and will not apply to other domains.

### Local

#### GUI

1. Log in to the device as a local admin
2. Press `Win + R` to open the 'run' dialog and enter `lusmgr.msc` or search "Local users".
3. Open 'Groups'
4. Right click on 'Administrators', select 'Properties'
5. Click 'Add'
6. Enter user's accessnet or full name
7. Click 'Check names'
8. Log in with a domain account.
9. Click Ok
10. Restart

#### PowerShell

1. Launch an elevated PowerShell terminal.
2. Replace `<accessnet>` in code block below and execute.

```powershell
Add-LocalGroupMember -Group Administrators -Member "TU\<accessnet>" -Credential (Get-Credential)
```

3. Provide credentials to a domain account.
4. Restart computer.

### Remote:

This process can also be done over a remote session, i.e. over Zoom with remote control access.

1. Connect user to Temple VPN
2. Gain remote control of user's computer over zoom
3. Open `run` with Win+R
4. Replace `<accessnet>` with the user's accessnet username in the script and execute.

```sh
powershell /c "Start-Process powershell -ArgumentList 'Add-LocalGroupMember -Group Administrators -Member tu\<accessnet>' -Verb runas"
```

This one-liner starts a PowerShell instance which then spawns another PowerShell instance with elevated privileges ("`-Verb runas`") necessary to add a local admin.

5. User will be prompted to enter local admin credentials.
6. Restart computer.