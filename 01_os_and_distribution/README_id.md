# 01_os_and_distribution

## Tujuan bab ini

Pada bab ini, Anda akan memeriksa perbedaan antara **OS**, **kernel Linux**, dan **distribusi** di lingkungan Linux.

Dalam pembelajaran sistem komputer, istilah "OS" sering muncul.
Namun, saat menggunakan Linux, Anda perlu memahami perbedaan antara istilah berikut:

* OS
* Linux
* Kernel Linux
* Distribusi
* Versi
* Arsitektur

Pada bab ini, Anda tidak hanya menghafal istilah-istilah tersebut.
Anda akan menjalankan perintah di lingkungan Linux nyata dan memahaminya dengan membaca informasi yang ditampilkan.

---

## Alur pembelajaran

Pada bab ini, Anda akan:

1. Memeriksa apa itu OS
2. Memeriksa apa itu kernel Linux
3. Memeriksa apa itu distribusi
4. Memeriksa apa itu shell
5. Membaca `/etc/os-release` untuk memeriksa informasi OS
6. Menggunakan `uname` untuk memeriksa informasi kernel
7. Memeriksa perbedaan antara `/etc/os-release` dan `uname`
8. Memikirkan perbedaan antara AlmaLinux dan Ubuntu
9. Menjalankan perintah pemeriksaan dan merangkum informasi lingkungan
10. Menjelaskan informasi yang telah diperiksa dengan kata-kata sendiri

---

## 1. Apa itu OS

OS adalah singkatan dari Operating System.

OS adalah perangkat lunak dasar yang berada di antara perangkat keras komputer dan aplikasi, serta mengelola seluruh komputer.

Sebagai contoh, OS mengelola:

* CPU
* Memori
* Penyimpanan
* Berkas
* Proses
* Pengguna
* Jaringan
* Perangkat input/output

Windows, macOS, dan Linux adalah contoh OS.

Mempelajari Linux bukan hanya menghafal perintah.
Ini juga tentang mengamati bagaimana OS mengelola komputer.

---

## 2. Apa itu kernel Linux

Secara ketat, kata Linux merujuk pada **kernel Linux**.

Kernel adalah bagian inti dari OS.
Kernel mengelola bagian yang dekat dengan perangkat keras dan memungkinkan aplikasi maupun perintah menggunakan komputer dengan aman.

Sebagai contoh, kernel memiliki peran berikut:

* Manajemen proses
* Manajemen memori
* Manajemen sistem berkas
* Manajemen perangkat
* Manajemen komunikasi jaringan

"Linux" yang biasa kita gunakan sehari-hari bukan hanya kernel.
Linux adalah gabungan kernel, perintah, pustaka, sistem manajemen paket, berkas konfigurasi, dan lain-lain.

---

## 3. Apa itu distribusi

**Distribusi Linux** adalah paket yang menggabungkan kernel Linux dengan berbagai perangkat lunak dan alat manajemen dalam bentuk yang mudah digunakan.

Contoh distribusi yang umum:

* Ubuntu
* Debian
* AlmaLinux
* Rocky Linux
* Fedora
* Arch Linux

Meskipun sama-sama Linux, setiap distribusi memiliki perbedaan.

Contohnya, perintah manajemen paket bisa berbeda.

| Keluarga | Contoh | Manajemen paket |
| --- | --- | --- |
| Keluarga Debian | Ubuntu, Debian | `apt` |
| Keluarga Red Hat | AlmaLinux, Rocky Linux, Fedora | `dnf`, `yum` |

Karena itu, saat menggunakan Linux, penting untuk memeriksa bukan hanya bahwa itu Linux, tetapi juga **distribusi apa yang digunakan**.

---

## 4. Apa itu shell

Saat mengoperasikan Linux, kita sering mengetik perintah di terminal.

Pada saat itu, program yang menerima input pengguna, menafsirkannya, lalu meminta OS menjalankan proses disebut **shell**.

Shell adalah antarmuka di antara pengguna dan OS.

```text
Pengguna
-> Shell
-> OS / Kernel
-> Perangkat keras
```

Sebagai contoh, misalkan Anda mengetik perintah berikut:

```bash
ls
```

Shell menafsirkan input `ls` dan menjalankan program yang sesuai.
Hasilnya, daftar berkas dan direktori pada lokasi saat ini akan ditampilkan.

---

### Jenis-jenis shell

Di Linux, ada beberapa jenis shell.

Contoh yang umum adalah:

| Shell | Penjelasan |
| --- | --- |
| `sh` | Shell Unix dasar |
| `bash` | Shell yang paling umum dipakai di banyak lingkungan Linux |
| `zsh` | Shell dengan fitur pelengkapan yang lebih kuat |
| `fish` | Shell yang berfokus pada kemudahan penggunaan |

Dalam kelas atau materi pembelajaran, `bash` biasanya paling sering digunakan.

Anda bisa memeriksa shell yang sedang dipakai dengan:

```bash
echo $SHELL
```

Contoh keluaran:

```text
/bin/bash
```

Anda juga bisa memeriksa proses shell yang sedang berjalan dengan:

```bash
ps
```

Contoh keluaran:

```text
	PID TTY          TIME CMD
 1234 pts/0    00:00:00 bash
 1250 pts/0    00:00:00 ps
```

Dari contoh ini, kita bisa melihat bahwa shell yang berjalan adalah `bash`.

---

### Shell dan input perintah

Shell tidak hanya menjalankan perintah.

Shell juga memiliki fungsi seperti:

* Menafsirkan perintah
* Mengelola variabel
* Menghubungkan perintah dengan pipe `|`
* Mengalihkan keluaran dengan `>` dan `>>`
* Menjalankan shell script
* Menyimpan riwayat perintah

Artinya, sebagian besar operasi baris perintah di Linux dilakukan melalui shell.

---

### Hubungan OS, kernel, dan shell

Hubungan OS, kernel, dan shell dapat diringkas sebagai berikut:

| Istilah | Peran |
| --- | --- |
| Kernel | Inti OS yang mengelola bagian dekat perangkat keras |
| Distribusi | Paket kernel Linux beserta berbagai perangkat lunak |
| Shell | Program yang menerima perintah pengguna dan meminta OS memprosesnya |
| Terminal | Layar/aplikasi untuk mengoperasikan shell |

Hal penting yang perlu diingat adalah **terminal dan shell bukan hal yang sama**.

Terminal adalah layar untuk mengetik dan menampilkan teks.
Shell adalah program penafsir perintah yang berjalan di dalamnya.

```text
Terminal
-> Layar untuk mengoperasikan shell

Shell
-> Program yang menafsirkan dan menjalankan perintah
```

Dengan memahami perbedaan ini, Anda dapat menjelaskan operasi Linux dengan lebih tepat.

---

## 5. Memeriksa informasi OS

Di lingkungan Linux, informasi OS dan distribusi dapat diperiksa melalui `/etc/os-release`.

```bash
cat /etc/os-release
```

Contoh keluaran:

```text
NAME="AlmaLinux"
VERSION="9.5 (Teal Serval)"
ID="almalinux"
VERSION_ID="9.5"
PLATFORM_ID="platform:el9"
PRETTY_NAME="AlmaLinux 9.5 (Teal Serval)"
```

Bagian penting yang perlu diperiksa:

| Item | Arti |
| --- | --- |
| `NAME` | Nama distribusi |
| `VERSION` | Nama versi |
| `ID` | Identitas internal yang digunakan sistem |
| `VERSION_ID` | Nomor versi |
| `PRETTY_NAME` | Nama tampilan yang mudah dibaca manusia |

Dari sini, Anda dapat mengetahui jenis Linux yang digunakan.

---

## 6. Memeriksa informasi kernel

Selanjutnya, periksa informasi kernel.

```bash
uname -a
```

Contoh keluaran:

```text
Linux localhost.localdomain 5.14.0-503.el9.x86_64 #1 SMP PREEMPT_DYNAMIC x86_64 GNU/Linux
```

Hasil ini memuat informasi seperti:

| Informasi | Arti |
| --- | --- |
| `Linux` | Nama kernel |
| `localhost.localdomain` | Hostname |
| `5.14.0-503.el9.x86_64` | Versi kernel |
| `x86_64` | Arsitektur CPU |
| `GNU/Linux` | Informasi yang menunjukkan jenis OS |

Jika ingin melihat lebih singkat, Anda juga bisa menggunakan perintah berikut.

```bash
uname -r
```

Perintah ini hanya menampilkan versi kernel.

```bash
uname -m
```

Perintah ini menampilkan arsitektur mesin.

---

## 7. Perbedaan `/etc/os-release` dan `uname`

`/etc/os-release` dan `uname` sama-sama digunakan untuk memeriksa informasi sistem.
Namun, jenis informasi yang dilihat berbeda.

| Perintah / berkas | Informasi yang dilihat |
| --- | --- |
| `cat /etc/os-release` | Informasi distribusi |
| `uname -a` | Informasi kernel |
| `uname -r` | Versi kernel |
| `uname -m` | Arsitektur CPU |

Artinya dapat diringkas seperti berikut.

```text
/etc/os-release
-> Memeriksa distribusi Linux yang digunakan

uname
-> Memeriksa kernel yang sedang berjalan
```

Dengan memahami perbedaan ini, Anda dapat menggunakan istilah "Linux" dengan lebih tepat.

---

## 8. Memikirkan perbedaan AlmaLinux dan Ubuntu

AlmaLinux dan Ubuntu sama-sama distribusi Linux.
Namun, ada perbedaan pada keluarga dan konteks penggunaannya.

| Item | AlmaLinux | Ubuntu |
| --- | --- | --- |
| Keluarga | Keluarga Red Hat | Keluarga Debian |
| Manajemen paket | `dnf` | `apt` |
| Penggunaan umum | Server, sistem perusahaan | Server, desktop, lingkungan belajar |
| Gaya konfigurasi | Gaya Red Hat | Gaya Debian |

Walaupun sama-sama Linux, perintah dan metode konfigurasi bisa berbeda tergantung lingkungan.

Karena itu, saat membaca materi atau artikel web, Anda perlu memperhatikan:

* Distribusi apa yang menjadi asumsi penjelasan
* Apakah perintah yang sama bisa dijalankan di lingkungan Anda
* Apakah manajemen paketnya `apt` atau `dnf`
* Apakah lokasi berkas konfigurasinya sama

---

## 9. Coba jalankan

Jalankan perintah berikut, lalu periksa hasilnya.

```bash
cat /etc/os-release
uname -a
uname -r
uname -m
hostnamectl
```

Dengan `hostnamectl`, Anda juga bisa memeriksa informasi OS, kernel, dan arsitektur sekaligus.

---

## 10. Catatan observasi

Berdasarkan hasil perintah, isi tabel berikut.

| Item | Lingkungan Anda |
| --- | --- |
| Nama distribusi | |
| Versi | |
| ID | |
| Versi kernel | |
| Arsitektur | |
| Hostname | |
| Perintah manajemen paket | |

---

## Mari berpikir

Jawab pertanyaan berikut dengan kata-kata Anda sendiri.

1. OS adalah perangkat lunak seperti apa, dan apa yang dikelolanya?
2. Apa itu kernel Linux?
3. Apa itu distribusi Linux?
4. Apa yang bisa diperiksa melalui `/etc/os-release`?
5. Apa yang bisa diperiksa melalui `uname -a`?
6. Apa perbedaan antara AlmaLinux dan Ubuntu?
7. Mengapa perbedaan distribusi perlu diperhatikan saat membaca artikel web atau materi belajar?

---

## Hal penting pada bab ini

Saat menggunakan Linux, penting untuk tidak menilai lingkungan hanya dengan satu kata "Linux".

Walaupun sama-sama Linux, distribusi, versi, kernel, dan metode manajemen paket dapat berbeda.

Yang penting adalah mengamati lingkungan Anda terlebih dahulu, lalu mampu menjelaskan OS, distribusi, dan kernel yang sedang digunakan.

Dalam pembelajaran sistem komputer, bukan hanya menghafal istilah yang penting.
Kemampuan membaca informasi dari lingkungan nyata juga sangat penting.