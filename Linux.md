## LSBLK
lsblk is a Linux command that shows all storage devices and their partitions in the system.

*  `lsblk -o NAME,TRAN,TYPE,SIZE,FSTYPE,MOUNTPOINTS,MODEL`

    This command helps to view the following details of a storage device:
    
    NAME – Device in OS (e.g., sda, sdb, nvme0n1)

    TRAN – Transport type showing how the device is connected (USB, SATA, NVMe, etc.)

    TYPE – Indicates whether the entry is a disk or partition.

    SIZE – Total size of the device or partition

    FSTYPE – Filesystem type (ext4, vfat, ntfs, etc.)

    MOUNTPOINTS – Location where the device is mounted in the filesystem

    MODEL – Hardware model or product name of the device
    

  * `lsblk -o NAME,TRAN,TYPE,SIZE,FSTYPE,MOUNTPOINTS,MODEL /dev/<disk>`

    This shows details only the detail of particula disk

## MOUNT

mount connects a storage device to a directory in the filesystem.

  *  `mount <disk_name> <mount_point>`





