# Penjadwalan CPU (Chapter 5)

## 🔍 Studi Kasus Singkat

Contoh data proses:

```
Proses | Kedatangan | Burst | Prioritas
-------|------------|--------|----------
P1     |     0      |   4    |    2
P2     |     1      |   3    |    1
P3     |     2      |   1    |    3
```

## ⚙️ Algoritma yang Digunakan: Penjadwalan Prioritas Preemptive

* **Prioritas lebih tinggi = angka lebih kecil.**
* Proses dengan prioritas tertinggi akan dijalankan.
* Jika proses baru masuk dan memiliki prioritas lebih tinggi, proses yang sedang berjalan akan dihentikan (preempted).

## 🧠 Penjelasan Konsep (dari Dokumen Resmi)

Berikut adalah penjelasan ringkas dari algoritma-algoritma penjadwalan CPU yang dijelaskan dalam Chapter 5:

### 🔹 FCFS (First Come First Serve)

* Proses yang datang lebih dulu akan dijalankan lebih dulu.
* Non-preemptive: proses tidak bisa dihentikan sampai selesai.
* Sederhana tapi bisa menyebabkan waktu tunggu lama jika ada proses dengan burst time besar di awal.

**Contoh:**

```
Proses | Kedatangan | Burst
P1     |     0      |   5
P2     |     1      |   2
P3     |     2      |   1
```

Gantt Chart: P1 | P2 | P3

### 🔹 SJF (Shortest Job First)

* Proses dengan burst time paling kecil dijalankan lebih dulu.
* Bisa preemptive (Shortest Remaining Time First) atau non-preemptive.
* Efisien untuk waktu tunggu rata-rata terendah, tapi bisa menyebabkan starvation.

**Contoh:**

```
Proses | Kedatangan | Burst
P1     |     0      |   8
P2     |     1      |   4
P3     |     2      |   2
```

Gantt Chart (preemptive): P1 | P2 | P3

### 🔹 Round Robin

* Setiap proses mendapat waktu eksekusi tertentu (time quantum), bergiliran.
* Cocok untuk sistem multitasking dan time-sharing.
* Preemptive secara otomatis setelah time quantum habis.

**Contoh (quantum = 2):**

```
Proses | Kedatangan | Burst
P1     |     0      |   5
P2     |     1      |   3
```

Gantt Chart: P1(2) | P2(2) | P1(2) | P2(1) | P1(1)

### 🔹 Priority Scheduling

* Proses dipilih berdasarkan prioritas.
* Bisa preemptive atau non-preemptive.
* Jika dua proses memiliki prioritas sama, bisa gunakan FCFS.

**Preemptive:** Proses baru dengan prioritas lebih tinggi bisa menghentikan proses yang sedang berjalan.
**Non-preemptive:** Proses saat ini akan selesai dulu baru proses berikutnya dijalankan.

**Contoh:**

```
Proses | Kedatangan | Burst | Prioritas
P1     |     0      |   4   |    2
P2     |     1      |   3   |    1
```

Gantt Chart Preemptive: P1 | P2 | P1

Dalam bab ini dibahas berbagai jenis algoritma penjadwalan, termasuk:

* **FCFS (First Come First Serve)**
* **SJF (Shortest Job First)**
* **Round Robin**
* **Priority Scheduling (Preemptive dan Non-preemptive)**

Konsep utama penjadwalan mencakup:

* Menentukan proses mana yang siap untuk dieksekusi
* Mengatur urutan eksekusi agar waktu tunggu dan waktu rata-rata minimum
* Menghindari starvation dengan teknik seperti aging (menaikkan prioritas jika proses terlalu lama menunggu)

## 🧰 Alur Logika Program (Flow Logic)

### 1. Input

* Jumlah proses
* Untuk setiap proses:

  * Waktu kedatangan (arrival time)
  * Lama proses dijalankan (burst time)
  * Prioritas

### 2. Proses Pemilihan

* Per satuan waktu (misal setiap 1 detik):

  * Lihat semua proses yang sudah datang (arrival time <= current time)
  * Di antara proses tersebut, pilih yang memiliki prioritas tertinggi
  * Jika proses baru dengan prioritas lebih tinggi muncul, lakukan **preemptive switching**

### 3. Eksekusi Proses

* Jalankan proses yang terpilih selama 1 satuan waktu
* Kurangi burst time-nya
* Jika burst time mencapai 0, proses dianggap selesai dan dicatat waktu selesainya

### 4. Perhitungan Waktu Penting

* **Waktu Selesai** = waktu saat proses selesai dieksekusi
* **Turnaround Time (TAT)** = waktu selesai - waktu datang
* **Waiting Time (WT)** = TAT - burst time awal

### 5. Output

* Tabel berisi proses, waktu selesai, TAT, dan WT
* Hitung rata-rata TAT dan WT

## 🧮 Perhitungan dan Gantt Chart

### Urutan Eksekusi (dengan preemptive priority):

* Waktu 0: P1 mulai (prioritas 2)
* Waktu 1: P2 datang (prioritas 1), P1 dipreempt
* Waktu 1-4: P2 jalan hingga selesai
* Waktu 4: P1 lanjutkan sisa 3 burst
* Waktu 7: P1 selesai
* Waktu 7: P3 mulai
* Waktu 8: P3 selesai

### Gantt Chart

```
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|
| P1| P2| P2| P2| P1| P1| P1| P3|   |
```

### Tabel Hasil Akhir

```
Proses | Arrival | Burst | Prioritas | Finish | Turnaround | Waiting
-------|---------|-------|-----------|--------|-------------|--------
P1     |   0     |   4   |     2     |   7    |     7       |   3
P2     |   1     |   3   |     1     |   4    |     3       |   0
P3     |   2     |   1   |     3     |   8    |     6       |   5
```

### Rata-rata

* **Avg Turnaround Time** = (7 + 3 + 6) / 3 = 5.33
* **Avg Waiting Time** = (3 + 0 + 5) / 3 = 2.67

