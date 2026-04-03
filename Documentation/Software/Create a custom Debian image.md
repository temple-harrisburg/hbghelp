---
tags:
  - linux
  - automation
public: true
---
## 0. Prerequisites
- GNU/Linux or WSL2
- `xorriso`

## 1. Obtain Debian Files
1. [Download a Debian ISO file](https://www.debian.org/distrib/)
2. Mount the ISO image and copy all contents to a working directory

## 2. Customize Distribution
### 2.0 Preseed.cfg
1. Create `preseed.cfg` at the root of the copied ISO files
2. Add settings according to [Debian documentation](https://wiki.debian.org/DebianInstaller/Preseed)
#### 2.0.1 Example `preseed.cfg`
The preseed file for our [[Automation PC]]:
```sh ln:false
# Keyboard
d-i debian-installer/language string en
d-i debian-installer/country string US
d-i keyboard-configuration/xkb-keymap select us

# Timezone
d-i time/zone string US/Eastern

# Network
d-i netcfg/choose_interface select auto
d-i netcfg/get_hostname string debian # Hostname and domain are set by kernel arguments. See '/boot/grub/grub.cfg' in installation media.
d-i netcfg/get_domain string unassigned-domain
d-i netcfg/get_hostname seen true
d-i netcfg/get_domain seen true

# Display manager
lightdm	shared/default-x-display-manager select	lightdm

# Partition Scheme
d-i partman-auto/method string regular
d-i partman-auto/choose_recipe select atomic
d-i partman-partitioning/confirm_write_new_label boolean true
d-i partman/choose_partition select finish
d-i partman/confirm boolean true
d-i partman/confirm_nooverwrite boolean true

# Grub stuff
d-i grub-installer/only_debian boolean true

# Package Manager
d-i apt-setup/use_mirror boolean true
d-i mirror/country string US
d-i mirror/http/mirror select deb.debian.org
d-i mirror/http/proxy string
d-i apt-setup/cdrom/set-first boolean false

# Don't Submit Usage Data 
popularity-contest popularity-contest/participate boolean false

# Install Packages
tasksel tasksel/first multiselect ssh
d-i pkgsel/include string git curl chromium openbox xorg lightdm pcmanfm network-manager nm-connection-editor
d-i pkgsel/upgrade select full-upgrade
d-i pkgsel/update-policy select none
d-i pkgsel/updatedb boolean true

# Setup tuhadmin
d-i passwd/root-login boolean false
d-i passwd/user-fullname string tuhadmin 
d-i passwd/username string tuhadmin
d-i passwd/user-password-crypted password $6$SinXfuGW4/cN3nGj$MWEYPanFrHFiiiY5gpxnIVVAyFP0q9n1fLGhw0LRYGoLJwIUEtQ4gATr9Dh0AbV6XZQnvbOVK0ZxcA2QWSxOq/

# Reboot
d-i finish-install/reboot_in_progress note

# Late Command
d-i preseed/late_command string /cdrom/preseed/late_command.sh automation_controller
```
### 2.1 late-command
1. Add this line to `preseed.cfg`
```sh ln:false
d-i preseed/late_comand string /cdrom/preseed_late.sh
```
2. Create `preseed_late.sh` at the root of the extracted ISO files
	use `in-target` to execute commands within the installed filesystem. See [[#2.1.1 Example `preseed_late.sh`|below]] for an example.
#### 2.1.1 Example `preseed_late.sh`
```sh
# #!/bin/sh

# Install Appspace
in-target snap install appspace-app

# Configure LightDM Display Manager Automatic login
in-target mkdir -p /etc/lightdm/
in-target /bin/bash -c 'cat << EOF > /etc/lightdm/lightdm.conf
[SeatDefaults]
autologin-user=tuhadmin
user-session=openbox
EOF'

# Configure Openbox Window Manager autostart
in-target mkdir -p /home/tuhadmin/.config/openbox/
in-target /bin/bash -c 'cat << ''EOF'' > /home/tuhadmin/.config/openbox/autostart
# Disable screensaver, screen blanking, and power management
xset s off
xset s noblank
xset -dpms

# Set portrait orientation
xrandr -o right

# Run Appspace
snap run appspace-app
EOF'

in-target chown tuhadmin /home/tuhadmin/.config/openbox/autostart
in-target chmod +x /home/tuhadmin/.config/openbox/autostart
```
### 3. Customize GRUB
#### 3.1 Menu Options
##### 3.1.1 Remove all other menu options
1. To remove all other menu options from the installer, replace the content of `boot/grub/grub.cfg` with the following:
``` ln:false
menuentry 'autoinstall' {
    linux    /install.amd/vmlinuz vga=788 --- quiet auto=true url=file:///cdrom/preseed.cfg
    initrd   /install.amd/initrd.gz
```
##### 3.1.2 Add options for multiple preseed files
``` ln:false
menuentry 'Install Automation Controller' {
    linux    /install.amd/vmlinuz vga=788 --- quiet auto=true url=file:///cdrom/preseed/preseed_automation_controller.cfg hostname=debian domain=''
    initrd   /install.amd/initrd.gz
}

menuentry 'Install Digital Signage' {
    linux    /install.amd/vmlinuz vga=788 --- quiet auto=true url=file:///cdrom/preseed/preseed_digital_signage.cfg hostname=debian domain=''
    initrd   /install.amd/initrd.gz
}

menuentry 'Manual Install' {
    linux    /install.amd/vmlinuz vga=788 --- quiet auto=true
    initrd   /install.amd/initrd.gz
}
```
#### 3.2 Custom Background


### 4. Build ISO Image
1. Run the below from the root of your ISO files directory to regenerate the `md5sum.txt` file.
```sh ln:false
find -L -type f ! -name md5sum.txt -print0 | xargs -0 md5sum > md5sum.txt
```

2. Create a bootable ISO file from your customized directory
```sh 
xorriso -as mkisofs \
  -r -J -joliet-long -l \
  -V "MY_VOLUME_LABEL" \
  -o MY_IMAGE_FILE.iso \
  -b isolinux/isolinux.bin \
  -c isolinux/boot.cat \
  -no-emul-boot -boot-load-size 4 -boot-info-table \
  -eltorito-alt-boot \
  -e boot/grub/efi.img \
  -no-emul-boot \
  CUSTOM_INSTALLER_FILES/
```


### 5. Deploy
#### 5.1 Burn to USB
I use [rufus](https://rufus.ie/en/) and check the 'Enable runtime UEFI media validation' advanced option, which validates all files against the `md5sum.txt` file before entering the bootloader. It's normal for `isolinux/isolinux.bin` and `boot.cat` to fail validation in this phase, but if other files are invalid, there may be an issue with the USB.

#### 5.2 Deploy to VM
Use Hyper-V or QEMU to spin up a virtual machine to test the automatic installation


---
# Resources
- [DebianInstaller/Preseed - Debian Wiki](https://wiki.debian.org/DebianInstaller/Preseed)
- [DebianInstaller/Preseed/EditIso - Debian Wiki](https://wiki.debian.org/DebianInstaller/Preseed/EditIso)