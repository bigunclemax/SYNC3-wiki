
# USB subsystem
### usblauncher

```shell
/fs/mp/etc/usblauncher/
├── iap2ea.lua
├── iap2.lua
├── iap2ncm.lua
├── netstart.sh
├── netstop.sh
├── override.lua
├── rules.lua
├── rules_otg.lua
├── startncm-molex.sh
├── startncm.sh
├── stopncm.sh
└── umass.lua
```

Useful commands:  
`usb -vvv -N /dev/otg/io-usb-otg`

## USB-LAN ethernet
List of supported NICs in `/fs/mp/etc/usblauncher/rules_otg.lua`

```lua
nic_devices = {
    device(0x0b95, 0x7720); -- CISCO linksys USB300M ethernet dongle
    device(0x0b95, 0x772b); -- Insignia NS-PU98505 ethernet dongle
    device(0x2001, 0x3c05); -- D-Link DUB-E100 (revB1) ethernet dongle
    device(0x2001, 0x1a02); -- D-Link DUB-E100 (revC1) ethernet dongle
}

foreach (nic_devices) {
    start"/fs/mp/etc/usblauncher/netstart.sh busnum=$(busno),devnum=$(devno),path=$(USB_PATH),ign_remove /fs/mp/lib/dll/devnp-asix.so";
    removal"/fs/mp/etc/usblauncher/netstop.sh";
}
```

Content of `/fs/mp/etc/usblauncher/netstart.sh`:

```shell
#!/bin/sh

IFACE=ax0
IPADDR=192.168.1.26
mount -T io-pkt -o $1 $2
ifconfig $IFACE $IPADDR netmask 255.255.255.0
echo "debug $IFACE done."
```

ℹ️ To get a working usb network on "production" OS, copy `devnp-asix.so` from reformat package to `/fs/mp/lib/dll/devnp-asix.so`

---

```shell
1. pidin ar | grep usblauncher_otg
2. usblauncher_otg -S1 -c /fs/mp/etc/usblauncher/rules_otg.lua -M /fs/mp/etc/mcd.mnt -s /fs/mp/lib/dll/pubs/ -n/dev/otg/io-usb-otg -vvvv -b -eErtl

/fs/mp/etc/usblauncher/netstart.sh busnum=0x01,devnum=0x2,path=/dev/otg/io-usb-otg,ign_remove /fs/mp/lib/dll/devnp-asix.so
```

## USB-HID
Run USB HID server:
```shell
io-hid -d devh-usb.so
```
ℹ️ You should get `devh-usb.so` lib from QNX SDP.

`io-hid` usage:
```shell
# use io-hid
io-hid - HID Server  ( Human Interface Device )

Usage:
io-hid [options] &

Options:
  -d dll [opts]     Device DLL to load and options to pass to the DLL.
  -n name           Set server name. default "/dev/io-hid/io-hid"
  -v                Be verbose
  -V                Display server version

Examples:

    USB HID devices, PS/2 mouse, Serial mouse on COM1 directly, PS/2 keyboard

      io-hid -dusb  -dps2ser ps2mouse:mousedev:msoft:uart,1:kbd:kbddev &

```

ℹ️ After launch `io-hid` all HID events will be grabbed by libscreen.

Use [`hidview`](https://openqnx.com/static/neutrino/utilities/h/hidview.html) tool for get info about connected HID devices.