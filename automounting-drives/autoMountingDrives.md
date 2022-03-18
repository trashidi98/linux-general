# So you want to auto-mount a drive?

## Why would I want to do that?

It helps to automount drives when you have multiple drives attached to a single computer, often Linux will not automatically pick these drives up, and you won't be able to navigate to them via terminal when you boot up. 

The lazy fix is to just click on the drive via your file browser and the drive will be mounted. 

But why use Linux/UNIX based systems if you're not gonna use the terminal??!!

## First bit of advice 

Good luck

## Second bit of advice

The file we will primarily work with is called the /etc/fstab folder, and it allows the system to recognize the different mountable partitions...and other stuff I don't know (Enlighten me with a pull request pls?)

## How to 

We need to edit the /etc/fstab file which looks something like...

```
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sdb5 during installation
UUID=514f6c73-3bd0-4827-9e7f-8dfd9b380e07 /               ext4    errors=remount-ro 0       1
# /boot/efi was on /dev/sdb2 during installation
UUID=G0A2-7668  /boot/efi       vfat    umask=0077      0       1
/swapfile                                 none            swap    sw              0       0
```

We need to add a new entry which follows the general format 

```
UUID=<uuid-of-your-drive>  <mount-point>  <file-system-type>  <mount-option>  <dump>  <pass>
```

We can find UUID via 

``` 
sudo blkid 
```

If you're mounting a ntfs file system it might be just convenient and easy to use this format 

```
UUID=<yourUUID>  /mnt/<nameofyourMountPoint>  ntfs  defaults  0  2
```

Please don't include the < > in the ntfs example above


That's about it!

**Works Cited** 

https://www.linuxbabe.com/desktop-linux/how-to-automount-file-systems-on-linux




