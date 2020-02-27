# sys-help


### Antergos Keyring

#### If it doesn't let you upgrade a package because of a signature run this
`sudo pacman-key --init; sudo pacman-key --populate; sudo pacman-key --refresh-keys`

### qmk_firmware

#### If qmk keymaps won't compile on arch because of a too new version of arm-none-eabi-gcc
`pacman -U https://archive.archlinux.org/packages/a/arm-none-eabi-gcc/arm-none-eabi-gcc-8.3.0-1-x86_64.pkg.tar.xz`

#### Could also use docker if this is an issue. Have had to do this on Void Linux and Fedora.
`example: sudo util/docker_build.sh planck/rev6:zawaken:flash`

#### Upgrading qmk fork from upstream
```
git remote add upstream https://github.com/qmk/qmk_firmware.git
git checkout master
git fetch upstream
git pull upstream master
git push origin master
```

#### Building qmk keymaps without sudo doesn't work
##### add the udev rules listed [here](https://docs.qmk.fm/#/faq_build?id=linux-udev-rules), then run this:
```
sudo udevadm control --reload-rules
sudo udevadm trigger
```
##### For olkb keyboards I am fairly certain `/etc/udev/rules.d/50-atmel-dfu.rules` is the only file needed.
```
# Atmel ATMega32U4
SUBSYSTEMS=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2ff4", MODE:="0666"
# Atmel USBKEY AT90USB1287
SUBSYSTEMS=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2ffb", MODE:="0666"
# Atmel ATMega32U2
SUBSYSTEMS=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2ff0", MODE:="0666"
```

### Keymaps

#### Stop linux from changing keymap when you unplug and replug keyboard.
`sudo vim /etc/X11/xorg.conf.d/11-usb-keyboard.conf`

##### I don't think the name of the file matters much, the content matters much more I would think.

```
Section "InputClass"
    Identifier         "Keyboard Defaults"
    MatchIsKeyboard	   "yes"
    MatchProduct       "keyboard"
    Option  "XkbLayout"  "no"
EndSection
```
