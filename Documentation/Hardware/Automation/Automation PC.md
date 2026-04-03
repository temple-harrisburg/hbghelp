---
tags:
  - hardware
  - automation
  - internal
public: false
---
The automation PC runs Debian with a minimal GUI. Chromium is launched automatically to open the Kramer Controller 

# 0. Create Custom Debian Image
Files for the custom installer used for Temple Harrisburg's automation controllers and digital signage are available at [`temple-harrisburg/custom-debian`](https://github.com/temple-harrisburg/custom-debian) on GitHub. Follow direction there to create a custom Debian image.

See [[Create a custom Debian image]] for more general instruction on pre-seeding a Debian installation.

Skip to [[#1. Installation|step 1]] if you already have an image
# 1. Installation
1. Burn custom Debian ISO to usb (if one does not already exist)
2. Insert into target machine
3. Boot using target machine BIOS's temporary boot device menu
Refer to [[General OS Installation Troubleshooting]] for troubleshooting

# 2. Details

## Stack
- Debian 13
- Xorg (display server)
- LightDM (display manager)
- Openbox (window manager)
- Chromium
## Scripts
These scripts are involved in the setup and execution of the automation controller GUI
- `~/setup.sh`
- `~/start_interface.sh`
- `~/.kramer_config`
- `~/.config/openbox/environment`
- `~/.config/openbox/autostart`
- `~/.config/openbox/rc.xml`

### `~/setup.sh`
Symlinked to `/usr/bin/setup`

An interactive script to set the host computer's static IP and the URL of the Kramer Controller web interface. Runs on first startup.


### `~/start_interface.sh`
Symlinked to `/usr/bin/start_interface`

A script to load the variables in `~/.kramer_config` and start Chromium in kiosk mode

### `~/.kramer_config`

>[!warning]
> Syntax errors in this file will cause [[#After logging in, the screen goes straight back to the login screen.|Openbox to fail to start]].

This file saves variables related to starting the Kramer GUI interface.

This file is overwritten by [[#`~/setup.sh`|~/setup.sh]]

If  `~/.kramer_config` exists, its variables are loaded by `~/.config/openbox/environment` on start. This also means that if there is a syntax error in `~/.kramer_config`, [[#After logging in, it goes straight back to the login screen.|Openbox will fail to start]].

### `~/.config/openbox/environment`

>[!warning]
> Syntax errors in this file will cause [[#After logging in, the screen goes straight back to the login screen.|Openbox to fail to start]].

Variables loaded when Openbox starts. The default location of the Kramer config file is defined here.

```sh
#!/usr/bin/env bash
export CONFIG_FILE="${CONFIG_FILE:="${HOME}/.kramer_config"}"

# Variables for automation controller
if [ -f "$CONFIG_FILE" ]; then
    . "$CONFIG_FILE" 
fi
```

### `~/.config/openbox/autostart`
Run either the interactive setup script or start the Chromium interface. 

`SKIP_SETUP` is set by [[#`~/setup.sh`|~/setup.sh]]. 

```sh
#!/usr/bin/env bash
# 
# $HOME/.config/openbox/autostart
# 
# This runs when the kiosk user logs in. If 
# the machine is configured to log in automatically,
# it executes on startup. SKIP_SETUP is unset when
# the machine first 

if [ "${SKIP_SETUP:-0}" -lt 1 ]; then 
    zutty -T "Kiosk Setup" -e "$(realpath ~/setup.sh)"
else
    start_interface
fi
```

### `~/.config/openbox/rc.xml`
Configuration for the Openbox interface. The only modifications to this file are the following keyboard shortcuts:
- `Win + E` - Launch PCManFM
- `Ctrl + Alt + T` - Start Terminal
- `Ctrl + Alt + Del` - Exit Openbox (with prompt)


# 3. Troubleshooting
## Exit GUI to terminal
If Openbox doesn't launch, you can enter a terminal session with `Ctrl + Alt + F1` from the login window.

## Opening a terminal
### ...with keyboard shortcut
If the custom Debian installer was used, the Openbox menu config at `~/.config/openbox/rc.xml` adds a custom keyboard shortcut for starting the graphical terminal emulator:
1. Press `Ctrl`+`Alt`+`T`
### ...with mouse
If the custom Openbox config files failed to copy _or_ Openbox fails to load them, the graphical terminal emulator needs to be opened from the context menu:
1. Connect a mouse and keyboard to the device
2. Use `Ctrl+Alt+Arrow Keys` to change to a different desktop
3. Right-click with the mouse on the blank desktop to open the context menu
4. Click "Terminal Emulator"


## Chrome doesn't launch on start
1. Check the permissions on `~/.config/openbox/autostart`.
2. Check for syntax errors in `~/.config/openbox/autostart`. 

## Chrome launches in the the 'New Tab' page
The `KRAMER_IP` variable is unset or set incorrectly. Check `~/.kramer_config` and `~/.config/openbox/environment`. Confirm that `~/setup.sh` sets the variable correctly.

## After logging in, the screen goes straight back to the login screen.
Check these files for syntax errors:
- `~/.kramer_config`
- `~/.config/openbox/environment`

A missing closing quotation mark (for example) can cause the X display server and Openbox to fail to start. Check the log files:
- `/var/log/Xorg.0.log`
- `~/.local/share/xorg`
