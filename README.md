# Arch Linux fingerprint guide

Tested working with:

- DELL Latitude 5400 (0a5c:5843)

- DELL Latitude 7240 (0a5c:5843)

## install

`sudo pacman -Syu openssl-1.1 fprintd python-gobject`

From the AUR, install

- https://aur.archkinux.org/libfprint-tod-git // AUR

- https://aur.archkinux.org/libfprint-2-tod1-broadcom // AUR


Clone and run `sudo sh ./install.sh && python3 debian/update-fw.py`

- https://git.launchpad.net/libfprint-2-tod1-broadcom

## usage

Reboot your machine - drivers should now be installed and working.

The first time you run `fprintd` it may update the firmware for your sensor. This can take around 5 minutes, and the device will be unavailable during that time. Be patient!



## bugs

A known bug with `libfprint-2-tod1-broadcom` is that `fprintd-verify` is run synchronously and blocked when only one print is being searched. You MUST enroll two prints.

`fprintd-verify` hangs:

Same bug as above. Enroll two prints, and instead use `fprintd-verify -f any`

