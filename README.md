# garden_rotation_helper
A simple c helper for the rotation issue on garden devices.

## Requirements
Debian:
 `sudo apt install libevdev-dev gcc libgtk-3-dev`

## Setup Method 1
Add/create: 
```
<busconfig>
  <policy context="mandatory">
    <allow user="root"/>
  </policy>
</busconfig>
```
to `/etc/dbus-1/session-local.conf` and `/usr/share/dbus-1/session.conf`.

## Setup Method 2
Add ```KERNEL=="uinput", GROUP="wheel", MODE:="0664"``` to f.e. /etc/udev/rules.d/99-uinput.conf

## Compiling
- Run: `gcc rot_helper.c $(pkg-config --libs --cflags gio-2.0 gtk+-3.0 libevdev) -O3 -o rot_helper`.
- Run (Setup Method 1): `sudo DBUS_SESSION_BUS_ADDRESS="unix:path=/run/user/32011/bus" ./rot_helper /dev/input/event3`.
- Run (Setup Method 2): `./rot_helper /dev/input/event3`.
