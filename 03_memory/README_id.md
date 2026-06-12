# 03 Mengamati Memori

## Tujuan bab ini

Dalam bab ini, Anda akan mengamati keadaan memori di Linux dan memahami bagaimana komputer menggunakan memori saat menjalankan program.

Dalam bab sebelumnya, Anda mempelajari tentang CPU dan proses.

Proses dieksekusi oleh CPU. Namun, proses tidak berjalan semata-mata pada CPU.

Saat program dieksekusi, program itu sendiri dan data yang sedang diproses ditempatkan pada memori.

Dengan kata lain, untuk memahami proses, Anda juga perlu memahami memori.

---

## Kata Kunci

- Memori
- RAM
- Proses
- Memori yang Digunakan
- Memori Bebas
- Buffer
- Cache
- Swap
- `/proc/meminfo`

---

## Apa itu Memori?

Memori adalah ruang kerja sementara untuk komputer.

Jika penyimpanan adalah "tempat untuk menyimpan jangka panjang," maka memori adalah "tempat untuk menyimpan apa yang sedang Anda gunakan."

Misalnya, saat Anda memulai aplikasi, program dimuat dari penyimpanan dan diperluas ke memori.

CPU memproses instruksi dan data yang ada di memori.

---

## Mari Kita Amati

Di Linux, Anda dapat memeriksa keadaan memori dengan perintah.

```bash
free -h
```

Perintah `free` menampilkan penggunaan memori dari seluruh sistem.

Saat Anda menambahkan opsi `-h`, ditampilkan dalam satuan yang mudah dibaca manusia.

---

## Representasi Data di Memori

Memori tidak hanya menyimpan program yang berjalan, tetapi juga data yang sedang diproses.

Data bisa berupa teks, bilangan bulat, bilangan desimal, gambar, suara, dan lain-lain.

Namun, di dalam komputer, semuanya direpresentasikan sebagai kombinasi 0 dan 1.

Sebagai contoh, bilangan bulat dan bilangan desimal direpresentasikan dengan cara yang berbeda di memori.

Nilai seperti berikut dapat direpresentasikan sebagai bilangan bulat.

```text
100
42
-7
```

Sementara itu,

```text
3.14
0.1
6.02 x 10^23
```

nilai seperti ini direpresentasikan sebagai bilangan floating-point.

Floating-point dapat dianggap sebagai notasi ilmiah versi biner.

Dalam notasi desimal, bilangan yang sangat besar bisa ditulis seperti ini:

```text
6.02 x 10^23
```

Di dalam komputer, idenya dinyatakan dalam biner:

```text
1.xxxxx x 2^n
```

Dengan cara ini, angka dibagi menjadi tiga bagian.

| Bagian | Makna |
| --- | --- |
| Tanda | Apakah bilangan positif atau negatif |
| Eksponen | Seberapa jauh titik desimal digeser |
| Mantisa | Bagian utama dari angka |

Contohnya, bilangan besar seperti `6.02 x 10^23` dapat dipandang secara perkiraan sebagai:

```text
6.02 x 10^23 ~= 1.xxxxx_2 x 2^78
```

Namun, jumlah bit yang tersedia di memori terbatas.

Karena itu, floating-point tidak selalu dapat menyimpan nilai secara persis.
Sering kali nilainya disimpan sebagai pendekatan terdekat.

Mari cek dengan Python.

```python
x = 6.02e23

print(x)
print(type(x))
```

`6.02e23` adalah cara penulisan Python untuk `6.02 x 10^23`.

Pada bab ini, Anda tidak perlu menghafal detail perhitungan floating-point.

Poin pentingnya adalah: data di memori direpresentasikan dengan 0 dan 1, dan bilangan bulat serta desimal memiliki representasi yang berbeda.

---

## Cara Membaca Perintah free

Saat Anda menjalankan `free -h`, item seperti berikut ditampilkan:

```text
              total        used        free      shared  buff/cache   available
Mem:          7.6Gi       1.2Gi       4.8Gi       100Mi       1.6Gi       6.0Gi
Swap:         2.0Gi          0B       2.0Gi
```

Poin-poin yang perlu diperhatikan adalah sebagai berikut:

| Item | Makna |
| --- | --- |
| total | Jumlah total memori |
| used | Jumlah memori yang sedang digunakan |
| free | Jumlah memori yang segera tersedia |
| buff/cache | Jumlah memori yang digunakan sebagai buffer dan cache |
| available | Jumlah memori yang dianggap praktis tersedia |
| swap | Area tambahan yang digunakan saat memori tidak cukup |

---

## Perbedaan Antara free dan available

Agak berisiko untuk menilai apakah ada memori yang cukup hanya dengan melihat nilai `free`.

Di Linux, memori bebas dimanfaatkan secara efektif sebagai cache.

Oleh karena itu, meskipun `free` tampak kecil, mungkin masih ada memori yang tersisa yang dapat digunakan kembali sesuai kebutuhan.

Di sinilah `available` menjadi penting.

`available` mewakili jumlah memori yang dapat digunakan oleh program baru dalam keadaan saat ini.

Saat memeriksa ketersediaan memori, perhatikan tidak hanya `free`, tetapi juga `available`.

---

## Melihat Informasi Memori yang Lebih Detail

Di Linux, informasi memori juga dapat diperiksa sebagai file teks.

```bash
cat /proc/meminfo
```

`/proc/meminfo` menampilkan informasi terperinci tentang memori.

Misalnya, berisi item seperti berikut:

```text
MemTotal
MemFree
MemAvailable
Buffers
Cached
SwapTotal
SwapFree
```

Di Linux, Anda dapat memeriksa keadaan sistem dari file virtual di bawah `/proc`.

Ini adalah konsep penting untuk mempelajari Linux.

---

## Melihat Penggunaan Memori per Proses

Memori digunakan oleh proses yang sedang berjalan.

Mari kita periksa proses mana yang menggunakan paling banyak memori.

```bash
ps aux --sort=-%mem | head
```

Perintah ini menampilkan proses dengan penggunaan memori tinggi dari atas.

Melihat kolom `%MEM`, Anda dapat melihat berapa banyak memori yang digunakan proses tersebut.

---

## Mengamati Secara Real-Time dengan top

Perintah `top` memungkinkan Anda memeriksa penggunaan CPU dan memori secara real-time.

```bash
top
```

Di layar `top`, informasi memori untuk seluruh sistem ditampilkan di bagian atas.

Anda juga dapat memeriksa penggunaan CPU dan memori dari setiap proses.

Saat keluar, tekan `q`.

---

## Memori dan Swap

Swap adalah mekanisme yang secara sementara menggunakan bagian dari penyimpanan sebagai pengganti memori saat memori tidak cukup.

Namun, karena penyimpanan lebih lambat dari memori, ketika swap digunakan secara ekstensif, kinerja sistem mungkin menjadi lambat.

Dengan `free -h`, Anda juga dapat memeriksa penggunaan swap.

```bash
free -h
```

Perhatikan baris `Swap`.

---

## Mari Kita Amati

Jalankan perintah berikut dan amati hasilnya.

```bash
free -h
```

```bash
cat /proc/meminfo | head
```

```bash
ps aux --sort=-%mem | head
```

```bash
top
```

---

## Misi

### Misi 1: Periksa Kapasitas Memori Lingkungan Anda

Jalankan `free -h` dan periksa jumlah total memori di lingkungan Anda.

Item yang perlu diperiksa:

- total
- used
- free
- available

---

### Misi 2: Jelaskan Perbedaan Antara free dan available

Jelaskan perbedaan antara `free` dan `available` dengan kata-kata Anda sendiri.

Contoh:

```text
free adalah jumlah memori yang segera tersedia, dan available adalah jumlah memori yang berpotensi dapat digunakan jika diperlukan.
```

---

### Misi 3: Amati /proc/meminfo

Jalankan perintah berikut:

```bash
cat /proc/meminfo | head
```

Dari item yang ditampilkan, pilih tiga yang tampaknya memiliki makna yang dapat dipahami dan jelaskan.

---

### Misi 4: Temukan Proses yang Menggunakan Banyak Memori

Jalankan perintah berikut:

```bash
ps aux --sort=-%mem | head
```

Dari proses yang ditampilkan, identifikasi yang memiliki penggunaan memori tinggi.

Item yang perlu diperiksa:

- USER
- PID
- %MEM
- COMMAND

---

### Misi 5: Pikirkan Tentang Hubungan Antara CPU dan Memori

Lengkapi kalimat berikut:

```text
Proses dieksekusi oleh CPU, tetapi program yang sedang berjalan dan data ditempatkan pada ________.
```

---

## Pikirkan Tentang Itu

Pikirkan tentang pertanyaan berikut dengan kata-kata Anda sendiri:

1. Apa perbedaan antara memori dan penyimpanan?
2. Mengapa memori digunakan saat program dieksekusi?
3. Mengapa Anda perlu memeriksa `available` daripada hanya `free`?
4. Mengapa sistem menjadi lambat ketika swap digunakan terlalu banyak?

---

## Ringkasan

Memori adalah ruang kerja sementara untuk komputer.

Proses dieksekusi oleh CPU, tetapi program yang sedang berjalan dan data ditempatkan pada memori.

Di Linux, Anda dapat mengamati keadaan memori menggunakan perintah seperti `free`, `top`, `ps`, dan `/proc/meminfo`.

Saat melihat memori, bukan sekadar menghafal angka,

- Apa yang menggunakan memori?
- Berapa banyak ruang yang tersisa?
- Bagaimana proses dan memori terkait?

Penting untuk mengamati aspek-aspek ini.

Dalam bab berikutnya, Anda akan mempelajari tentang penyimpanan dan sistem file sebagai lawan dari memori.
