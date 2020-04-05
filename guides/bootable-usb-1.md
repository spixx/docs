# Bootable USB
## Preamble
Short guide in how you can create a bootable USB from a ISO image.

Warning, the commands below are all potentially able to overwrite 
important data. Make sure you are using the correct devices when
performing the ```dd``` command.

## What device
First step is to figure out which device we can overwrite. One good
command is:

```lsblk```

This will output all block devices currently attached to the system:

```
NAME                                          MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT                                                           
sda                                             8:0    1 14.4G  0 disk                                                                       
└─sda1                                          8:1    1 14.4G  0 part                                                                       
nvme0n1                                       259:0    0  477G  0 disk                                                                       
├─nvme0n1p1                                   259:1    0  512M  0 part  /boot/efi                                                            
├─nvme0n1p2                                   259:2    0  512M  0 part  /boot                                                                
└─nvme0n1p3                                   259:3    0  476G  0 part             
```

In this example you can see my primary NVME based SSD and a USB drive. 
Commonly ```/dev/sda``` is the first drive and most likely where the OS
is installed. Please ensure that you are using the correct device!

### Download
I usually feel lazy and just utilize ```wget``` or ```curl``` but it
might be simpler to download via a browser.

### Create ISO
```dd if="~/Downloads/centos.iso" of="/dev/sda" status="progress" ; sync```
