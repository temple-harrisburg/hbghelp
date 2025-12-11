---
tags:
  - hardware
  - automation
  - internal
public: false
---
The automation PC runs Debian with a minimal GUI. Chromium is launched automatically to open the Kramer Controller 

# Settings
## Network
The device is configured with a static IP address in order to interface with the [[Documentation/Hardware/Automation/Kramer Controller|Kramer controller]]. 

### Configuration
Network configuration is located in `/etc/network/interfaces`.

```

```

### Restart network daemon
```sh
sudo systemctl restart systemd-networkd
```

# Troubleshooting
## Open a terminal
1. Connect a mouse and keyboard to the device
2. Use `Ctrl+Alt+Arrow Keys` to change to a different desktop
3. Right-click with the mouse on the blank desktop to open the context menu
4. Click "Terminal Emulator"

# Configure a Debian machine for kiosk usage
## 1. Install `lightdm`, `openbox`, and `x-org`
1. Install prerequisites[^1]
	- `openbox` is a minimal window manager
	- `x-org` is the display server
	- `lightdm` is the display manager
	- `chromium` is used to display the web page opened by the `autostart` script in step [[#2.2 `openbox`|2.2]].

```sh ln:false
sudo apt update
sudo apt install xorg openbox lightdm chromium
```
## 2. Configure
### 2.1 `lightdm`
1. Overwrite the contents of `/etc/lightdm/lightdm.confg`:
```toml 
[SeaDefaults]
autologin-user=kiosk-user
user-session=openbox
```

### 2.2 `openbox`
1. Create `~/.config/openbox/autostart.sh`. This will run when the user session starts.[^2][^3]
```sh
# Configuration
WEBSITE_URL="https://PUT_YOUR_WEBSITE_ADDRESS_HERE"
XDG_CONFIG_HOME=/tmp/.chromium
XDG_CONFIG_CACHE=/tmp/.chromium

# Disable screensaver, screen blanking, and power management
xset +dpms
xset dpms 300 1200 3600 # Standby: 5m; Suspend: 20m; Power-off: 1hr

# Auto-detect screen resolution
RESOLUTION=$(xrandr 2>/dev/null | grep '*' | awk '{print $1}')
if [ -z "$RESOLUTION" ]; then
    RESOLUTION="1920x1080"  # Default fallback can be ="1280x720"
fi
SCREEN_WIDTH=$(echo $RESOLUTION | cut -d 'x' -f1)
SCREEN_HEIGHT=$(echo $RESOLUTION | cut -d 'x' -f2)

echo "Detected screen resolution: ${SCREEN_WIDTH}x${SCREEN_HEIGHT}"

# Check internet connection using ping before launching Chromium
if ping -c 1 -W 2 google.com >/dev/null 2>&1; then
    echo "Internet connected. Proceeding with Chromium launch."
else
    echo "No internet connection detected. Exiting."
fi

# Allow quitting the X server with CTRL-ALT-Backspace
# setxkbmap -option terminate:ctrl_alt_bksp

# Prevent Chromium restore prompts
sed -i 's/"exited_cleanly":false/"exited_cleanly":true/' ~/.config/chromium/'Local State'
sed -i 's/"exit_type":"[^"]\+"/"exit_type":"Normal"/' ~/.config/chromium/Default/Preferences

# Clean up Chromium cache, cookies, and logs
find ~/.config/chromium/Default/ -type f \( -name "Cookies" -o -name "History" -o -name "*.log" -o -name "*.ldb" -o -name "*.sqlite" \) -delete
rm -rf ~/.config/chromium/Default/Logs/*

# Clear system logs
sudo journalctl --vacuum-time=1d
sudo find /var/log -type f \( -name "*.log" -o -name "*.gz" -o -name "*.1" \) -delete
sudo truncate -s 0 /var/log/syslog /var/log/dmesg

# Kill any existing Chromium instances
pkill -9 chromium 2>/dev/null
pkill -9 chrome 2>/dev/null

# Start Chromium in kiosk mode
chromium --kiosk --disable-gpu --noerrdialogs --disable-infobars --disable-features=TranslateUI \
    --disable-session-crashed-bubble --no-sandbox --disable-notifications --disable-sync-preferences \
    --disable-background-mode --disable-popup-blocking --no-first-run \
    --enable-gpu-rasterization --disable-translate --disable-logging --disable-default-apps \
    --disable-extensions --disable-crash-reporter --disable-pdf-extension --disable-new-tab-first-run \
    --disable-dev-shm-usage --start-maximized --mute-audio --disable-crashpad --hide-scrollbars \
    --ash-hide-cursor --memory-pressure-off --force-device-scale-factor=1 --window-position=0,0 \
    --window-size=${SCREEN_WIDTH},${SCREEN_HEIGHT} "$WEBSITE_URL" &

if [ $? -eq 0 ]; then
    echo "Chromium started successfully."
else
    echo "Failed to start Chromium."
    sudo reboot
fi
```

## 3. Resources
[Openbox Autostart docs](https://openbox.org/help/Autostart)
[Debian Fullscreen GUI Kiosk - Will Haley](https://www.willhaley.com/blog/debian-fullscreen-gui-kiosk/)
[How to run Chromium in kiosk mode on a Raspberry Pi 2025](https://gist.github.com/lellky/673d84260dfa26fa9b57287e0f67d09e)

---
[^1]: https://www.willhaley.com/blog/debian-fullscreen-gui-kiosk/
[^2]: [How to run Chromium in kiosk mode on a Raspberry Pi 2025](https://gist.github.com/lellky/673d84260dfa26fa9b57287e0f67d09e)
[^3]: For some reason `chromium` will crash if the following environment variables aren't set: 
- `XDG_CONFIG_HOME=/tmp/.chromium`
- `XDG_CONFIG_CACHE=/tmp/.chromium`


