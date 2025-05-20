# 🧠 SJF (Shortest Job First) Scheduling - Non-Preemptive

Program ini mengimplementasikan algoritma **Shortest Job First (SJF)** dengan pendekatan **Non-Preemptive** menggunakan bahasa C.  
SJF Non-Preemptive menjadwalkan proses berdasarkan waktu burst terkecil, dan proses yang sedang berjalan tidak dapat dihentikan oleh proses lain yang datang.

---

## 📋 Deskripsi Algoritma

- **SJF Non-Preemptive** mengeksekusi proses berdasarkan waktu burst yang paling kecil terlebih dahulu.
- Tidak menggunakan arrival time (diasumsikan semua proses datang bersamaan).
- Setelah proses mulai berjalan, ia akan menyelesaikan eksekusinya tanpa gangguan (*non-preemptive*).
- Cocok digunakan untuk sistem batch di mana semua proses telah diketahui sebelumnya.

---

## 🧾 Code
```c
#include<stdio.h>
struct proc
{
    int no,bt,ct,tat,wt;
};
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    return p;
}
int main()
{
    struct proc p[10],tmp;
    float avgtat=0,avgwt=0;
    int n,ct=0;
    printf("<--SJF Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
    for(int i=0;i<n-1;i++)
        for(int j=0;j<n-i-1;j++)    
            if(p[j].bt>p[j+1].bt)
            {
				tmp=p[j];
				p[j]=p[j+1];
				p[j+1]=tmp;
            }
    printf("\nProcessNo\tBT\tCT\tTAT\tWT\tRT\n");
    for(int i=0;i<n;i++)
    {
        ct+=p[i].bt;
		p[i].ct=p[i].tat=ct;
		avgtat+=p[i].tat;
        p[i].wt=p[i].tat-p[i].bt;
        avgwt+=p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
    }
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
}
```

## 🧾 Contoh Input

Program akan meminta jumlah proses dan waktu burst untuk masing-masing proses.  
Contoh input:

Masukkan jumlah proses: 4

Masukkan burst time:
P1 = 6
P2 = 8
P3 = 7
P4 = 3


---

## 📊 Hasil Output Program

| Process | Burst Time (BT) | Completion Time (CT) | Turn Around Time (TAT) | Waiting Time (WT) | Response Time (RT) |
|---------|------------------|-----------------------|--------------------------|--------------------|---------------------|
| P4      | 3                | 3                     | 3                        | 0                  | 0                   |
| P1      | 6                | 9                     | 9                        | 3                  | 3                   |
| P3      | 7                | 16                    | 16                       | 9                  | 9                   |
| P2      | 8                | 24                    | 24                       | 16                 | 16                  |

📌 **Rumus:**
- `CT` (Completion Time) = waktu proses selesai
- `TAT` (Turn Around Time) = CT - Arrival Time (karena arrival time = 0, maka TAT = CT)
- `WT` (Waiting Time) = TAT - Burst Time
- `RT` (Response Time) = waktu mulai proses - Arrival Time = WT

---

<img src="1.png" alt="sjf" width="400">

## 🕒 Gantt Chart Eksekusi

Berikut adalah diagram Gantt Chart untuk penjadwalan berdasarkan burst time terkecil:

```mermaid
gantt
    title Gantt Chart - SJF Non-Preemptive
    dateFormat  x
    axisFormat  %L
    section Proses
    P4 : 0, 3
    P1 : 3, 6
    P3 : 9, 7
    P2 : 16, 8

