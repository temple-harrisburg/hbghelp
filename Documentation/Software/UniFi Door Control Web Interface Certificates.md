---
public: true
---
The UniFi door system server issues a self-signed certificate. The web interface can function without having the self-signed certificate installed in the Root certificate store, but using the web interface then requires the additional step of manually proceeding to the 'unsafe' site.

## 1. Edit the hosts file
The hosts file is located at `C:\Windows\System32\drivers\etc`. The host file stores a list of IP addresses and their associated hostname. The hosts file has been largely supplanted by DHCP, but it's useful for niche scenarios and developers.
### ...with notepad
Open the hosts file in notepad and add the following line to the bottom:
```
  155.247.100.237 unifi.local                # Unifi Door System
```

### ...with Host File Editor
Microsoft's [PowerToys](https://learn.microsoft.com/en-us/windows/powertoys/install?tabs=gh%2Cextract-094) includes the Host File Editor, which provides an interface to edit the hosts file which prevents formatting errors.

1. Start Hosts File Editor with Administrator priviledges.
2. Click 'Add Entry'
3. Set the following values:
   **Address**: `155.247.100.237`
   **Hosts**: `unifi.local`
   **Comment**: `Unifi Door System`
4. Click 'Add'

![[Pasted image 20260421114726.png]]

## 2. Import UniFi Self-Signed Certificate
The following PowerShell script retrieves and saves the UniFi door access server's self-signed certificate to the host computer's root certificate storage.

```powershell
Import-Module pki

Add-Type @"
using System;
using System.Net.Http;
public class SelfSignedCert 
{
    private string _certdata;
    public string GetCert(string uri)
    {
        var handler = new HttpClientHandler();
        handler.ServerCertificateCustomValidationCallback = (msg, cert, chain, err) => { _certdata = cert?.ExportCertificatePem(); return true; };
        var client = new HttpClient(handler);
        HttpResponseMessage res = client.GetAsync(uri).GetAwaiter().GetResult();
        return _certdata;
    }
}
"@

$certFile = New-TemporaryFile;
$getcert = [SelfSignedCert]::new()
$getcert.GetCert("https://unifi.local") | Out-File $certFile

Import-Certificate -FilePath $certFile -CertStoreLocation "Cert:\LocalMachine\Root"
```

1. Run the script in an elevated PowerShell instance
2. Restart the computer

## 3. Access `https://unifi.local`
With `unifi.local` in the hosts file and the self-signed certificate installed, the web interface should now be accessible without error from [unifi.local](https://unifi.local).
