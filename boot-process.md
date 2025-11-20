# Linux Boot Process – My Notes
This document explains the Linux boot process in my own words and includes commands I ran inside WSL to explore how Linux starts services.

## 1. High-Level Boot Sequence
 - BIOS/UEFI: 
    1. Hardware checks
    2. Looks for a bootable device
 - Boot Loader (GRUB): 
    1. Loads and launches the Linux kernel into memory
 - Kernel: 
    1. Initializes drivers, memory, CPU scheduling 
    2. Mounts the initial RAM disk (initramfs)
 - init (PID 1): 
    1. The first user-space process 
    2. Starts system services (network, logging, sshd, etc.)
 - Login or GUI: 
    1. Terminal login prompt 
    2. Or a graphical desktop (if installed)

## 2. Practical Checks I Ran in WSL
Even though WSL doesn’t use a traditional bootloader or BIOS for Linux,
I can still inspect the init system and active services.

Check what process is PID 1:
```bash
ps -p 1 -o comm=
```

List running services (WSL systemd):
```bash
systemctl list-units --type=service --state=running
```

## 3. Summary (In My Words)
This seems like the boot pattern for Linux machines:
    * The bootloader starts Linux
    * The kernel prepares the system
    * init/systemd launches services
    * This forms the foundation of a running Linux OS

### It seems as though understanding this helps with troubleshooting, cloud servers, and DevOps work












