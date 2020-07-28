# sys-help


### Antergos Keyring

#### If it doesn't let you upgrade a package because of a signature run this
`sudo pacman-key --init; sudo pacman-key --populate; sudo pacman-key --refresh-keys`

### qmk_firmware

#### If qmk keymaps won't compile on arch because of a too new version of arm-none-eabi-gcc
`pacman -U https://archive.archlinux.org/packages/a/arm-none-eabi-gcc/arm-none-eabi-gcc-8.3.0-1-x86_64.pkg.tar.xz`

#### Could also use docker if this is an issue.
`example: sudo util/docker_build.sh planck/rev6:zawaken:flash`

#### Upgrading qmk fork from upstream
```
git remote add upstream https://github.com/qmk/qmk_firmware.git
git checkout master
git fetch upstream
git pull upstream master
git push origin master
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

### Games

#### World of Warcraft

##### Streaming error occured (WOW51900322).
Download the [Windows WOW cache](https://github.com/1thumbbmcc/wowcache/blob/master/Cache.zip) ([Source](https://forums.lutris.net/t/world-of-warcraft-streaming-error/2322))
Go to the directory you've installed World of warcraft. (for me it was ~/Games/world-of-warcraft/drive_c/Program Files (x86)/World of Warcraft/_retail_)
Delete the "Cache" folder.
Unzip the Cache.zip file into the _retail_ directory.

