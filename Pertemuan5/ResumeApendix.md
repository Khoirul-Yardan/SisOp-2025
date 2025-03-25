# Resume Appendix A: Operating System Concepts

## Pendahuluan
Appendix A dari buku *Operating System Concepts* membahas dasar-dasar arsitektur komputer yang menjadi fondasi bagi sistem operasi modern. Topik yang dibahas meliputi struktur perangkat keras, manajemen memori, serta konsep fundamental terkait pengoperasian komputer dan bagaimana sistem operasi berinteraksi dengan komponen-komponen tersebut.

## 1. Struktur Perangkat Keras
Sistem komputer terdiri dari beberapa komponen utama yang bekerja bersama untuk menjalankan instruksi program:
- **CPU (Central Processing Unit)**: Bertanggung jawab untuk mengeksekusi instruksi. CPU terdiri dari beberapa unit penting, yaitu:
  - **Unit Kontrol (CU - Control Unit)**: Mengontrol aliran data dalam sistem komputer.
  - **Unit Aritmetika dan Logika (ALU - Arithmetic Logic Unit)**: Melakukan operasi aritmetika dan logika.
  - **Register**: Penyimpanan kecil dalam CPU untuk data sementara yang sedang diproses.
  - **Cache Memory**: Penyimpanan data berkecepatan tinggi untuk mempercepat eksekusi instruksi.
- **Memori Utama**: Digunakan untuk menyimpan data dan instruksi yang sedang diproses oleh CPU.
- **Penyimpanan Sekunder**: Seperti Hard Disk Drive (HDD) dan Solid State Drive (SSD) untuk penyimpanan data jangka panjang.
- **Perangkat Input/Output (I/O)**: Termasuk keyboard, mouse, printer, layar, dan perangkat jaringan untuk interaksi dengan pengguna dan komunikasi antar sistem.
- **Interkoneksi Sistem**: Menghubungkan CPU, memori, dan perangkat I/O melalui bus data, bus alamat, dan bus kontrol.

## 2. Siklus Instruksi dan Mode Operasi
CPU menjalankan instruksi dalam siklus berikut:
- **Fetch**: Mengambil instruksi dari memori utama.
- **Decode**: Menguraikan instruksi agar dapat dieksekusi.
- **Execute**: Menjalankan instruksi yang telah didekodekan.
- **Write-back**: Menyimpan hasil eksekusi ke dalam register atau memori utama.

Sistem operasi mendukung dua mode eksekusi untuk memastikan keamanan dan stabilitas:
- **Mode Kernel**: Memiliki akses penuh ke perangkat keras dan dapat menjalankan instruksi sistem.
- **Mode Pengguna**: Memiliki akses terbatas, digunakan oleh aplikasi agar tidak mengganggu sistem secara langsung.

## 3. Manajemen Memori
Memori utama berperan penting dalam eksekusi program. Sistem operasi bertanggung jawab atas pengalokasian dan pengelolaan memori dengan teknik berikut:
- **Paging**: Memori dibagi ke dalam halaman kecil dengan ukuran tetap agar penggunaan lebih efisien.
- **Segmentation**: Memori dibagi menjadi segmen yang lebih besar berdasarkan logika program, seperti kode program, data, dan stack.
- **Virtual Memory**: Memungkinkan sistem menggunakan penyimpanan sekunder sebagai perpanjangan dari memori utama untuk menjalankan program lebih besar dari kapasitas RAM.
- **Memory Protection**: Sistem operasi mencegah program mengakses memori yang bukan miliknya untuk menghindari konflik dan kerusakan data.

## 4. Organisasi dan Hierarki Penyimpanan
Hierarki penyimpanan komputer dirancang untuk menyeimbangkan kecepatan, kapasitas, dan biaya:
- **Register**: Penyimpanan tercepat dalam CPU, berukuran kecil dan digunakan untuk operasi langsung.
- **Cache Memory**: Menyimpan data yang sering diakses untuk mempercepat eksekusi.
- **Memori Utama (RAM)**: Menyimpan data dan program yang sedang dieksekusi.
- **Penyimpanan Sekunder (HDD/SSD)**: Digunakan untuk penyimpanan jangka panjang.
- **Penyimpanan Tersier (Optical Disk, Tape Drive)**: Digunakan untuk arsip dan pencadangan data.

## 5. Manajemen Input/Output (I/O)
Operasi I/O dikelola oleh sistem operasi menggunakan berbagai metode untuk meningkatkan efisiensi dan mengurangi beban CPU:
- **Polling**: CPU secara aktif mengecek status perangkat I/O dalam loop.
- **Interrupts**: Perangkat mengirim sinyal ke CPU untuk meminta perhatian tanpa harus terus-menerus diperiksa.
- **Direct Memory Access (DMA)**: Memungkinkan perangkat I/O mengakses memori utama langsung tanpa intervensi CPU, mempercepat transfer data.
- **Buffering dan Spooling**:
  - **Buffering**: Menyimpan sementara data sebelum dikirim ke perangkat I/O.
  - **Spooling**: Mengantrekan data I/O untuk diproses secara efisien, sering digunakan dalam pencetakan.

## 6. Manajemen Proses dan Penjadwalan
Sistem operasi bertanggung jawab dalam mengatur proses yang berjalan:
- **PCB (Process Control Block)**: Struktur data yang menyimpan informasi setiap proses.
- **Penjadwalan CPU**: Menentukan proses mana yang akan dieksekusi selanjutnya berdasarkan algoritma seperti:
  - **FCFS (First Come First Serve)**: Proses dieksekusi sesuai urutan kedatangan.
  - **SJF (Shortest Job First)**: Proses dengan waktu eksekusi terpendek dieksekusi lebih dahulu.
  - **Round Robin**: Setiap proses mendapat jatah waktu eksekusi bergilir.

## Kesimpulan
Appendix A memberikan pemahaman dasar mengenai arsitektur komputer dan bagaimana sistem operasi mengelola berbagai komponen perangkat keras untuk menjalankan program dengan efisien. Pemahaman ini sangat penting bagi pengembang sistem operasi serta pengguna yang ingin memahami bagaimana komputer bekerja secara mendasar.

**Oleh:** [Khoirul Yardan Mauluddin Zhorif 3124521022 TI A PSDKU LA]