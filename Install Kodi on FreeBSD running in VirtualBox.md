# INSTALLING KODI MEDIA PLAYER ON FREEBSD IN VIRTUALBOX


1. Install and set up FreeBSD

Download a bootonly FreeBSD iso and install it (just do quick next-next-finish).
Let the installer create a user account ('kodi').

Reboot the server and finish the OS setup.


Install updates 
```
freebsd-update fetch install
```

Install basic packages
```
pkg install pkg 
pkg update && pkg upgrade
pkg install vim sudo bash open-vm-tools
```

Allow 'su' for the 'kodi' user
```
pw groupmod wheel -m kodi
```

Mmake bash the default shell for root and the 'kodi' user
```
pw usermod root -s /usr/local/bin/bash
pw usermod kodi -s /usr/local/bin/bash
```

Kernel tuning: add the following lines to ``/etc/rc.conf``
```
ntpd_enable="YES"
ntpd_sync_on_start="YES"
dbus_enable="YES" 
slim_enable="YES"
```



2. Set up the graphical environment


Install xorg
```
pkg install xorg
```

Add 'kodi' to the 'video' group (or to the 'wheel' group if 'video' doesn't exist)
```
pw groupmod video -m kodi || pw groupmod wheel -m kodi
```
 
Set video output mode
```
echo "kern.vty=vt" >> /boot/loader.conf
```



3. Install 'openbox' and 'slim' login manager

Add /proc to fstab
```
echo "proc /proc procfs  rw  0  0" >> /etc/fstab
```

Install openbox and slim login manager
```
pkg install openbox slim
```

To autostart 'kodi media player' at boot edit ``/usr/local/etc/slim.conf``
```
auto_login yes
default_user kodi
login_cmd           exec /bin/sh - /home/kodi/.xinitrc %session
```

Ccreate .xinitrc file for user 'kodi'
```
echo "# autostart kodi media player" > /home/kodi/.xinitrc
echo "/usr/local/bin/kodi" >> /home/kodi/.xinitrc
chown kodi:kodi /home/kodi/.xinitrc
```



4. Install Kodi Media Player

```
pkg install kodi | tee /tmp/kodi.install.log
```

Check ``/tmp/kodi.install.log`` for possible post-install tasks and information.



5. Reboot the server

```
reboot
```


