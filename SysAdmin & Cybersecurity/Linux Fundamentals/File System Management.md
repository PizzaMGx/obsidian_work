Linux is a powerful operating system that supports a wide range of file systems, including ext2, ext3, ext4, XFS, Btrfs, NTFS, and more.

The Linux file system is based on the Unix file system, which is a hierarchical structure that is composed of various components. At the top of this structure is the inode table, the basis for the entire file system. The inode table is a table of information associated with each file and directory on a Linux system. Inodes contain metadata about the file or directory, such as its permissions, size, type, owner, and so on. The inode table is like a database of information about every file and directory on a Linux system, allowing the operating system to quickly access and manage files.
## Disks & Drives
Disk management on Linux involves managing physical storage devices, including hard drives, solid-state drives, and removable storage devices. The main tool for disk management on Linux is the `fdisk`, which allows us to create, delete, and manage partitions on a drive.

```
sudo fdisk -l
```

Output: 
```
Disk /dev/vda: 160 GiB, 171798691840 bytes, 335544320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x5223435f

Device     Boot     Start       End   Sectors  Size Id Type
/dev/vda1  *         2048 158974027 158971980 75.8G 83 Linux
/dev/vda2       158974028 167766794   8792767  4.2G 82 Linux swap / Solaris

Disk /dev/vdb: 452 KiB, 462848 bytes, 904 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```

## Mounting
In order to read the external disks we need to `mount` them with the mount tool, Or we can define them in the [/etc/fstab]([fstab - ArchWiki (archlinux.org)](https://wiki.archlinux.org/title/Fstab#:~:text=The%20fstab(5)%20file%20can%20be%20used%20to%20define%20how%20disk#:~:text=The%20fstab(5)%20file%20can%20be%20used%20to%20define%20how%20disk)) file so they are mounted at boot.


When we list the devices we can find for example a USB drive in /dev/sda1, To work with it we can run the commands:
```
# To Mount
sudo mount /dev/sdb1 /mnt/usb
# To Umount
sudo umount /mnt/usb
```

It is important to note that we must have sufficient permissions to unmount a file system. We also cannot unmount a file system that is in use by a running process. To ensure that there are no running processes that are using the file system, we can use the `lsof` command to list the open files on the file system.

## SWAP
Swap space is a crucial aspect of memory management in Linux, and it plays an important role in ensuring that the system runs smoothly, even when the available physical memory is depleted. When the system runs out of physical memory, the kernel transfers inactive pages of memory to the swap space, freeing up physical memory for use by active processes. This process is known as swapping.

In addition to being used as an extension of physical memory, swap space can also be used for hibernation, which is a power management feature that allows the system to save its state to disk and then power off instead of shutting down completely. When the system is later powered on, it can restore its state from the swap space, returning to the state it was in before it was powered off.