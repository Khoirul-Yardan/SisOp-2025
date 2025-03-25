# BenchUtil

**Program untuk mengukur kemampuan CPU dalam satuan IOPS dan FLOPS.**

## Build Binaries
```sh
$ make
```
*Perintah `make` akan menjalankan proses kompilasi menggunakan Makefile untuk menghasilkan binary eksekusi utama.*

## Cleaning Old Build
```sh
$ make clean
```
*Perintah `make clean` akan menghapus file objek (`.o`) dan binary eksekusi untuk memastikan kompilasi ulang tanpa konflik dari build sebelumnya.*

## Install Binaries
```sh
$ sudo make install
```
*Perintah ini akan menyalin binary yang telah dikompilasi ke direktori sistem agar dapat diakses secara global.*

## Uninstall Binaries
```sh
$ sudo make uninstall
```
*Perintah ini akan menghapus binary yang telah diinstal dari sistem.*

## Usage
```sh
$ ./bench -i
```
*Menjalankan benchmark untuk IOPS (Input/Output Operations Per Second).*

```sh
$ ./bench -f
```
*Menjalankan benchmark untuk FLOPS (Floating Point Operations Per Second).*

```sh
$ ./bench -h
```
*Menampilkan bantuan terkait penggunaan program.*

## CPU yang diuji
```sh
CPU: Intel(R) Core(TM) i7-8550U CPU @ 1.80GHz
```

## Interpretasi Output
### 1. Hasil Pengukuran IOPS
```sh
$ ./bench -i
```
Output:
```sh
Integer operations per second: 2.79e+09
```
*Ini menunjukkan bahwa CPU mampu menangani sekitar **2.79 miliar operasi integer per detik**. Semakin tinggi nilai ini, semakin baik performa CPU dalam menangani operasi integer seperti perhitungan aritmetika sederhana.*

### 2. Hasil Pengukuran FLOPS
```sh
$ ./bench -f
```
Output:
```sh
Floating point operations per second: 1.94e+09
```
*Ini berarti CPU dapat menangani sekitar **1.94 miliar operasi floating-point per detik**. FLOPS sering digunakan untuk mengukur kinerja dalam komputasi ilmiah dan pemrosesan grafis.*

## Analisis Makefile
Makefile digunakan untuk menyederhanakan proses kompilasi. Berikut beberapa bagian penting:

1. **Target `all`**
   ```make
   all: bench
   ```
   - Menentukan bahwa target utama adalah `bench`.
   - Akan menjalankan proses kompilasi jika binary `bench` belum tersedia.

2. **Kompilasi Binary**
   ```make
   bench: bench.o
   	gcc -o bench bench.o -lm
   ```
   - Menggunakan `gcc` untuk menghasilkan file eksekusi `bench` dari `bench.o`.
   - `-lm` diperlukan untuk menghubungkan pustaka matematika.

3. **Membersihkan Build Lama**
   ```make
   clean:
   	rm -f bench bench.o
   ```
   - Menghapus file binary dan file objek lama.

4. **Instalasi dan Uninstalasi**
   ```make
   install:
   	cp bench /usr/local/bin/
   ```
   - Menyalin binary ke direktori `/usr/local/bin/` agar dapat dijalankan dari mana saja.

   ```make
   uninstall:
   	rm -f /usr/local/bin/bench
   ```
   - Menghapus file binary dari sistem.

## Kesimpulan
Makefile mempermudah proses kompilasi dan instalasi, sedangkan output program menunjukkan performa CPU dalam menangani operasi integer dan floating-point. Nilai yang lebih tinggi berarti performa CPU lebih baik dalam menangani tugas-tugas tersebut.

**Oleh:** [Khoirul Yardan Mauluddin Zhorif 3124521022 TI A PSDKU LA]