# ADDING NEW DISK TO FREEBSD


1. Add/attach the new disk to the server (install a new disk in the server or attach an external usb storage or add a virtual disk).



2. Detect the new disk 

Quick tip:
- IDE disks are /dev/ad*
- SCSI disks are /dev/da*


Login to the server and become root.

Detect the new disk with different tools
```
egrep "ad[0-9]|da[0-9]" --color /var/run/dmesg.boot
ls -la /dev | egrep "ad[0-9]|da[0-9]" --color
camcontrol devlist
gpart show
```

*In this tutorial 'ada1' will be the new disk.*



3. Create a ZFS storage pool on the new disk

Create the zpool "BIGDATA"
```
zpool create BIGDISK /dev/ada1
```

The new zpool is automatically mounted to /BIGDATA

Check the status of the zpool
```
zpool status BIGDISK
```

