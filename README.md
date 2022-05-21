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
##### For ATMega32u4 keyboards like the viterbi, `/etc/udev/rules.d/50-atmel-dfu.rules` is needed.
```
# Atmel ATMega32U4
SUBSYSTEMS=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2ff4", TAG+="uaccess"
# Atmel USBKEY AT90USB1287
SUBSYSTEMS=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2ffb", TAG+="uaccess"
# Atmel ATMega32U2
SUBSYSTEMS=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2ff0", TAG+="uaccess"
# Atmel ATMega328p / USBAspLoader
SUBSYSTEMS=="usb", ATTRS{idVendor}=="16c0", ATTRS{idProduct}=="05dc", TAG+="uaccess"
```

##### For olkb keyboards, `/etc/udev/rules.d/56-dfu-util.rules` is needed.
```
# stm32duino
SUBSYSTEMS=="usb", ATTRS{idVendor}=="1eaf", ATTRS{idProduct}=="0003", MODE:="0666"
# Generic stm32
SUBSYSTEMS=="usb", ATTRS{idVendor}=="0483", ATTRS{idProduct}=="df11", MODE:="0666"
```

### Keymaps

#### Stop linux from changing keymap when you unplug and replug keyboard.
`sudo vim /etc/X11/xorg.conf.d/11-usb-keyboard.conf` (non-systemd)
`sudo vim /etc/X11/xorg.conf.d/00-keyboard.conf` (systemd)

##### I don't think the name of the file matters much, the content matters much more I would think.

```
Section "InputClass"
    Identifier         "Keyboard Defaults"
    MatchIsKeyboard	   "yes"
    MatchProduct       "keyboard"
    Option  "XkbLayout"  "no"
EndSection
```

### Games

#### World of Warcraft

##### Streaming error occured (WOW51900322).
Download the [Windows WOW cache](https://github.com/1thumbbmcc/wowcache/blob/master/Cache.zip) ([Source](https://forums.lutris.net/t/world-of-warcraft-streaming-error/2322))
Go to the directory you've installed World of warcraft. (for me it was `~/Games/world-of-warcraft/drive_c/Program Files (x86)/World of Warcraft/_retail_`)
Delete the "Cache" folder.
Unzip the Cache.zip file into the `_retail_` directory.

### Homelab

#### Idrac autonegotiation
##### [Here](https://www.bvanleeuwen.nl/faq/?p=1120) is the source

`racadm getconfig -g cfgNetTuning`

If cfgNetTuningNicAutoneg is 1, then run these commands:

`racadm config -g cfgNetTuning -o cfgNetTuningNicAutoneg 0`

`racadm racreset`
