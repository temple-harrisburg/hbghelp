---
tags:
  - hardware
  - hdmi
  - internal
  - gefen
public: true
---
The Gefen EXT-UHD6000A-44 is a 4x4 HDMI matrix.

## Troubleshooting with the Web GUI

### Prerequisites

1. [Gefen Syner-G](https://www.gefen.com/gefen-syner-g-software/) installed on a client computer
2. A stand-alone router to connect the client computer and Gefen

### Access the web GUI

1. Open the Gefen Syner-G application on the client computer.
2. Connect client computer and Gefen device to router.
3. The Gefen device should appear as "EXT-UHD6000A-44" in the "Discover and Configure IP" section of Gefen Syner-G
4. Select the EXT-UHD6000A-44.
5. Set the device's IP Mode to "Static"
6. Set the device's Gateway IP to the IPv4 address of the router.
7. Set the Gefen device IP address to a legal address within the range of the router's subnet. For example, if the router's IP is 192.168.0.1, with a subnet mask of 255.255.255.0, a legal address would be 192.168.0.72. **The IP must not be the same as the IP address of the client computer on the router's LAN.**
8. Click "Save" in Gefen Syner-G to save changes
9. Reboot the Gefen device for the changes to take effect.
10. Once the Gefen device reboots and is detected in Gefen Syner-G, you should be able to access the web GUI through a browser at the Gefen device's IP
11. The password for the Operator account is 'Operator'; for Administrator, 'Admin'.