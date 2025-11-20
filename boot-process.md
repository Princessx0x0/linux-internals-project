# Linux Boot Process – My Notes
This document explains the Linux boot process in my own words and includes commands I ran inside WSL to explore how Linux starts services.

---

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

---    

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

---

## 3. Summary (In My Words)
This seems like the boot pattern for Linux machines:
    * The bootloader starts Linux
    * The kernel prepares the system
    * init/systemd launches services
    * This forms the foundation of a running Linux OS

---

## 4. Boot Failure Modes & Troubleshooting

Learning about the Linux boot system was rewarding however the need to explore possible failures with the boot process felt important.
Below are common failure modes at each stage of the boot process, what causes them, and what the symptoms look like.

---

## 4.1 BIOS / UEFI Failures

BIOS/UEFI is the very first layer.  
If failure happens here, Linux is not involved at all.

### **Symptoms**
- Stuck on manufacturer logo  
- "No bootable device found"  
- Boot loop before GRUB  
- Incorrect date/time on every boot (CMOS battery issue)

### **Common Causes**
- Wrong boot order  
- Disabled disk controller (SATA/NVMe disabled in BIOS)  
- Corrupt NVRAM settings  
- Secure Boot blocking unsigned components  
- Dead or corrupted disk  
- CMOS battery failure (causes time resets and erratic behavior)

### **Cloud Equivalent**
Cloud VMs skip BIOS entirely, but “no bootable device” maps to:
- deleted root disk  
- corrupted boot volume  
- OS image not found  

---

## 4.2 Bootloader (GRUB) Failures

GRUB loads the kernel.  
If GRUB breaks, Linux never starts.

### **Symptoms**
- `grub>` prompt  
- `grub rescue>` prompt  
- “Unknown filesystem”  
- “Minimal BASH-like line editing”  
- Boot menu missing

### **Common Causes**
- Wrong GRUB configuration (`grub.cfg` missing or misconfigured)
- Root partition UUID changed  
- Kernel update broke GRUB  
- Filesystem corruption  
- You edited partition layout but didn’t reinstall GRUB  

### **Fix**
- Boot from live USB  
- Reinstall GRUB:

```bash
sudo grub-install /dev/sda
sudo update-grub
```
### **Cloud Equivalent**
- GRUB errors visible in serial console
- AMI/VM image missing GRUB files
- Corrupt or missing `/boot` partition

---

## 4.3 Kernel Failures

After GRUB loads the kernel, initialization begins.
Kernel problems typically result in kernel panics or initramfs shells.

### **Symptoms**
- Kernel panic
- `Unable to mount root fs`
- `VFS: Cannot open root device`
- Dropped into `initramfs` shell
- Reboot loop

### **Common Causes**
- Bad kernel update
- Missing drivers (disk/NVMe/RAID)
- Corrupt `initramfs`
- Wrong root filesystem UUID
- Hardware compatibility issues

### **Cloud Equivalent**
- Wrong kernel used in custom image
- Damaged root disk
- Incompatible drivers for hypervisor

---

## 4.4 init / systemd Failures

If the kernel loads but init/systemd cannot complete startup,
the system enters emergency mode or rescue mode.

### **Symptoms**
- Emergency mode prompt
- Maintenance mode
- “Failed to mount /home”
- “Dependency failed for …”
- Several `FAILED` units during boot

### **Common Causes**
- Incorrect `/etc/fstab` entries
- Missing or corrupt partitions
- Broken systemd service files
- Disk full (especially `/`, `/var`, `/home`)
- Service dependency loops

### **Fix**

Check failed services:
```bash
systemctl --failed
```

View boot logs:
```bash
journalctl -xb
```

Fix filesystem or service issues accordingly.

### Cloud Equivalent
- Cloud-init stuck or failing
- Startup script errors
- Missing attached volumes required by `/etc/fstab`

---

## 4.5 User Space Failures

Kernel and systemd succeed, but the user environment fails.

### **Symptoms**
- No login prompt
- Black screen after login
- Desktop environment not loading
- SSH not accepting connections
- Authentication errors


### **Common Causes**
- Misconfigured shell
- GUI/desktop package failures
- Incorrect permissions on /home
- Broken `/sshd_config`
- PAM authentication issues

### **Fix**
Check SSH status:
```bash
systemctl status ssh
journalctl -u ssh
```
Reset shell or fix user config.

That concludes the exploration of possible boot errors can could occur and their fixes.

### It seems as though understanding this helps with troubleshooting, cloud servers, and DevOps work












