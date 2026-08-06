# Linux Disk Partition Commands Cheatsheet

## 1. lsblk

```bash
lsblk
```

**Syntax**

```bash
lsblk [options]
```

**Purpose**

* Displays block devices and partition structure.

**Example**

```bash
lsblk
```

**Notes**

* First command to understand disk layout.
* Shows disks, partitions, and mount points.

---

## 2. lsblk -f

```bash
lsblk -f
```

**Syntax**

```bash
lsblk -f
```

**Purpose**

* Displays filesystem information.

**Example**

```bash
lsblk -f
```

**Notes**

* Shows:

  * Filesystem type
  * UUID
  * Mount point

---

## 3. fdisk -l

```bash
sudo fdisk -l
```

**Syntax**

```bash
fdisk -l [device]
```

**Purpose**

* Lists partition tables.

**Example**

```bash
sudo fdisk -l /dev/nvme0n1
```

**Notes**

* Useful for checking MBR/GPT partitions.
* Requires root privileges.

---

## 4. parted -l

```bash
sudo parted -l
```

**Syntax**

```bash
parted -l
```

**Purpose**

* Displays all disks and partition information.

**Example**

```bash
sudo parted -l
```

**Notes**

* Supports GPT and MBR.

---

## 5. parted print free

```bash
sudo parted /dev/nvme0n1 print free
```

**Syntax**

```bash
parted /dev/device print free
```

**Purpose**

* Shows partitions and unallocated space.

**Example**

```bash
sudo parted /dev/nvme0n1 print free
```

**Notes**

* Useful before resizing partitions.

---

## 6. df -h

```bash
df -h
```

**Syntax**

```bash
df [options]
```

**Purpose**

* Displays filesystem disk usage.

**Example**

```bash
df -h
```

**Notes**

* Shows:

  * Used space
  * Available space
  * Mount points

---

## 7. findmnt

```bash
findmnt
```

**Syntax**

```bash
findmnt [options]
```

**Purpose**

* Displays mounted filesystems.

**Example**

```bash
findmnt /
```

**Notes**

* Useful for identifying active mounts.

---

## 8. mount

```bash
mount
```

**Syntax**

```bash
mount [device] [directory]
```

**Purpose**

* Mounts filesystems.

**Example**

```bash
sudo mount /dev/sdb1 /mnt
```

**Notes**

* Used to access filesystems.

---

## 9. umount

```bash
umount
```

**Syntax**

```bash
umount [device|mountpoint]
```

**Purpose**

* Safely unmounts filesystems.

**Example**

```bash
sudo umount /dev/sdb1
```

**Notes**

* Required before modifying partitions.

---

## 10. swapoff

```bash
swapoff
```

**Syntax**

```bash
swapoff [device]
```

**Purpose**

* Disables swap.

**Example**

```bash
sudo swapoff /swapfile
```

**Notes**

* Needed before resizing swap areas.

---

## 11. swapon

```bash
swapon
```

**Syntax**

```bash
swapon [options]
```

**Purpose**

* Enables swap.

**Example**

```bash
sudo swapon --show
```

**Notes**

* Verify active swap spaces.

---

## 12. dd

```bash
dd
```

**Syntax**

```bash
dd if=input of=output
```

**Purpose**

* Copies data at block level.

**Example**

```bash
sudo dd if=kali.iso of=/dev/sdb bs=4M status=progress
```

**Notes**

* Dangerous command.
* Wrong target can destroy data.

---

## 13. sync

```bash
sync
```

**Syntax**

```bash
sync
```

**Purpose**

* Writes cached data to storage.

**Example**

```bash
sync
```

**Notes**

* Recommended after disk operations.

---

## 14. blkid

```bash
blkid
```

**Syntax**

```bash
blkid [device]
```

**Purpose**

* Displays filesystem UUIDs and types.

**Example**

```bash
sudo blkid
```

**Notes**

* Useful for `/etc/fstab` configuration.

---

## 15. e2fsck

```bash
e2fsck
```

**Syntax**

```bash
e2fsck [options] device
```

**Purpose**

* Checks and repairs ext filesystem errors.

**Example**

```bash
sudo e2fsck -f /dev/nvme0n1p5
```

**Notes**

* Filesystem must be unmounted.

---

## 16. resize2fs

```bash
resize2fs
```

**Syntax**

```bash
resize2fs device
```

**Purpose**

* Resizes ext2/ext3/ext4 filesystems.

**Example**

```bash
sudo resize2fs /dev/nvme0n1p5
```

**Notes**

* Used after expanding partitions.

---

## 17. smartctl

```bash
smartctl
```

**Syntax**

```bash
smartctl [options] device
```

**Purpose**

* Checks drive health using SMART data.

**Example**

```bash
sudo smartctl -a /dev/nvme0n1
```

**Notes**

* Useful for checking SSD/HDD health.

---

## 18. sfdisk

```bash
sfdisk
```

**Syntax**

```bash
sfdisk [options] device
```

**Purpose**

* Creates and manages partition tables.

**Example**

```bash
sudo sfdisk -l /dev/nvme0n1
```

**Notes**

* Useful for scripting partition layouts.

---

## 19. timeshift

```bash
timeshift
```

**Syntax**

```bash
timeshift [options]
```

**Purpose**

* Creates and restores system snapshots.

**Example**

```bash
sudo timeshift --create
```

**Notes**

* Useful before major system changes.

---

## 20. sha256sum

```bash
sha256sum
```

**Syntax**

```bash
sha256sum file
```

**Purpose**

* Verifies file integrity.

**Example**

```bash
sha256sum kali-linux.iso
```

**Notes**

* Used to verify downloaded ISOs.

---

# Quick Disk Troubleshooting Flow

```bash
lsblk
```

↓

```bash
lsblk -f
```

↓

```bash
df -h
```

↓

```bash
sudo fdisk -l
```

↓

```bash
sudo parted -l
```

↓

```bash
findmnt
```

↓

```bash
sudo smartctl -a /dev/device
```

---

# Summary

Essential commands for:

* Disk identification
* Partition management
* Filesystem checks
* Storage troubleshooting
* Backup preparation
* Linux system maintenance
