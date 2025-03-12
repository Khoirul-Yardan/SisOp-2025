# Resume Sistem Operasi 1.34 proses management - 1.40 caching

## Daftar Isi
- [Transisi User ke Kernel Mode](#transisi-user-ke-kernel-mode)
- [Manajemen Proses](#manajemen-proses)
- [Aktivitas Manajemen Proses](#aktivitas-manajemen-proses)
- [Manajemen Memori](#manajemen-memori)
- [Manajemen File-System](#manajemen-file-system)
- [Manajemen Mass-Storage](#manajemen-mass-storage)
- [Caching](#caching)

## Transisi User ke Kernel Mode
Sistem operasi menggunakan mekanisme timer untuk mencegah program mengkonsumsi sumber daya CPU secara berlebihan:

- **Timer** digunakan untuk mencegah loop tak terbatas atau proses yang menghabiskan sumber daya
- Timer diatur untuk menginterupsi komputer setelah periode waktu tertentu
- **Keep counter** adalah penghitung yang dikendalikan oleh physical clock
- Sistem operasi menetapkan counter (instruksi istimewa)
- Saat counter mencapai nol, terjadi interrupt
- Program dibatasi sebelum proses penjadwalan untuk mencegah program melebihi waktu yang dialokasikan

## Manajemen Proses
Proses adalah konsep fundamental dalam sistem operasi modern:

- **Proses** adalah program yang sedang dieksekusi, merupakan unit kerja dalam sistem
- **Program** adalah entitas pasif, sedangkan **proses** adalah entitas aktif
- Proses membutuhkan sumber daya untuk menyelesaikan tugasnya:
  - CPU
  - Memori
  - I/O
  - Berkas
- Terminasi proses memerlukan pengembalian sumber daya yang dapat digunakan kembali
- **Single-threaded**: proses memiliki satu program counter yang menentukan lokasi instruksi berikutnya
- Proses mengeksekusi instruksi secara berurutan sampai selesai
- **Multi-threaded**: proses memiliki beberapa counter program
- Sistem biasanya memiliki banyak proses, beberapa milik pengguna, dan beberapa milik sistem operasi
- **Konkurensi** dicapai dengan multiplexing CPU di antara proses/thread

## Aktivitas Manajemen Proses
Sistem operasi bertanggung jawab untuk kegiatan manajemen proses, meliputi:

- Membuat dan menghapus proses pengguna dan sistem
- Menunda dan melanjutkan proses
- Menyediakan mekanisme untuk sinkronisasi proses
- Menyediakan mekanisme untuk komunikasi antar proses
- Menyediakan mekanisme untuk penanganan deadlock

## Manajemen Memori
Memori adalah komponen penting yang harus dikelola dengan efisien:

- Untuk mengeksekusi program, semua (atau sebagian) instruksi harus berada di memori
- Semua (atau sebagian) data yang dibutuhkan program harus berada di memori
- Manajemen memori menentukan apa yang ada di memori dan kapan
- Tujuannya mengoptimalkan penggunaan CPU dan respon komputer terhadap pengguna
- Aktivitas manajemen memori meliputi:
  - Melacak bagian memori yang sedang digunakan dan oleh siapa
  - Memutuskan proses mana (atau bagian) yang dipindahkan ke dan dari memori
  - Alokasi dan dealokasi ruang memori sesuai kebutuhan

## Manajemen File-System
File system menyediakan abstraksi untuk penyimpanan data:

- OS menyediakan tampilan logis yang seragam dari penyimpanan informasi
- Abstraksi properti fisik ke unit penyimpanan logis: file
- Setiap media dikendalikan oleh perangkat (disk, tape drive)
- Properti bervariasi termasuk kecepatan akses, kapasitas, metode transfer
- Files biasanya diatur dalam direktori
- Akses kontrol pada sistem menentukan siapa yang dapat mengakses file
- Aktivitas OS meliputi:
  - Membuat dan menghapus file dan direktori
  - Primitif untuk memanipulasi file dan direktori
  - Memetakan file ke penyimpanan sekunder
  - Backup file ke media penyimpanan stabil (non-volatile)

## Manajemen Mass-Storage
Penyimpanan massal (seperti hard disk) memerlukan manajemen yang efisien:

- Disk biasanya digunakan untuk menyimpan data yang tidak disimpan di memori utama
- Data harus disimpan untuk waktu yang lama
- Aktivitas OS meliputi:
  - Pemasangan dan pelepasan
  - Manajemen ruang bebas
  - Alokasi penyimpanan
  - Penjadwalan disk
  - Partisi dan Proteksi
- Beberapa jenis penyimpanan:
  - Penyimpanan tersier: penyimpanan optik, tape magnetik
  - Masih harus dikelola oleh OS atau aplikasi

## Caching
Caching adalah teknik untuk meningkatkan kinerja sistem:

- Prinsip penting, dilakukan di banyak level komputer (hardware, OS, software)
- Informasi yang sering digunakan disalin dari penyimpanan lambat ke penyimpanan lebih cepat secara sementara
- Penyimpanan lebih cepat (cache) diperiksa terlebih dahulu untuk menentukan apakah informasi ada di sana
- Jika ada, informasi digunakan langsung dari cache
- Jika tidak, data disalin ke cache untuk digunakan nanti
- Cache lebih kecil dari penyimpanan yang di-cache
- Manajemen cache merupakan masalah desain penting
- Kebijakan ukuran dan penggantian cache sangat mempengaruhi kinerja

---

**Oleh:** [Khoirul Yardan Mauluddin Zhorif 3124521022 TI A PSDKU LA]