# 04 Storage and Filesystem

## Theme of This Chapter

A computer cannot keep working with only the CPU and memory.

Files you create, software you install, configuration files, logs, and other data are saved in a place where they remain even after the power is turned off.

In this chapter, you will observe the following on Linux:

- What storage is
- What a filesystem is
- What a directory structure is
- What mounting means
- How to check disk capacity and usage
- What an inode is

---

## 1. What Is Storage?

Storage is a device used to save data.

Typical examples of storage include:

- HDD
- SSD
- USB flash drive
- SD card
- Virtual disk

In Linux, these devices are also handled like files.

---

## 2. Checking Storage Devices

First, check the storage devices recognized by Linux.

```bash
lsblk
```

`lsblk` is a command that lists `block devices`.

A `block device` is a device that reads and writes data in fixed-size blocks.

Example:

```text
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0   64G  0 disk
├─sda1   8:1    0    1G  0 part /boot
└─sda2   8:2    0   63G  0 part /
```

From this example, we can read the following:

- `sda` is the whole disk
- `sda1` and `sda2` are partitions
- `/` and `/boot` are mount points

---

## 3. What Is a Partition?

A partition is a divided area of one storage device.

For example, one SSD can be divided into areas such as:

- Area for the OS
- Area for booting
- Area for storing data

In Linux, each partition can be formatted with a filesystem and used.

Check the partitions.

```bash
sudo fdisk -l
```

Or you can use the following command to also check filesystem types.

```bash
lsblk -f
```

---

## 4. What Is a Filesystem?

A filesystem is a mechanism for saving and managing files and directories on storage.

Typical filesystems include the following:

| Filesystem | Main Use |
| --- | --- |
| ext4 | Commonly used in Linux |
| xfs | Commonly used in RHEL-based systems such as AlmaLinux |
| btrfs | Has advanced features such as snapshots |
| vfat | Sometimes used for USB flash drives |
| ntfs | Commonly used in Windows |

Check the filesystem used in your current environment.

```bash
df -T
```

---

## 5. What Is Mounting?

Mounting means connecting a storage device or partition into the Linux directory structure.

Linux does not manage storage with drive names such as `C:` or `D:` like Windows.

In Linux, all files and directories are placed under one tree structure starting from `/`.

Example:

```text
/
├── boot
├── home
├── var
├── etc
└── tmp
```

Even if the storage device is different, it is connected to some directory.

Check the mount status.

```bash
mount
```

If there is too much information, combine it with `grep`.

```bash
mount | grep "^/dev"
```

Or use the following command for easier viewing.

```bash
findmnt
```

---

## 6. Checking Disk Capacity

Use the `df` command to check disk usage.

```bash
df -h
```

`-h` means human readable.

It displays sizes in units that are easier for humans to read.

Example:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        63G   12G   51G  20% /
```

From this example, we can read the following:

- Total size: 63G
- Used: 12G
- Available: 51G
- Usage rate: 20%
- Mount point: /

---

## 7. Checking Directory Usage

`df` checks the usage of the entire filesystem.

On the other hand, use `du` when you want to check usage by directory.

```bash
du -sh /var
```

Meaning:

- `du`: disk usage
- `-s`: summary
- `-h`: human readable

You can also compare multiple directories.

```bash
sudo du -sh /var/* 2>/dev/null
```

`/var` stores data that changes frequently, such as logs and cache files.

---

## 8. What Is an inode?

In a Linux filesystem, there is management information for the actual file, separate from the file name.

This management information is called an inode.

An inode contains information such as:

- Owner
- Permissions
- File size
- Modification time
- Location of the data

Check inode numbers.

```bash
ls -i
```

Example:

```text
123456 README.md
```

The number such as `123456` is the inode number.

---

## 9. Relationship Between File Names and inodes

A file name is a name that is easy for humans to handle.

However, inside the Linux filesystem, files are managed using inodes.

In other words, a file name is like a label pointing to an inode.

Check this.

```bash
touch sample.txt
ls -li sample.txt
```

Next, create a hard link.

```bash
ln sample.txt sample_link.txt
ls -li sample.txt sample_link.txt
```

You can confirm that the two file names point to the same inode number.

---

## 10. Difference from a Symbolic Link

A symbolic link is a reference to another file.

```bash
ln -s sample.txt sample_symlink.txt
ls -li sample.txt sample_symlink.txt
```

A symbolic link has a different inode from the original file.

Check it.

```bash
ls -l sample_symlink.txt
```

Example:

```text
sample_symlink.txt -> sample.txt
```

---

## 11. What Is /etc/fstab?

`/etc/fstab` is a file that defines which filesystems are mounted to which locations at startup.

Check its contents.

```bash
cat /etc/fstab
```

Or:

```bash
less /etc/fstab
```

`/etc/fstab` is an important configuration file.

If it is edited incorrectly, the OS may not boot properly.

In this chapter, only check the contents. Do not edit it.

---

## 12. Practice: Observing the Filesystem

Check the following items and save the results to `04_storage_report.txt`.

### 1. Check the current directory

```bash
pwd >> 04_storage_report.txt
```

### 2. Check block devices

```bash
lsblk >> 04_storage_report.txt
```

### 3. Check filesystem types

```bash
df -T >> 04_storage_report.txt
```

### 4. Check disk capacity

```bash
df -h >> 04_storage_report.txt
```

### 5. Check mount status

```bash
findmnt >> 04_storage_report.txt
```

### 6. Check the size of /var

```bash
sudo du -sh /var 2>/dev/null >> 04_storage_report.txt
```

### 7. Check inode numbers

```bash
ls -li >> 04_storage_report.txt
```

---

## 13. Reflection Questions

Answer the following questions in your own words.

### Q1. What is the difference between storage and memory?

Hints:

- Whether data remains after the power is turned off
- Whether the CPU uses it directly for work
- Whether it is a place to save files

---

### Q2. What is a filesystem used for?

Hints:

- File names
- Directories
- Owners
- Permissions
- Storage locations

---

### Q3. Why does Linux manage files starting from `/` instead of using `C:` or `D:`?

Hints:

- Everything is handled inside one directory structure
- Other storage devices are also connected to some directory
- The idea of mounting

---

### Q4. What is the difference between `df` and `du`?

Hints:

- Looking at the entire filesystem
- Looking at directories or files individually

---

### Q5. What is an inode?

Hints:

- It is not the file name itself
- It is management information for a file
- It is related to hard links

---

## 14. Summary of This Chapter

In this chapter, you learned about storage and filesystems in Linux.

Important points are as follows:

- Storage is a device for saving data
- A partition is a divided area of storage
- A filesystem is a mechanism for managing files and directories
- In Linux, all files are placed in a tree structure starting from `/`
- Mounting connects storage to the directory structure
- `df` checks the capacity of the entire filesystem
- `du` checks usage by directory
- An inode is file management information

Storage and filesystems are closely related to log management, user management, permission management, and security.

This chapter is a foundation for future Linux learning.
