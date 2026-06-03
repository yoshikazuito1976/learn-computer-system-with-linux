# 04 存储与文件系统

## 本章主题

计算机不能只依靠 CPU 和内存持续工作。

创建的文件、安装的软件、配置文件、日志等数据，需要保存在即使关机后也能保留的地方。

本章将在 Linux 上观察以下内容：

- 什么是存储
- 什么是文件系统
- 什么是目录结构
- 什么是挂载
- 如何确认容量和使用情况
- 什么是 inode

---

## 1. 什么是存储

存储是用来保存数据的设备。

常见的存储设备包括：

- HDD
- SSD
- USB 闪存盘
- SD 卡
- 虚拟磁盘

在 Linux 中，这些设备也会像文件一样被处理。

---

## 2. 确认存储设备

首先，确认 Linux 识别到的存储设备。

```bash
lsblk
```

`lsblk` 是显示 `block device` 列表的命令。

`block device` 是指以固定大小的数据块为单位进行读写的设备。

示例：

```text
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0   64G  0 disk
├─sda1   8:1    0    1G  0 part /boot
└─sda2   8:2    0   63G  0 part /
```

从这里可以读出以下内容：

- `sda` 是整个磁盘
- `sda1` 和 `sda2` 是分区
- `/` 和 `/boot` 是挂载点

---

## 3. 什么是分区

分区是把一个存储设备划分出来的区域。

例如，一个 SSD 可以分成以下区域：

- 存放 OS 的区域
- 用于启动的区域
- 保存数据的区域

在 Linux 中，每个分区可以创建文件系统后使用。

确认一下。

```bash
sudo fdisk -l
```

或者使用以下命令，也可以确认文件系统类型。

```bash
lsblk -f
```

---

## 4. 什么是文件系统

文件系统是在存储设备上保存和管理文件、目录的机制。

常见的文件系统如下：

| 文件系统 | 主要用途 |
| --- | --- |
| ext4 | Linux 中常用 |
| xfs | RHEL 系统、AlmaLinux 等常用 |
| btrfs | 具有 snapshot 等高级功能 |
| vfat | 有时用于 USB 闪存盘 |
| ntfs | Windows 中常用 |

确认当前环境中使用的文件系统。

```bash
df -T
```

---

## 5. 什么是挂载

挂载是指把存储设备或分区连接到 Linux 的目录结构中。

Linux 不像 Windows 那样使用 `C:` 或 `D:` 这样的驱动器名称来管理存储。

在 Linux 中，所有文件和目录都放在以 `/` 为顶点的一棵树状结构中。

示例：

```text
/
├── boot
├── home
├── var
├── etc
└── tmp
```

即使是不同的存储设备，也会被连接到某个目录上。

确认挂载状态。

```bash
mount
```

如果信息太多，可以与 `grep` 组合使用。

```bash
mount | grep "^/dev"
```

或者使用以下命令，更容易查看。

```bash
findmnt
```

---

## 6. 确认磁盘容量

确认磁盘使用量时，使用 `df` 命令。

```bash
df -h
```

`-h` 表示 human readable。

它会用人更容易阅读的单位显示容量。

示例：

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        63G   12G   51G  20% /
```

从这里可以读出以下内容：

- 总容量：63G
- 已使用：12G
- 可用容量：51G
- 使用率：20%
- 挂载点：/

---

## 7. 确认每个目录的使用量

`df` 是确认整个文件系统使用量的命令。

如果想确认每个目录的容量，使用 `du`。

```bash
du -sh /var
```

含义：

- `du`：disk usage
- `-s`：summary
- `-h`：human readable

也可以比较多个目录。

```bash
sudo du -sh /var/* 2>/dev/null
```

`/var` 中保存日志、缓存等经常变化的数据。

---

## 8. 什么是 inode

在 Linux 文件系统中，除了文件名之外，还有用于管理文件实体的信息。

这种管理信息称为 inode。

inode 中包含例如以下信息：

- 所有者
- 权限
- 文件大小
- 更新时间
- 数据保存位置

确认 inode 编号。

```bash
ls -i
```

示例：

```text
123456 README.md
```

像 `123456` 这样的数字就是 inode 编号。

---

## 9. 文件名与 inode 的关系

文件名是人类容易使用的名称。

但是，在 Linux 文件系统内部，文件是通过 inode 来管理的。

也就是说，文件名就像指向 inode 的标签。

确认一下。

```bash
touch sample.txt
ls -li sample.txt
```

接下来，创建硬链接。

```bash
ln sample.txt sample_link.txt
ls -li sample.txt sample_link.txt
```

可以确认两个文件名指向同一个 inode 编号。

---

## 10. 与符号链接的区别

符号链接是指向另一个文件的引用。

```bash
ln -s sample.txt sample_symlink.txt
ls -li sample.txt sample_symlink.txt
```

符号链接拥有与原文件不同的 inode。

确认一下。

```bash
ls -l sample_symlink.txt
```

示例：

```text
sample_symlink.txt -> sample.txt
```

---

## 11. 什么是 /etc/fstab

`/etc/fstab` 是定义系统启动时把哪个文件系统挂载到哪个位置的文件。

确认内容。

```bash
cat /etc/fstab
```

或者：

```bash
less /etc/fstab
```

`/etc/fstab` 是重要的配置文件。

如果错误编辑，OS 可能无法正常启动。

本章只进行确认，不进行编辑。

---

## 12. 实习：观察文件系统

确认以下内容，并把结果保存到 `04_storage_report.txt`。

### 1. 确认当前目录

```bash
pwd >> 04_storage_report.txt
```

### 2. 确认 block device

```bash
lsblk >> 04_storage_report.txt
```

### 3. 确认文件系统类型

```bash
df -T >> 04_storage_report.txt
```

### 4. 确认磁盘容量

```bash
df -h >> 04_storage_report.txt
```

### 5. 确认挂载状态

```bash
findmnt >> 04_storage_report.txt
```

### 6. 确认 /var 的容量

```bash
sudo du -sh /var 2>/dev/null >> 04_storage_report.txt
```

### 7. 确认 inode 编号

```bash
ls -li >> 04_storage_report.txt
```

---

## 13. 思考问题

请用自己的话回答以下问题。

### Q1. 存储和内存有什么区别？

提示：

- 关机后数据是否保留
- CPU 是否直接用于作业
- 是否是保存文件的地方

---

### Q2. 文件系统是为了什么而存在的？

提示：

- 文件名
- 目录
- 所有者
- 权限
- 保存位置

---

### Q3. 为什么 Linux 不使用 `C:` 或 `D:`，而是使用从 `/` 开始的结构来管理？

提示：

- 所有内容都在一个目录结构中处理
- 其他存储设备也会连接到某个目录
- 挂载的概念

---

### Q4. `df` 和 `du` 有什么区别？

提示：

- 查看整个文件系统
- 按目录或文件查看

---

### Q5. inode 是什么？

提示：

- 不是文件名本身
- 是文件的管理信息
- 与硬链接有关

---

## 14. 本章总结

本章学习了 Linux 中的存储和文件系统。

重要要点如下：

- 存储是保存数据的设备
- 分区是把存储划分出来的区域
- 文件系统是管理文件和目录的机制
- 在 Linux 中，所有文件都放在以 `/` 开始的树状结构中
- 挂载会把存储连接到目录结构中
- `df` 可以确认整个文件系统的容量
- `du` 可以确认每个目录的使用量
- inode 是文件的管理信息

存储和文件系统与日志管理、用户管理、权限管理、安全性都有很深的关系。

本章是今后学习 Linux 的基础。
