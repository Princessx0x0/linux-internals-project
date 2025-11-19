Linux Commands – Quick Reference

A personal cheat-sheet of useful Linux commands I’ve learned and used
while studying Linux internals.

File & Directory Commands
ls            # list files
ls -l         # detailed list
cd DIR        # change directory
pwd           # print working directory
mkdir DIR     # create directory
touch FILE    # create empty file
rm FILE       # remove file
rm -r DIR     # remove directory
cp SRC DST    # copy files
mv SRC DST    # move/rename files

System Information
uname -a       # kernel info
hostnamectl    # OS + kernel + machine info
df -h          # disk usage
du -sh DIR     # folder size
free -h        # memory usage
top            # running processes

Package Management (Ubuntu / Debian)
sudo apt update
sudo apt upgrade
sudo apt install PACKAGE
sudo apt remove PACKAGE

Filesystem & Partitions
lsblk             # list block devices
mount             # show mounted filesystems
df -Th            # show filesystem types
sudo mkfs.ext4    # format a filesystem (NOT in WSL)

Services (Using systemd)
systemctl status SERVICE
systemctl start SERVICE
systemctl stop SERVICE
systemctl enable SERVICE
systemctl disable SERVICE

Process Management
ps aux        # list all processes
kill PID      # kill process
pgrep NAME    # find PID by name

Networking
ip a               # show network interfaces
ping google.com    # test connectivity
curl localhost     # test local web server