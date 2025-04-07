# Tugas Fork: Parent - Child Process

**Oleh:** [Khoirul Yardan Mauluddin Zhorif 3124521022 TI A PSDKU LA]

## 1. Konsep fork() dalam Pemrograman C

Dalam sistem operasi berbasis UNIX/Linux, `fork()` adalah salah satu sistem call terpenting yang digunakan untuk membuat proses baru. Ketika fungsi `fork()` dipanggil, maka proses yang sedang berjalan (disebut parent) akan membuat salinan dirinya sendiri (disebut child). Keduanya akan melanjutkan eksekusi secara independen dari titik setelah `fork()` dipanggil.

Nilai kembalian dari `fork()` digunakan untuk membedakan proses induk dan anak:
- Jika `fork()` mengembalikan 0, maka itu berarti kode sedang dijalankan oleh proses child.
- Jika `fork()` mengembalikan nilai positif (PID child), maka kode dijalankan oleh parent.
- Jika `fork()` mengembalikan -1, maka proses gagal dibuat.

### Implementasi fork() dalam Bahasa C

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    fork();
    printf("Hello from process %d\n", getpid());
    return 0;
}
```

Kode di atas akan mencetak dua baris "Hello from process ..." karena `fork()` membuat proses baru yang mengeksekusi `printf()` juga. Hal ini menunjukkan bagaimana satu baris kode dapat dieksekusi lebih dari sekali dengan `fork()`.

## 2. Akses dan cloning repo

```bash
git clone https://github.com/ferryastika/operatingsystem.git
cd operatingsystem/fork
```

## 3. Deskripsi dan Visualisasi Pohon Proses

### Fork01.cpp

```cpp
using namespace std;

#include <iostream>
#include <sys/types.h>
#include <unistd.h>

/* getpid() adalah system call yg dideklarasikan pada unistd.h.
Menghasilkan suatu nilai dengan type pid_t.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/
int main(void) {
        pid_t mypid;
        uid_t myuid;
        for (int i = 0; i < 3; i++) {
                mypid = getpid();
                cout << "I am process " << mypid << endl;
                cout << "My parent process ID is " << getppid() << endl;
                cout << "The owner of this process has uid " << getuid()
        << endl;
/* sleep adalah system call atau fungsi library
yang menghentikan proses ini dalam detik
*/
        sleep(3);
        }
return 0;
```

Program ini belum menggunakan `fork()`, jadi tidak membuat proses anak (child process). Artinya, hanya akan ada 1 proses tunggal yang dieksekusi.

**Penjelasan Isi Program:**
- `getpid()` = Mengambil ID dari proses yang sedang berjalan.
- `getppid()` = Mengambil ID dari proses induk (parent).
- `getuid()` = Mengambil ID dari user pemilik proses.
- `sleep(3)` = Menunda proses selama 3 detik.
- Program akan melakukan loop sebanyak 3 kali, dan setiap kali mencetak info prosesnya.

**Visualisasi Pohon Proses:**

Karena tidak ada `fork()`, maka tidak ada percabangan proses. Prosesnya linear, hanya satu proses.

```
[Terminal/Shell] → [fork01]
```

### Fork02.cpp

```cpp
#include <iostream>
#include <sys/types.h>
#include <unistd.h>
using namespace std;

/* getpid() dan fork() adalah system call yg dideklarasikan
pada unistd.h.
Menghasilkan suatu nilai dengan type pid_t.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/
int main(void) {
        pid_t childpid;
        int x = 5;
        childpid = fork();

        while (1) {
                cout << "This is process ID" << getpid() << endl;
                cout << "In this process the value of x becomes " << x << endl;
                sleep(2);
                x++;
        }
        return 0;
}
```

**Penjelasan:**
- `fork()` akan menduplikasi proses. Jadi, setelah `fork()` dipanggil:
  - Satu proses menjadi dua (parent dan child).
  - Keduanya akan mengeksekusi kode yang sama, dari baris setelah `fork()`.
- Variabel x di-copy (bukan shared), sehingga proses parent dan child punya salinan x masing-masing.

**Perulangan:**
- Proses parent dan child masuk ke `while(1)`, dan mencetak:
  - PID proses
  - Nilai dari x (yang akan terus naik tiap 2 detik)
- `x++` dilakukan di masing-masing proses = nilainya bisa berbeda antar parent dan child seiring waktu.

**Visualisasi Pohon Proses:**

```
[Terminal/Shell] → [fork02 (parent)] → [fork02 (child)]
```

Setelah `fork()`, dua proses akan berjalan berdampingan secara paralel: parent dan child.

### Fork03.cpp

```cpp
#include <iostream>
using namespace std;
#include <sys/types.h>
#include <unistd.h>

/* getpid() dan fork() adalah system call yg dideklarasikan
pada unistd.h.
Menghasilkan suatu nilai dengan type pid_t.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/
int main(void) {
        pid_t childpid;
        childpid = fork();
        for (int i = 0; i < 5; i++) {
                cout << "This is process " << getpid() << endl;
                sleep(2);
        }
        return 0;
}
```

**Penjelasan:**
- Program akan memanggil `fork()`, yang artinya:
  - Proses parent akan beranak satu proses child.
- Setelah `fork()`, dua proses (parent & child) akan masuk ke loop for 5 kali.
- Di setiap iterasi, program akan mencetak:
  - PID proses (dari `getpid()`)
  - Kemudian tidur selama 2 detik menggunakan `sleep(2)`.

Karena `fork()` dijalankan sebelum loop, maka:
- Kedua proses akan menjalankan loop yang sama, bersamaan, namun PID-nya berbeda.

**Visualisasi Pohon Proses:**

```
[Terminal/Shell] → [fork03 (parent)] → [fork03 (child)]
```

Tidak bercabang banyak, hanya 1 parent dan 1 child, lalu masing-masing mencetak 5 kali identitas dirinya.

### Fork04.cpp

```cpp
#include <iostream>
using namespace std;
#include <sys/types.h>
#include <unistd.h>
#include <sys/wait.h>
/* pid_t fork() dideklarasikan pada unistd.h.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/

int main(void) {
        pid_t child_pid;
        int status;
        pid_t wait_result;
        child_pid = fork();
        if (child_pid == 0) {
                /* kode ini hanya dieksekusi proses child */
                cout << "I am a child and my pid = " << getpid() << endl;
                cout << "My parent is " << getppid() << endl;
                /* keluar if akan menghentikan hanya proses child */
        }
        else if (child_pid > 0) {
                /* kode ini hanya mengeksekusi proses parent */
                cout << "I am the parent and my pid = " << getpid() << endl;
                cout << "My child has pid = " << child_pid << endl;
        }
        else {
                cout << "The fork system call failed to create a new process" << endl;
                exit(1);
        }
                /* kode ini dieksekusi baik oleh proses parent dan child */
                cout << "I am a happy, healthy process and my pid = " << getpid() << endl;
                if (child_pid == 0) {
                /* kode ini hanya dieksekusi oleh proses child */
                cout << "I am a child and I am quitting work now!"<< endl;
        }
        else {
                /* kode ini hanya dieksekusi oleh proses parent */
                cout << "I am a parent and I am going to wait for my child" << endl;
        do {
                /* parent menunggu sinyal SIGCHLD mengirim tanda bahwa proses child diterminasi */
                wait_result = wait(&status);
        } while (wait_result != child_pid);
                cout << "I am a parent and I am quitting." << endl;
        }
        return 0;
}
```

**Penjelasan:**
- Program membuat satu child process menggunakan `fork()`.
- Proses Child:
  - Menampilkan PID-nya dan PID parent-nya (`getpid()` dan `getppid()`).
  - Lalu mencetak pesan bahwa dia berhenti kerja.
- Proses Parent:
  - Menampilkan PID-nya dan PID anak-nya.
  - Menunggu child selesai dengan `wait()`.
  - Baru kemudian mencetak pesan bahwa dia ikut keluar.

**Fungsi wait():**
- Fungsi `wait(&status)` akan menahan eksekusi proses parent hingga proses child selesai.
- Ini menghindari zombie process (proses anak yang belum diambil statusnya oleh parent).

**Visualisasi Pohon Proses:**

```
[Terminal/Shell] → [fork04 (parent)] → [fork04 (child)]
                                       ↓
                                      [exit]
                                       ↓
                [fork04 (parent)] → [wait done] → [exit]
```

Hanya dua proses, tapi alur eksekusinya lebih rapi karena ada `wait()`.

### Fork05.cpp

```cpp
#include <iostream>
using namespace std;
#include <sys/types.h>
#include <unistd.h>
#include <sys/wait.h>
/* pid_t fork() dideklarasikan pada unistd.h.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/

int main(void) {
  pid_t child_pid;
  int status;
  pid_t wait_result;
  child_pid = fork();
  if (child_pid == 0) {
    /* kode ini hanya dieksekusi proses child */
    cout << "I am a child and my pid = " << getpid() << endl;
    execl("/bin/ls", "ls", "-l", "/home", NULL);
    /* jika execl berhasil kode ini tidak pernah digunakan */
    cout << "Could not execl file /bin/ls" << endl;
    exit(1);
    /* exit menghentikan hanya proses child */
   }
  else if (child_pid > 0) {
    /* kode ini hanya mengeksekusi proses parent */
   cout << "I am the parent and my pid = " << getpid() << endl;
   cout << "My child has pid = " << child_pid << endl;
  }
  else {
   cout << "The fork system call failed to create a new process" << endl;
   exit(1);
  }
  /* kode ini hanya dieksekusi oleh proses parent karena
  child mengeksekusi dari "/bin/ls" atau keluar */
   cout << "I am a happy, healthy process and my pid = " << getpid() << endl;
   if (child_pid == 0) {
  /* kode ini tidak pernah dieksekusi */
   printf("This code will never be executed!\n");
  }
  else {
   /* kode ini hanya dieksekusi oleh proses parent */
    cout << "I am a parent and I am going to wait for my child" << endl;
    do {
      /* parent menunggu sinyal SIGCHLD mengirim tanda bila proses child diterminasi */
      wait_result = wait(&status);
    } while (wait_result != child_pid);
    cout << "I am a parent and I am quitting." << endl;
  }
  return 0;
}
```

**Fungsi-fungsi:**
- `fork()` = membuat child process.
- `execl("/bin/ls", "ls", "-l", "/home", NULL)` = menggantikan program di child dengan perintah `ls -l /home`.
- `wait()` = membuat parent menunggu child selesai, agar tidak langsung keluar.

**Alur Eksekusi:**
1. Parent process:
   - Membuat child dengan `fork()`.
   - Mencetak informasi prosesnya.
   - Menunggu child selesai (`wait()`).
   - Keluar setelah itu.
2. Child process:
   - Mencetak informasi dirinya.
   - Menjalankan `ls -l /home` lewat `execl()`.
   - Jika berhasil, kode setelah `execl()` tidak dijalankan.
   - Jika gagal, mencetak pesan error.

**Visualisasi Pohon Proses:**

```
[Terminal/Shell] → [fork05 (parent)] → [fork05 (child)]
                                       ↓
                                      [execl /bin/ls]
                                       ↓
                                      [ls -l /home]
                                       ↓
                                      [exit]
                                       ↓
                [fork05 (parent)] → [wait done] → [exit]
```

- `execl()` mengganti image proses, PID-nya tetap, tapi prosesnya bukan lagi fork05, melainkan ls.
- Parent hanya melihat PID anaknya (child_pid), dan `wait()` sampai selesai.

### Fork06.cpp

```cpp
#include <iostream>
using namespace std;
#include <sys/types.h>
#include <unistd.h>
#include <sys/wait.h>
/* pid_t fork() dideklarasikan pada unistd.h.
pid_t adalah type khusus untuk process id yg ekuivalen dg int
*/

int main(void) {
        pid_t child_pid;
        int status;
        pid_t wait_result;
        child_pid = fork();


        if (child_pid == 0) {
                /* kode ini hanya dieksekusi proses child */
                cout << "I am a child and my pid = " << getpid() << endl;
                execl("fork03", "goose", NULL);
                /* jika execl berhasil kode ini tidak pernah digunakan */
                cout << "Could not execl file fork3" << endl;
                exit(1);
                /* exit menghentikan hanya proses child */
        }
        else if (child_pid > 0) {
                /* kode ini hanya mengeksekusi proses parent */
                cout << "I am the parent and my pid = " << getpid()<< endl;
                cout << "My child has pid = " << child_pid << endl;
        }
        else {
                cout << "The fork system call failed to create a new process" << endl;
                exit(1);
        }
        /* kode ini hanya dieksekusi oleh proses parent karena
        child mengeksekusi dari "fork3" atau keluar */
                cout << "I am a happy, healthy process and my pid = " << getpid() << endl;
                if (child_pid == 0) {
        /* kode ini tidak pernah dieksekusi */
                printf("This code will never be executed!\n");
        }
        else {
        /* kode ini hanya dieksekusi oleh proses parent */
                cout << "I am a parent and I am going to wait for my child" << endl;
                do {
                /* parent menunggu sinyal SIGCHLD mengirim tanda
                bila proses child diterminasi */
                        wait_result = wait(&status);
                } while (wait_result != child_pid);
                cout << "I am a parent and I am quitting." << endl;
        }
        return 0;
}
```

**Fungsi-fungsi:**
- `fork()` = membuat child process.
- `execl("fork03", "goose", NULL)` = menggantikan proses child dengan program bernama fork03 (yang harus berada di direktori yang sama dan sudah di-compile jadi executable).
- `wait()` = membuat parent menunggu child selesai.
- `exit(1)` = mengakhiri child jika `execl()` gagal.

**Alur Eksekusi:**
1. Parent process:
   - Mencetak PID dirinya dan anaknya.
   - Menunggu hingga child selesai dengan `wait()`.
   - Keluar.
2. Child process:
   - Mencetak PID-nya sendiri.
   - Menjalankan fork03 dengan `execl()`.
     - Jika `execl()` berhasil, maka proses fork06 child akan digantikan oleh program fork03.
     - Jika `execl()` gagal, muncul pesan error dan proses keluar.

**Visualisasi Pohon Proses:**

```
[Terminal/Shell] → [fork06 (parent)] → [fork06 (child)]
                                       ↓
                                      [execl fork03]
                                       ↓
                                      [fork03]
                                       ↓
                                      [exit]
                                       ↓
                [fork06 (parent)] → [wait done] → [exit]
```

- fork06 membuat child.
- Child langsung digantikan oleh fork03.
- Parent tetap menunggu hingga proses fork03 selesai.