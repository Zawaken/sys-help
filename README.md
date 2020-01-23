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
