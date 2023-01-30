# Arch Linux fingerprint guide

### Tested working with:

- DELL Latitude 5400 (Broadcom 0a5c:5843)

- DELL Latitude 7430 (Broadcom 0a5c:5843)

- DELL XPS 9310 (GOODIX 27c6:533c)

### no drivers:

- DELL XPS 7390 (GOODIX 27c6:5385)

## install

`sudo pacman -Syu openssl-1.1 fprintd python-gobject`

From the AUR, install

- https://aur.archkinux.org/libfprint-tod-git

### broadcom

From the AUR, install

- https://aur.archkinux.org/libfprint-2-tod1-broadcom

Clone and run `sudo sh ./install.sh && python3 debian/update-fw.py`

- https://git.launchpad.net/libfprint-2-tod1-broadcom

### XPS 93XX (GOODIX 27c6:533c)

From the AUR, install

- https://aur.archlinux.org/libfprint-2-tod1-xps9300-bin

## usage

Reboot your machine - drivers should now be installed and working.

The first time you run `fprintd` it may update the firmware for your sensor. This can take around 5 minutes, and the device will be unavailable during that time. Be patient!

To login to a tty with your fingerprint:

`/etc/pam.d/system-local-login`

```
auth	sufficient	pam_fprintd.so
```

To verify sudo with your fingerprint:

`/etc/pam.d/sudo`

```
auth	sufficient	pam_fprintd.so
```

To unlock i3lock with your fingerprint:

`/etc/pam.d/i3lock`

```
auth	sufficient	pam_fprintd.so
```

## bugs

### `fprintd-enroll` works, but `fprintd-verify` hangs:

A known bug with `libfprint-2-tod1-broadcom` is that `fprintd-verify` is run synchronously and blocked when only one print is being searched. You MUST enroll two prints and use `fprintd-verify -f any` instead.


### i3lock doesn't unlock:

i3lock only verifies after an input is entered, i.e. press enter, then scan your fingerprint.
