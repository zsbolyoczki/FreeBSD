# FreeBSD first steps after install



## Decrease boot delay

echo "autoboot_delay='1'" >> /boot/loader.conf 


## Upgrade the packages
```
freebsd-update fetch install

pkg install pkg
pkg update 
pkg upgrade
```


## Install basic tools
```
pkg install vim less bash sudo
```


## Modify user config
```
pw groupmod -n wheel USERNAME # to have su

pw usermod -n root -s /usr/local/bin/bash
echo "LC_ALL=en_US.UTF-8" > /root/.bashrc
echo "export EDITOR=vim" >> /root/.bashrc
echo "alias grep='grep --color'" >> /root/.bashrc
echo "alias egrep='egrep --color'" >> /root/.bashrc
echo "alias vi=vim" >> /root/.bashrc
ln -s .bashrc .bash_profile

pw usermod -n USERNAME -s /usr/local/bin/bash
echo "LC_ALL=en_US.UTF-8" >> /home/USERNAME/.bashrc
echo "export EDITOR=vim" >> /home/USERNAME/.bashrc
echo "alias grep='grep --color'" >> //home/USERNAME/.bashrc
echo "alias egrep='egrep --color'" >> //home/USERNAME/.bashrc
ln -s .bashrc .bash_profile
```

## Set UTF8 support in console
```
echo "kern.vty='vt'" >> /boot/loader.conf
```

## Set Hungarian keyboard layout in terminal
Print current config
```
kbdmap -s
```

Set up new keyboard layout
```
echo "keymap='hu.101.kbd'" >> /etc/rc.conf
```

## Graphical environment (openbox)

```
echo "dbus_enable='YES'" >> /etc/rc.conf
echo "hald_enable='YES'" >> /etc/rc.conf
echo "slim_enable='YES'" >> /etc/rc.conf

pkg install xorg openbox slim tint2 obmenu obconf lxterminal mate-terminal

su - USERNAME
mkdir -p .config/openbox
cp /usr/local/etc/xdg/openbox/menu.xml ~/.config/openbox/menu.xml
chmod 644 ~/.config/openbox/menu.xml
echo "tint2 &" > .xinitrc
echo "setxkbmap -model pc105 -layout hu -variant 102_qwerty_comma_dead &"
echo "openbox" >> .xinitrc

exit
```





```
reboot
```

