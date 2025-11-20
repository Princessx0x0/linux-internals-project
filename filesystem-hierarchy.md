# Linux Filesystem Hierarchy (FHS) – My Notes
This document explains the standard Linux directory layout and what each folder in the hierarchy is used for.


### The Linux filesystem is organized as a single tree starting at /.

### 1. The Root Directory /
Everything in Linux starts here.
All files, devices, and partitions attach under /.

### 2. Important Directories (In My Words)
```bash
/bin
```
Essential user commands (ls, cp, mv, etc.)


```bash
/sbin
```
System binaries (mount, shutdown, fdisk).


```bash
/etc
```
System-wide configuration files
(e.g., ssh/sshd_config, hosts, fstab).


```bash
/home
```
User home directories
(/home/princess, /home/user1).


```bash
/root
```
Home directory for the root user.


```bash
/var
```
Variable files: logs, spools, databases.
e.g., /var/log.


```bash
/usr
```
Most user programs and libraries.
/usr/bin, /usr/lib, /usr/share.


```bash
/tmp
```
Temporary files (cleared on reboot).


```bash
/boot
```
Kernel, initrd, and GRUB configuration.


```bash
/proc
```
Virtual filesystem showing kernel and process info
(e.g., /proc/cpuinfo, /proc/meminfo).


```bash
/sys
```
Exposes devices and kernel interfaces.


```bash
/dev
```
Device files (disks, USBs, loops):
/dev/sda, /dev/loop0, /dev/null.


```bash
/mnt
```
Temporary mount points for manual mounts.


```bash
/media
```
Automatic mount points for USB drives.

### 3. Commands I Can Run in WSL
List top-level directories:
```bash
ls -l /
```

Show the Linux filesystem tree (first 2 levels):
```bash
tree -L 2 /
```

### 4. Summary
Linux has a unified filesystem tree which means that every file and directory lives under "/".
Each folder has a specific purpose defined by the FHS standard

#### Understanding this helps with navigation and administratiton of Linux systems
