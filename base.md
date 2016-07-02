    version   :   1.0.0
    status    :   production
    system    :   CentOS 7.x

# Base #

## Information ##
Base install aims to be a complete, secure and slimlined Operating System
that uses a well-known Linux distrobution as the foundation. CentOS 6.X 
fullfills all the demands and is also widely used due to those facts, but
to further develop the concept some changes has been made. To support newer
and a more wide range of packages CentOS 7.X is also used with the same
parameters as the above.

## Partitions ##
The parition scheme is based upon security guides provided by the community
and to secure against local filesystem vurnerabilities. Each physical disk
is split into two partitions one for the /boot partition and the second for
the full disk with LVM. All partitions are ext4.

    /               - 1GB - Root partition
    /tmp            - 1GB - Temporary files
    /usr            - 4GB - Binary and library
    /var            - 2GB - System variable files
    /var/log        - 1GB - Logfiles
    /var/log/audit  - 512M - Audit logfile
    /boot           - 512M - Boot files
    /home           - 1GB - Home with user files
    swap            - 1GB - Swap file

Extra partition for a database will be pushed onto a secondary volumegroup
vg1 instead of the OS volume group vg0.

## Installation ##
First of all we need to download a ISO file. I usually go for a favorite: 
[hh](http://mirror.hh.se) but you should choose a mirror that is closer to you.

### Pre installation ###

