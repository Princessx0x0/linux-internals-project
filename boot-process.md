Linux Boot Process – My Notes
This document explains the Linux boot process in my own words
and includes commands I ran inside WSL to explore how Linux starts services.

1. High-Level Boot Sequence
BIOS/UEFI: Hardware checks; Looks for a bootable device
Boot Loader (GRUB): Loads and launches the Linux kernel into memory
Kernel: Initializes drivers, memory, CPU scheduling; Mounts the initial RAM disk (initramfs)
init (PID 1): The first user-space process; Starts system services (network, logging, sshd, etc.)
Login or GUI: Terminal login prompt; Or a graphical desktop (if installed)

2. Practical Checks I Ran in WSL
Even though WSL doesn’t use a traditional bootloader or BIOS for Linux,
I can still inspect the init system and active services.

Check what process is PID 1:
ps -p 1 -o comm=

List running services (WSL systemd):
systemctl list-units --type=service --state=running

3. Summary (In My Words)
The bootloader starts Linux
The kernel prepares the system
init/systemd launches services
This forms the foundation of a running Linux OS
Understanding this helps with troubleshooting, cloud servers, and DevOps work












