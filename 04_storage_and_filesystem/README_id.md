# 04 Storage dan Filesystem

## Tema Bab Ini

Komputer tidak dapat terus bekerja hanya dengan CPU dan memori.

File yang dibuat, perangkat lunak yang diinstal, file konfigurasi, log, dan data lainnya disimpan di tempat yang tetap ada meskipun daya dimatikan.

Pada bab ini, kita akan mengamati hal-hal berikut di Linux:

- Apa itu storage
- Apa itu filesystem
- Apa itu struktur direktori
- Apa arti mount
- Cara memeriksa kapasitas dan penggunaan disk
- Apa itu inode

---

## 1. Apa Itu Storage?

Storage adalah perangkat untuk menyimpan data.

Contoh storage yang umum adalah:

- HDD
- SSD
- USB flash drive
- Kartu SD
- Disk virtual

Di Linux, perangkat-perangkat ini juga diperlakukan seperti file.

---

## 2. Memeriksa Perangkat Storage

Pertama, periksa perangkat storage yang dikenali oleh Linux.

```bash
lsblk
```

`lsblk` adalah perintah untuk menampilkan daftar `block device`.

`block device` adalah perangkat yang membaca dan menulis data dalam satuan blok berukuran tetap.

Contoh:

```text
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda      8:0    0   64G  0 disk
├─sda1   8:1    0    1G  0 part /boot
└─sda2   8:2    0   63G  0 part /
```

Dari contoh ini, kita dapat membaca hal berikut:

- `sda` adalah seluruh disk
- `sda1` dan `sda2` adalah partisi
- `/` dan `/boot` adalah lokasi mount

---

## 3. Apa Itu Partisi?

Partisi adalah area yang dibagi dari satu perangkat storage.

Misalnya, satu SSD dapat dibagi menjadi beberapa area seperti:

- Area untuk OS
- Area untuk boot
- Area untuk menyimpan data

Di Linux, setiap partisi dapat dibuatkan filesystem dan digunakan.

Mari kita periksa.

```bash
sudo fdisk -l
```

Atau gunakan perintah berikut untuk melihat jenis filesystem juga.

```bash
lsblk -f
```

---

## 4. Apa Itu Filesystem?

Filesystem adalah mekanisme untuk menyimpan dan mengelola file serta direktori di atas storage.

Contoh filesystem yang umum adalah:

| Filesystem | Penggunaan Utama |
| --- | --- |
| ext4 | Sering digunakan di Linux |
| xfs | Sering digunakan di sistem berbasis RHEL seperti AlmaLinux |
| btrfs | Memiliki fitur lanjutan seperti snapshot |
| vfat | Kadang digunakan pada USB flash drive |
| ntfs | Sering digunakan di Windows |

Periksa filesystem yang digunakan pada lingkungan saat ini.

```bash
df -T
```

---

## 5. Apa Itu Mount?

Mount berarti menghubungkan storage atau partisi ke dalam struktur direktori Linux.

Linux tidak mengelola storage dengan nama drive seperti `C:` atau `D:` seperti Windows.

Di Linux, semua file dan direktori ditempatkan dalam satu struktur pohon yang dimulai dari `/`.

Contoh:

```text
/
├── boot
├── home
├── var
├── etc
└── tmp
```

Meskipun perangkat storagenya berbeda, perangkat tersebut akan dihubungkan ke salah satu direktori.

Periksa status mount.

```bash
mount
```

Jika informasinya terlalu banyak, kombinasikan dengan `grep`.

```bash
mount | grep "^/dev"
```

Atau gunakan perintah berikut agar lebih mudah dilihat.

```bash
findmnt
```

---

## 6. Memeriksa Kapasitas Disk

Gunakan perintah `df` untuk memeriksa penggunaan disk.

```bash
df -h
```

`-h` berarti human readable.

Opsi ini menampilkan ukuran dengan satuan yang mudah dibaca oleh manusia.

Contoh:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        63G   12G   51G  20% /
```

Dari contoh ini, kita dapat membaca hal berikut:

- Kapasitas total: 63G
- Terpakai: 12G
- Tersedia: 51G
- Persentase penggunaan: 20%
- Lokasi mount: /

---

## 7. Memeriksa Penggunaan per Direktori

`df` digunakan untuk memeriksa penggunaan seluruh filesystem.

Sebaliknya, gunakan `du` jika ingin memeriksa kapasitas berdasarkan direktori.

```bash
du -sh /var
```

Arti opsi:

- `du`: disk usage
- `-s`: summary
- `-h`: human readable

Anda juga dapat membandingkan beberapa direktori.

```bash
sudo du -sh /var/* 2>/dev/null
```

`/var` menyimpan data yang sering berubah, seperti log dan file cache.

---

## 8. Apa Itu inode?

Dalam filesystem Linux, terdapat informasi pengelolaan untuk file sebenarnya, yang terpisah dari nama file.

Informasi pengelolaan ini disebut inode.

inode berisi informasi seperti:

- Pemilik
- Hak akses
- Ukuran file
- Waktu pembaruan
- Lokasi penyimpanan data

Periksa nomor inode.

```bash
ls -i
```

Contoh:

```text
123456 README.md
```

Nomor seperti `123456` adalah nomor inode.

---

## 9. Hubungan Antara Nama File dan inode

Nama file adalah nama yang mudah digunakan oleh manusia.

Namun, di dalam filesystem Linux, file dikelola menggunakan inode.

Dengan kata lain, nama file seperti label yang menunjuk ke inode.

Mari kita periksa.

```bash
touch sample.txt
ls -li sample.txt
```

Berikutnya, buat hard link.

```bash
ln sample.txt sample_link.txt
ls -li sample.txt sample_link.txt
```

Anda dapat memastikan bahwa dua nama file tersebut menunjuk ke nomor inode yang sama.

---

## 10. Perbedaan dengan Symbolic Link

Symbolic link adalah referensi ke file lain.

```bash
ln -s sample.txt sample_symlink.txt
ls -li sample.txt sample_symlink.txt
```

Symbolic link memiliki inode yang berbeda dari file asli.

Periksa dengan perintah berikut.

```bash
ls -l sample_symlink.txt
```

Contoh:

```text
sample_symlink.txt -> sample.txt
```

---

## 11. Apa Itu /etc/fstab?

`/etc/fstab` adalah file yang menentukan filesystem mana yang akan di-mount ke lokasi mana saat sistem dinyalakan.

Periksa isinya.

```bash
cat /etc/fstab
```

Atau:

```bash
less /etc/fstab
```

`/etc/fstab` adalah file konfigurasi yang penting.

Jika diedit secara salah, OS mungkin tidak dapat boot dengan benar.

Pada bab ini, cukup periksa isinya. Jangan mengeditnya.

---

## 12. Praktik: Mengamati Filesystem

Periksa item berikut dan simpan hasilnya ke `04_storage_report.txt`.

### 1. Periksa direktori saat ini

```bash
pwd >> 04_storage_report.txt
```

### 2. Periksa block device

```bash
lsblk >> 04_storage_report.txt
```

### 3. Periksa jenis filesystem

```bash
df -T >> 04_storage_report.txt
```

### 4. Periksa kapasitas disk

```bash
df -h >> 04_storage_report.txt
```

### 5. Periksa status mount

```bash
findmnt >> 04_storage_report.txt
```

### 6. Periksa ukuran /var

```bash
sudo du -sh /var 2>/dev/null >> 04_storage_report.txt
```

### 7. Periksa nomor inode

```bash
ls -li >> 04_storage_report.txt
```

---

## 13. Pertanyaan Refleksi

Jawablah pertanyaan berikut dengan kata-kata Anda sendiri.

### Q1. Apa perbedaan antara storage dan memori?

Petunjuk:

- Apakah data tetap ada setelah daya dimatikan
- Apakah CPU menggunakannya secara langsung untuk bekerja
- Apakah itu tempat untuk menyimpan file

---

### Q2. Untuk apa filesystem digunakan?

Petunjuk:

- Nama file
- Direktori
- Pemilik
- Hak akses
- Lokasi penyimpanan

---

### Q3. Mengapa Linux mengelola file mulai dari `/`, bukan menggunakan `C:` atau `D:`?

Petunjuk:

- Semua hal dikelola dalam satu struktur direktori
- Storage lain juga dihubungkan ke suatu direktori
- Konsep mount

---

### Q4. Apa perbedaan antara `df` dan `du`?

Petunjuk:

- Melihat seluruh filesystem
- Melihat direktori atau file secara individual

---

### Q5. Apa itu inode?

Petunjuk:

- Bukan nama file itu sendiri
- Informasi pengelolaan file
- Berhubungan dengan hard link

---

## 14. Ringkasan Bab Ini

Pada bab ini, Anda mempelajari storage dan filesystem di Linux.

Poin pentingnya adalah sebagai berikut:

- Storage adalah perangkat untuk menyimpan data
- Partisi adalah area storage yang dibagi
- Filesystem adalah mekanisme untuk mengelola file dan direktori
- Di Linux, semua file ditempatkan dalam struktur pohon yang dimulai dari `/`
- Mount menghubungkan storage ke struktur direktori
- `df` dapat memeriksa kapasitas seluruh filesystem
- `du` dapat memeriksa penggunaan berdasarkan direktori
- inode adalah informasi pengelolaan file

Storage dan filesystem sangat berkaitan dengan pengelolaan log, pengelolaan pengguna, pengelolaan hak akses, dan keamanan.

Bab ini menjadi dasar untuk pembelajaran Linux berikutnya.
