# 00_environment

## Tujuan bab ini

Pada bab ini, Anda akan belajar cara memeriksa lingkungan Linux yang sedang digunakan.

Sebelum mengoperasikan sistem komputer, hal pertama yang penting dilakukan adalah mengamati kondisi saat ini:

- Saya sedang berada di direktori mana?
- Saya sedang menggunakan pengguna siapa?
- Sistem operasi apa yang sedang berjalan?
- Apa nama komputer ini?
- Sudah berapa lama sistem ini berjalan?

Di Linux, banyak informasi sistem ditampilkan dalam bentuk teks.
Tujuan bab ini adalah membaca informasi teks tersebut dan menjelaskan lingkungan kerja Anda dengan kata-kata sendiri.

---

## Alur pembelajaran

Pada bab ini, Anda akan mempelajari hal-hal berikut:

1. Memeriksa direktori saat ini
2. Memeriksa pengguna saat ini
3. Memeriksa nama host
4. Memeriksa informasi OS
5. Memeriksa informasi kernel
6. Memeriksa tanggal dan waktu saat ini
7. Memeriksa lama sistem berjalan
8. Menjelaskan lingkungan kerja dengan kata-kata sendiri

---

## 1. Memeriksa direktori saat ini

Pertama, periksa direktori tempat Anda sedang berada.

```bash
pwd
```

`pwd` adalah singkatan dari “print working directory”.
Perintah ini menampilkan direktori tempat Anda sedang bekerja.

**Contoh keluaran**

```text
/home/siwuser/learn-computer-system-with-linux
```

Dari hasil ini, Anda dapat mengetahui posisi Anda di dalam sistem file.

---

## 2. Memeriksa pengguna saat ini

Selanjutnya, periksa pengguna yang sedang digunakan.

```bash
whoami
```

**Contoh keluaran**

```text
siwuser
```

Di Linux, setiap pengguna dapat memiliki hak akses yang berbeda.
Karena itu, penting untuk mengetahui pengguna mana yang sedang digunakan saat bekerja.

---

## 3. Memeriksa nama host

Periksa nama komputer yang sedang Anda operasikan.

```bash
hostname
```

**Contoh keluaran**

```text
localhost.localdomain
```

Hostname adalah nama yang digunakan untuk mengidentifikasi komputer, terutama di dalam jaringan.

---

## 4. Memeriksa informasi OS

Linux memiliki berbagai distribusi, seperti Ubuntu, AlmaLinux, Debian, dan Rocky Linux.

Anda dapat memeriksa informasi OS dengan perintah berikut:

```bash
cat /etc/os-release
```

**Contoh keluaran**

```text
NAME="AlmaLinux"
VERSION="9.5 (Teal Serval)"
ID="almalinux"
VERSION_ID="9.5"
```

Dari file ini, Anda dapat membaca nama distribusi Linux dan versinya.

**Bagian penting yang perlu diperhatikan**

- `NAME`
- `VERSION`
- `ID`
- `VERSION_ID`

---

## 5. Memeriksa informasi kernel

Kernel adalah bagian inti dari sistem operasi.

Anda dapat memeriksa informasi yang berkaitan dengan kernel menggunakan perintah berikut:

```bash
uname -a
```

**Contoh keluaran**

```text
Linux localhost.localdomain 5.14.0-503.el9.x86_64 #1 SMP PREEMPT_DYNAMIC x86_64 GNU/Linux
```

Dari keluaran ini, Anda dapat mengetahui informasi seperti:

- Jenis OS
- Hostname
- Versi kernel
- Arsitektur CPU

`/etc/os-release` menunjukkan informasi tentang distribusi Linux.
Sementara itu, `uname -a` menunjukkan informasi yang lebih dekat dengan kernel.

---

## 6. Memeriksa tanggal dan waktu saat ini

Periksa tanggal dan waktu saat ini.

```bash
date
```

**Contoh keluaran**

```text
Sat May 30 15:20:00 JST 2026
```

Informasi waktu sangat penting dalam administrasi sistem.
Misalnya, ketika membaca log, Anda perlu mengetahui kapan suatu peristiwa terjadi.

---

## 7. Memeriksa lama sistem berjalan

Periksa sudah berapa lama sistem berjalan.

```bash
uptime
```

**Contoh keluaran**

```text
15:20:10 up 2 hours, 15 minutes, 1 user, load average: 0.00, 0.01, 0.05
```

Dari keluaran ini, Anda dapat memeriksa:

- Waktu saat ini
- Lama sistem berjalan
- Jumlah pengguna yang sedang login
- Rata-rata beban sistem

---

## Menjalankan semua perintah sekaligus

Coba jalankan semua perintah berikut secara berurutan.

```bash
pwd
whoami
hostname
cat /etc/os-release
uname -a
date
uptime
```

Baca setiap hasilnya dan periksa hal-hal berikut:

- Saya sedang berada di direktori mana?
- Saya sedang menggunakan pengguna siapa?
- Apa hostname komputer ini?
- Apa nama dan versi OS yang digunakan?
- Apa versi kernel yang digunakan?
- Apakah waktu saat ini sudah benar?
- Sudah berapa lama sistem berjalan?

---

## Mari berpikir

Jawablah pertanyaan berikut dengan kata-kata Anda sendiri.

1. Informasi apa yang dapat diperiksa dengan `pwd`?
2. Informasi apa yang dapat diperiksa dengan `whoami`?
3. Informasi apa saja yang tertulis di `/etc/os-release`?
4. Apa perbedaan antara `uname -a` dan `/etc/os-release`?
5. Mengapa penting untuk memeriksa tanggal, waktu, dan uptime saat mengelola server?

---

## Poin penting bab ini

Di Linux, Anda dapat mengamati kondisi sistem dengan menggunakan perintah.

Hal yang penting bukan hanya menghafal nama perintah.

Anda juga perlu membaca keluaran teks dari perintah tersebut dan menjelaskan artinya.

Pembelajaran sistem komputer dimulai dari observasi.
