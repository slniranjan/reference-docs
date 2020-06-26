### find
Search files in linux including advance options.
```
find /home -name *.jpg // Find all .jpg files in the /home and sub-directories.
find . -type f -empty // Find an empty file within the current directory.
-type d --> search for directories
 
find /home -user exampleuser -mtime -7 -iname ".db"
// Find all .db files (ignoring text case) modified
// in the last 7 days by a user named exampleuser
 
find . -type f -exec grep "example" '{}' \; -print
// Use Grep to Find Files Based on Content
 
find . -name "rc.conf" -exec chmod o+r '{}' \; // find and process files
find . -name "*.bak" -delete // delete all .bak files
find . -name "*.srt" -exec rm -r {} \;

```
### dpkg
1. Find installed packages
  - dpkg --get-selections | grep "softmaker"
    --> output softmaker-freeoffice-2016:i386          install
2. Remove package
  - sudo dpkg -r softmaker-freeoffice-2016:i386
### Clean journal
```
journalctl --rotate
journalctl --vacuum-time=1s
```
### List devices
```
lsblk --> List block devices (for example, the drives).
lspci --> List PCI devices.
lsusb --> List USB devices.
```
### Safely remove device
```
udisksctl unmount -b /dev/sda1
udisksctl power-off -b /dev/sda1
```
