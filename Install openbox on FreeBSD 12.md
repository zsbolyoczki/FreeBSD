# Install openbox on FreeBSD 12


1. Install FreeBSD 12

Select base components, partition disks, set up network and add users.



2. Update the new system and install packages
```
freebsd-update fetch install
pkg install pkg
pkg update && pkg upgrade

pkg install tree vim less bash sudo
pkg install xorg open-vm-tools # only necessary in case of a VM
```



3. Install and set up openbox and related packages
```
pkg install openbox slim tint2 obconf xbindkeys numlockx feh | tee /tmp/openbox.install.txt
```

Check ``/tmp/openbox.install.txt`` for instructions to finish the installation.

Create .xinitrc for all users
```
for h in $(ls -1d /home/*); do echo "openbox" >> ${h}/.xinitrc; chmod 644 ${h}/.xinitrc; done
```

Add the following to /etc/rc.conf:
```
sysrc ntpd_enable="YES"
sysrc ntpd_sync_on_start="YES"
sysrc dbus_enable="YES" 
sysrc slim_enable="YES"
```

Add /proc to fstab:
```
echo "proc /proc procfs  rw  0  0" >> /etc/fstab
```

Allow "su" for users:
```
pw groupmod wheel -m USERNAME
```


4. Reboot
```
reboot
```
