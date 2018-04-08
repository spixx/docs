    version   :   1.0.0
    status    :   production
    system    :   CentOS 7.x

# Base #

## Information ##
Base install aims to be a complete, secure and slimlined Operating System
that uses a well-known Linux distribution as the foundation. CentOS 6.X
fullfills all the demands and is also widely used due to those facts, but
to further develop the concept some changes has been made. To support newer
and a more wide range of packages CentOS 7.X is also used with the same
parameters as the above.

## Preamble ##
### Hardware ###
To be able to handle restrictive hardware allocations the guide is based upon
hardware with the following specifications:

    CPU: 1 core
    RAM: 1024MB
    HDD: 10GiB

What you add later is then dependent on the role of the server but this will
be enough for most roles (DNS/DHCP/FTP/HTTP).

To be able to fit within this narrow margin but still be able to handle a
wildcard physical machine follow these rules:

 * At least 2 harddrives
 * Use RAID to create 2 logical volumes
 * Always use RAID (fake-raid/software if you lack a RAID card)

So if the above is true we will create a logical RAID volume with 10GiB of
storage space and let the other logical volume be the second drive where all
data storage will take place.

### Partitions ###
The parition scheme is based upon security guides provided by the community
and to secure against local filesystem vurnerabilities. Each physical disk
is split into two partitions one for the /boot partition and the second for
the full disk with LVM. All partitions are ext4.

VG0 sda

    /               - 1GB  - Root partition
    /tmp            - 1GB  - Temporary files
    /usr            - 4GB  - Binary and library
    /var            - 2GB  - System variable files
    /var/log        - 1GB  - Logfiles
    /var/log/audit  - 512M - Audit logfile
    /boot           - 512M - Boot files
    /home           - 1GB  - Home with user files
    swap            - 1GB  - Swap file

VG1 sdb (example)

    /var/lib/mysql  - 1TB  - Database files
    /srv/nfs/share1 - 1TB  - NFS share

VG2 sdc (example)

    /srv/nfs/share2 - 1TB  - Another NFS share

When the role of the server then demands extra storage (database/web) a second
harddrive is added. Instead of cluttering the system with partitioned drives
there will be two drives (sda and sdb). Where sdb will not contain any MBR/GPT
tables but instead it will be a physical volume.

One thought here is that if this is for instance a NFS server where we know
that data volumes will be above 2TiB it is sugested that you splice the data
over more then one extra harddrive. This is both true for virtual and physical
enviornments since moving a harddrive of +2TiB is really time consuming.

There is no magical one-fits-all solutions, if you are going to be using 200TiB
NFS server then you might need to think a bit extra ;).

### Filesystem ###
Usually there is a good reason to use for instance /opt, in the documentation
here we always use /usr/local. This will contain anything local and unique to
the server. Above all else try and keep to normal shares otherwise, adding
complexity will not make normal system tasks easy on the administrators. Also
always keep to the thing you decide upon.

### Applications ###

## Installation ##
First of all we need to download a ISO file. I usually go for a favorite:
[hh](http://mirror.hh.se) but you should choose a mirror that is closer to you.
