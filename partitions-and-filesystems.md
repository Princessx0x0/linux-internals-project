Linux Partitions & Filesystems – My Notes

This document explains what partitions and filesystems are,
how they differ, and how they work inside Linux.

1. What is a Partition? (In My Words)
A partition is a section of a physical disk.
It divides the disk into independent regions:
/dev/sda1
/dev/sda2
/dev/sdb1

Partitions help organize data and isolate system components.

Example reasons to use partitions:
Keep /home separate from /
Protect user data if the OS breaks
Prevent logs in /var from filling the entire disk
Manage multiple operating systems

2. What is a Filesystem?
A filesystem is how data is stored inside a partition.
It defines how files are organized, permissions, metadata, etc.

Common Linux filesystems:
ext4
XFS
Btrfs
FAT32 / exFAT
NTFS (Windows)

A filesystem must exist inside a partition before it can be used.

3. How They Work Together
The relationship looks like this:
[Physical Disk]  
    ↓  
[Partition]  
    ↓ (formatted with)  
[Filesystem]  
    ↓ (mounted at)  
[Directory in Linux]

Example:
/dev/sda1 → ext4 → mounted at /
/dev/sda2 → ext4 → mounted at /home
/dev/sda3 → xfs  → mounted at /var

Linux mounts partitions into its unified directory tree.


4. Commands I Can Run in WSL
Even though WSL does not use real partitions, I can still explore:

Check mounted filesystems:
df -h

List block devices (WSL will show virtual devices):
lsblk

Check mounts:
mount | head -20


5. Summary
Partitions divide physical disks
Filesystems define how data is stored
Linux mounts partitions into folders like /home, /var, /
This structure is foundational for Linux administration