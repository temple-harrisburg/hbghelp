---
tags:
  - network
  - internet
  - windows
  - windows11
public: true
---
### What is a DNS server?

The **Domain Name System** (DNS) is part of the infrastructure of the internet that assigns names and addresses to websites and computers. A **DNS Server** keeps a record of what names are assigned to what addresses. For example, when you type "google.com" into your web browser's URL bar and hit enter, your computer asks a DNS server to retrieve Google's **IP address**, which may be something like `142.250.64.110`.

Issues with your configured DNS server may cause certain websites or services to be unavailable. In those cases, changing your DNS may help.

### Change your DNS server

> [!warning]
> Changing your DNS server while connected to a Temple network may prevent you from accessing certain intranet services, such as printers. Use `155.247.225.230` and `155.247.225.231` as primary and alternative DNS servers when connected to a Temple network.

1. Open your Windows 10/11 Settings
2. Go to "Network & Internet"
3. Review the IP address next to "IPv4 DNS servers"

![](https://sites.temple.edu/hbghelp/files/2024/12/image-1024x796.png)

4. Next to "DNS server assignment", click "Edit"
5. Select "Manual" from the dropdown list
6. Toggle IPv4 to "On"
7. Enter the IPv4 address of an accessible DNS server. See [Public DNS servers](#public-dns-servers) below.
8. Click "Save"

![](https://sites.temple.edu/hbghelp/files/2024/12/image-2.png)

### Public DNS Servers

These are some trusted public DNS servers.

| Preferred | Alternate       | Maintained By                                                         |
| --------- | --------------- | --------------------------------------------------------------------- |
| 8.8.8.8   | 8.8.4.4         | [Google](https://developers.google.com/speed/public-dns/)             |
| 1.1.1.1   | 1.0.0.1         | [Cloudflare](https://developers.cloudflare.com/1.1.1.1/ip-addresses/) |
| 9.9.9.9   | 149.112.112.112 | [Quad9](https://www.quad9.net/)                                       |
### Private DNS Server
When connected to a Temple network (either by being on-campus or over the VPN) it's recommended to use the DNS servers:

| Preferred       | Alternate       |
| --------------- | --------------- |
| 155.247.225.230 | 155.247.255.231 |
