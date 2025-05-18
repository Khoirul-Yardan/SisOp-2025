# CPU Scheduling 
**Oleh:** [Khoirul Yardan Mauluddin Zhorif 3124521022 TI A PSDKU LA]

## Soal 5.17

Diberikan proses sebagai berikut:

| Process | Burst Time | Priority |
|---------|------------|----------|
| P₁      | 5          | 4        |
| P₂      | 3          | 1        |
| P₃      | 1          | 2        |
| P₄      | 7          | 2        |
| P₅      | 4          | 3        |

### a. Gantt Chart untuk Setiap Algoritma

#### FCFS (First Come First Serve)

Semua proses datang di waktu 0.

```
| P₁ | P₂ | P₃ | P₄ | P₅ |
0    5    8   9   16   20
```

#### SJF (Shortest Job First)

Urutan burst: P₃(1), P₂(3), P₅(4), P₁(5), P₄(7)

```
| P₃ | P₂ | P₅ | P₁ | P₄ |
0    1    4    8   13   20
```

#### Non-Preemptive Priority (semakin besar = prioritas lebih tinggi)

Urutan: P₁(4), P₅(3), P₃(2), P₄(2), P₂(1)

```
| P₁ | P₅ | P₃ | P₄ | P₂ |
0    5    9   10  17   20
```

#### Round Robin (Quantum = 2)

Proses berputar per 2 ms.

```
| P₁ | P₂ | P₃ | P₄ | P₅ | P₁ | P₄ | P₅ | P₁ | P₄ | P₄ |
0    2    4    5    7    9   11   13  15  16   18  20
```

### b. Turnaround Time (TAT)

Rumus: `TAT = Completion Time - Arrival Time`

| Proses | FCFS | SJF | Priority | RR |
|--------|------|-----|----------|----|
| P₁     | 5    | 13  | 5        | 15 |
| P₂     | 8    | 4   | 20       | 4  |
| P₃     | 9    | 1   | 10       | 5  |
| P₄     | 16   | 20  | 17       | 20 |
| P₅     | 20   | 8   | 9        | 13 |

### c. Waiting Time

Rumus: `Waiting Time = Turnaround Time - Burst Time`

| Proses | FCFS | SJF | Priority | RR |
|--------|------|-----|----------|----|
| P₁     | 0    | 8   | 0        | 10 |
| P₂     | 5    | 1   | 17       | 1  |
| P₃     | 8    | 0   | 9        | 4  |
| P₄     | 9    | 13  | 10       | 13 |
| P₅     | 16   | 4   | 5        | 9  |

### d. Rata-rata Waiting Time

| Algoritma | Avg Waiting Time |
|-----------|------------------|
| FCFS      | (0+5+8+9+16)/5 = 7.6 |
| SJF       | (8+1+0+13+4)/5 = 5.2 |
| Priority  | (0+17+9+10+5)/5 = 8.2 |
| RR (q=2)  | (10+1+4+13+9)/5 = 7.4 |

**Minimum average waiting time: SJF**

---

## Soal 5.18

| Process | Priority | Burst | Arrival |
|---------|----------|-------|---------|
| P₁      | 8        | 15    | 0       |
| P₂      | 3        | 20    | 0       |
| P₃      | 4        | 20    | 20      |
| P₄      | 4        | 20    | 25      |
| P₅      | 5        | 5     | 45      |
| P₆      | 5        | 15    | 55      |

### a. Gantt Chart (Priority Preemptive + RR for same priority, q=10)

```
| P₁ | P₂ | P₁ | idle | P₅ | idle | P₆ | P₃ | P₄ |
0    10   20   25     45   50    55   70   90   110
```

### b. Turnaround Time

| Process | Arrival | Completion | Turnaround |
|---------|---------|------------|------------|
| P₁      | 0       | 25         | 25         |
| P₂      | 0       | 20         | 20         |
| P₃      | 20      | 90         | 70         |
| P₄      | 25      | 110        | 85         |
| P₅      | 45      | 50         | 5          |
| P₆      | 55      | 70         | 15         |

### c. Waiting Time

| Process | Turnaround | Burst | Waiting |
|---------|------------|-------|---------|
| P₁      | 25         | 15    | 10      |
| P₂      | 20         | 20    | 0       |
| P₃      | 70         | 20    | 50      |
| P₄      | 85         | 20    | 65      |
| P₅      | 5          | 5     | 0       |
| P₆      | 15         | 15    | 0       |

---

