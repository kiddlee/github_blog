---
layout: post
title: "Make Ubuntu Startup Disk"
date:   2016-02-06
description: Make Ubuntu Startup Disk
categories: Linux
tags: linux
---

* Check USB flash disk

```
diskutil list
```
And you will get information as follow:

```
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *251.0 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:          Apple_CoreStorage Macintosh HD            250.1 GB   disk0s2
   3:                 Apple_Boot Recovery HD             650.0 MB   disk0s3
/dev/disk1 (internal, virtual):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:                  Apple_HFS Macintosh HD           +249.8 GB   disk1
                                 Logical Volume on disk0s2
                                 AFC412BE-25DE-4B96-A918-783799BD0D95
                                 Unlocked Encrypted
/dev/disk2 (disk image):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     Apple_partition_scheme                        +17.4 MB    disk2
   1:        Apple_partition_map                         32.3 KB    disk2s1
   2:                  Apple_HFS Flash Player            17.4 MB    disk2s2
/dev/disk4 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *8.0 GB     disk4
   1:                 DOS_FAT_32                         8.0 GB     disk4s4
``` 

* Get the information of flash disk and unmount it.

```
diskutil unmountDisk /dev/disk4
```
Then we will get the information as follow:

```
Unmount of all volumes on disk4 was successful
```

* Write ios file in USB flash disk

```
sudo dd if=~/Downloads/ubuntu-14.04.3-desktop-amd64.iso of=/dev/disk4 bs=4m
```
Wait for a while, the Startup Disk will be created.

## Make MacOS Startup Disk

* Launch diskutil. Format USB flash disk with OSX Extended, and named the disk, like  Capitan.
* Write the image to USB flash disk with command:

```
sudo /Applications/Install\ OS\ X\ 10.11\ Developer\ Beta.app/Contents/Resources/createinstallmedia --volume /Volumes/Capitan --applicationpath /Applications/Install\ OS\ X\ 10.11\ Developer\ Beta.app --nointeraction
```

Notice: the USB flash name & OS image file maybe different.

[OS X 10.11 El Capitan U盘制作 OS X 10.11下载](http://www.pc6.com/edu/80319.html)
