Linux Filesystem Hierarchy (FHS) – My Notes

This document explains the standard Linux directory layout
and what each folder in the hierarchy is used for.

The Linux filesystem is organized as a single tree starting at /.

1. The Root Directory /
Everything in Linux starts here.
All files, devices, and partitions attach under /.

2. Important Directories (In My Words)
/bin
Essential user commands (ls, cp, mv, etc.)

/sbin
System binaries (mount, shutdown, fdisk).

/etc
System-wide configuration files
(e.g., ssh/sshd_config, hosts, fstab).

/home
User home directories
(/home/princess, /home/user1).

/root
Home directory for the root user.

/var
Variable files: logs, spools, databases.
e.g., /var/log.

/usr
Most user programs and libraries.
/usr/bin, /usr/lib, /usr/share.

/tmp
Temporary files (cleared on reboot).

/boot
Kernel, initrd, and GRUB configuration.

/proc
Virtual filesystem showing kernel and process info
(e.g., /proc/cpuinfo, /proc/meminfo).

/sys
Exposes devices and kernel interfaces.

/dev
Device files (disks, USBs, loops):
/dev/sda, /dev/loop0, /dev/null.

/mnt
Temporary mount points for manual mounts.

/media
Automatic mount points for USB drives.

3. Commands I Can Run in WSL
List top-level directories:
ls -l /

Show the Linux filesystem tree (first 2 levels):
tree -L 2 /



4. Summary
Linux has a unified filesystem tree
Every file and directory lives under /
Each folder has a specific purpose defined by the FHS standard
Understanding this helps navigate and administer Linux systems