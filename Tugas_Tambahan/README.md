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

**Gantt Chart (Non Preemtive):**

```
| P1 | P2 | P3 |
|----|----|----|
| 0  | 5  | 7  | 8
```

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

**Gantt Chart (Preemtive):**

```
| P1 | P3 | P2 | P1 |
|----|----|----|----|
| 0  | 2  | 4  | 8  | 16
```

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

**Gantt Chart (Non Preemtive):**

```
| P1(2) | P2(2) | P1(2) | P2(1) | P1(1) |
|------|------|------|------|------|
| 0    | 2    | 4    | 6    | 7    | 8
```

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

**Gantt Chart (Preemtive):**

```
| P1 | P2 | P2 | P2 | P1 | P1 | P1 |
|----|----|----|----|----|----|----|
| 0  | 1  | 2  | 3  | 4  | 5  | 6  | 7
```

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


## 💻 Implementasi dalam Bahasa C

```c
#include <stdio.h>

#define MAX 10

typedef struct {
    int id, arrival, burst, remaining, priority;
    int finish, turnaround, waiting;
} Process;

int main() {
    Process p[3] = {
        {1, 0, 4, 4, 2},
        {2, 1, 3, 3, 1},
        {3, 2, 1, 1, 3}
    };

    int time = 0, completed = 0;
    int n = 3;

    while (completed < n) {
        int highest = -1;
        for (int i = 0; i < n; i++) {
            if (p[i].arrival <= time && p[i].remaining > 0) {
                if (highest == -1 || p[i].priority < p[highest].priority) {
                    highest = i;
                }
            }
        }

        if (highest != -1) {
            p[highest].remaining--;
            if (p[highest].remaining == 0) {
                p[highest].finish = time + 1;
                completed++;
            }
        }
        time++;
    }

    float totalTAT = 0, totalWT = 0;

    printf("Proses | Arrival | Burst | Priority | Finish | TAT | WT\n");
    for (int i = 0; i < n; i++) {
        p[i].turnaround = p[i].finish - p[i].arrival;
        p[i].waiting = p[i].turnaround - p[i].burst;
        totalTAT += p[i].turnaround;
        totalWT += p[i].waiting;
        printf("P%d     |   %d      |   %d   |    %d     |   %d    |  %d  | %d\n",
               p[i].id, p[i].arrival, p[i].burst, p[i].priority,
               p[i].finish, p[i].turnaround, p[i].waiting);
    }

    printf("\nAverage TAT: %.2f\n", totalTAT / n);
    printf("Average WT : %.2f\n", totalWT / n);

    return 0;
}
```

---

##  Penjelasan Singkat Kode C

### 1. Import dan Konstanta

```c
#include <stdio.h>
#define MAX 10
```

* Menggunakan `stdio.h` untuk input/output.
* `MAX` disiapkan untuk batas array proses (opsional).

### 2. Struktur Proses

```c
typedef struct {
    int id, arrival, burst, remaining, priority;
    int finish, turnaround, waiting;
} Process;
```

* Menyimpan semua data dan waktu penting dari proses.

### 3. Data Proses

```c
Process p[3] = {
    {1, 0, 4, 4, 2},
    {2, 1, 3, 3, 1},
    {3, 2, 1, 1, 3}
};
```

* Contoh proses:

  * P1: datang di 0, burst 4, prioritas 2
  * P2: datang di 1, burst 3, prioritas 1
  * P3: datang di 2, burst 1, prioritas 3

### 4. Simulasi Eksekusi

```c
int time = 0, completed = 0;
int n = 3;
```

* `time`: waktu berjalan.
* `completed`: jumlah proses selesai.

### 5. Loop Utama

```c
while (completed < n) {
    int highest = -1;
    for (int i = 0; i < n; i++) {
        if (p[i].arrival <= time && p[i].remaining > 0) {
            if (highest == -1 || p[i].priority < p[highest].priority)
                highest = i;
        }
    }
```

* Pilih proses dengan prioritas tertinggi yang sudah datang.

```c
    if (highest != -1) {
        p[highest].remaining--;
        if (p[highest].remaining == 0) {
            p[highest].finish = time + 1;
            completed++;
        }
    }
    time++;
}
```

* Jalankan proses 1 unit waktu.
* Tandai selesai jika sisa waktunya 0.

### 6. Hitung dan Cetak Hasil

```c
float totalTAT = 0, totalWT = 0;
for (int i = 0; i < n; i++) {
    p[i].turnaround = p[i].finish - p[i].arrival;
    p[i].waiting = p[i].turnaround - p[i].burst;
    totalTAT += p[i].turnaround;
    totalWT += p[i].waiting;
    printf("P%d | %d | %d | %d | %d | %d | %d\n", 
        p[i].id, p[i].arrival, p[i].burst, p[i].priority,
        p[i].finish, p[i].turnaround, p[i].waiting);
}
```

* Hitung Turnaround Time (TAT) dan Waiting Time (WT) per proses.
* Cetak dalam bentuk tabel.

```c
printf("\nRata-rata TAT: %.2f\n", totalTAT / n);
printf("Rata-rata WT : %.2f\n", totalWT / n);
```

* Hitung dan tampilkan rata-rata.

---

## ✅ Ringkasan

* Proses dengan prioritas tertinggi dijalankan lebih dulu.
* Preemptive: proses bisa dihentikan jika ada proses baru yang lebih prioritas.
* Output menampilkan waktu selesai, TAT, WT, dan rata-ratanya.

---



## Alur (Flow) dan Logika Program

###  Alur Umum Program:

1. **Inisialisasi Proses**

   * Data proses dimasukkan: waktu datang, burst time, dan prioritas.
   * Sisa waktu (`remaining`) diset sama dengan burst.

2. **Simulasi Waktu**

   * Waktu (`time`) dimulai dari 0 dan terus berjalan hingga semua proses selesai.

3. **Pemilihan Proses**

   * Setiap satuan waktu:

     * Cari semua proses yang sudah datang (`arrival <= time`).
     * Di antara mereka, pilih proses dengan **prioritas tertinggi** (angka terkecil).
     * Jika proses baru datang dengan prioritas lebih tinggi, proses lama akan **dipreempt**.

4. **Eksekusi Proses**

   * Proses yang dipilih akan dijalankan selama **1 unit waktu**.
   * Kurangi nilai `remaining`.
   * Jika `remaining == 0`, proses dianggap **selesai** dan waktu selesai dicatat.

5. **Perhitungan Akhir**

   * Setelah semua proses selesai, hitung:

     * **Turnaround Time (TAT)** = Finish Time - Arrival Time
     * **Waiting Time (WT)** = TAT - Burst Time
   * Hitung juga **rata-rata TAT dan WT**.


---

##  Kesimpulan Logika

* Simulasi dilakukan per detik.
* Proses dengan prioritas tertinggi yang tersedia akan dijalankan.
* Jika ada proses baru dengan prioritas lebih tinggi, sistem akan segera preempt proses lama.
* Waktu selesai dihitung secara akurat sesuai eksekusi per detik.
* Semua nilai akhir dihitung setelah proses selesai.

---


# Penjadwalan CPU: Priority Scheduling (Preemptive)

## 🔄 Alur (Flow) dan Logika Program

### 🧭 Alur Umum Program:

1. **Inisialisasi Proses**

   * Data proses dimasukkan: waktu datang, burst time, dan prioritas.
   * Sisa waktu (`remaining`) diset sama dengan burst.

2. **Simulasi Waktu**

   * Waktu (`time`) dimulai dari 0 dan terus berjalan hingga semua proses selesai.

3. **Pemilihan Proses**

   * Setiap satuan waktu:

     * Cari semua proses yang sudah datang (`arrival <= time`).
     * Di antara mereka, pilih proses dengan **prioritas tertinggi** (angka terkecil).
     * Jika proses baru datang dengan prioritas lebih tinggi, proses lama akan **dipreempt**.

4. **Eksekusi Proses**

   * Proses yang dipilih akan dijalankan selama **1 unit waktu**.
   * Kurangi nilai `remaining`.
   * Jika `remaining == 0`, proses dianggap **selesai** dan waktu selesai dicatat.

5. **Perhitungan Akhir**

   * Setelah semua proses selesai, hitung:

     * **Turnaround Time (TAT)** = Finish Time - Arrival Time
     * **Waiting Time (WT)** = TAT - Burst Time
   * Hitung juga **rata-rata TAT dan WT**.

---

## 💻 Potongan Kode Penting

### Inisialisasi:

```c
Process p[3] = {
    {1, 0, 4, 4, 2},
    {2, 1, 3, 3, 1},
    {3, 2, 1, 1, 3}
};
```

### Pemilihan dan Eksekusi:

```c
while (completed < n) {
    int highest = -1;
    for (int i = 0; i < n; i++) {
        if (p[i].arrival <= time && p[i].remaining > 0) {
            if (highest == -1 || p[i].priority < p[highest].priority)
                highest = i;
        }
    }

    if (highest != -1) {
        p[highest].remaining--;
        if (p[highest].remaining == 0) {
            p[highest].finish = time + 1;
            completed++;
        }
    }
    time++;
}
```

### Perhitungan Output:

```c
for (int i = 0; i < n; i++) {
    p[i].turnaround = p[i].finish - p[i].arrival;
    p[i].waiting = p[i].turnaround - p[i].burst;
    totalTAT += p[i].turnaround;
    totalWT += p[i].waiting;
}
```

---

## ✅ Kesimpulan Logika

* Simulasi dilakukan per detik.
* Proses dengan prioritas tertinggi yang tersedia akan dijalankan.
* Jika ada proses baru dengan prioritas lebih tinggi, sistem akan segera preempt proses lama.
* Waktu selesai dihitung secara akurat sesuai eksekusi per detik.
* Semua nilai akhir dihitung setelah proses selesai.


