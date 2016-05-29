# Base
## Information
Base install aims to be a complete, secure and slimlined Operating System
that uses a well-known Linux distrobution as the foundation. CentOS 6.X 
fullfills all the demands and is also widely used due to those facts, but
to further develop the concept some changes has been made.

## Partitions
/               - 1GB - Root partition
/tmp            - 1GB - Temporary files
/usr            - 4GB - Binary and library
/var            - 2GB - System variable files
/var/log        - 1GB - Logfiles
/var/log/audit  - 512M - Audit logfile
/boot           - 512M - Boot files
swap            - 1GB - Swap file

## Applications
salt-minion
