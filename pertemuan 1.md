# 📌 Tugas Pertemuan 1 - Sistem Operasi

## 📖 Topik: Sistem Bilangan

### 📌 Deskripsi
Tugas ini mencakup berbagai konversi sistem bilangan dari satu bentuk ke bentuk lainnya, termasuk biner, desimal, oktal, heksadesimal, BCD, dan ASCII.

---

## 🔢 **Daftar Soal & Jawaban**

### 1️⃣ **Pengertian Dasar**
**a.** Bilangan biner adalah bilangan yang berbasis **dua (2)**.
**b.** Bilangan heksadesimal adalah bilangan yang berbasis **enam belas (16)**.

---

### 2️⃣ **Konversi Desimal ke Biner**
**a.** 2321₁₀ 
1.	2321 ÷ 2 = 1160, sisa 1
2.	1160 ÷ 2 = 580, sisa 0
3.	580 ÷ 2 = 290, sisa 0
4.	290 ÷ 2 = 145, sisa 0
5.	145 ÷ 2 = 72, sisa 1
6.	72 ÷ 2 = 36, sisa 0
7.	36 ÷ 2 = 18, sisa 0
8.	18 ÷ 2 = 9, sisa 0
9.	9 ÷ 2 = 4, sisa 1
10.	4 ÷ 2 = 2, sisa 0
11.	2 ÷ 2 = 1, sisa 0
12.	1 ÷ 2 = 0, sisa 1
Membaca hasil dari bawah ke atas:
2321₁₀ = 100100010001₂


---

### 3️⃣ **Konversi Biner ke Desimal**
**a.** 10101010
(1 x 2⁷) + (0 x 2⁶) + (1 x 2⁵) + (0 x 2⁴) + (1 x 2³) + (0 x 2²) + (1 x 2¹) + (0 x 2⁰)

hasilnya:

128 + 0 + 32 + 0 + 8 + 0 + 2 + 0 = 170

Jadi, 10101010₂ = 170


---

### 4️⃣ **Konversi Biner ke Oktal**
**a.** 101 011 111 001
Jawab :
 101    011    111    001 
  5      3      7      1
Jadi, hasil konversi bilangan Jadi, hasil konversi bilangan biner 101011111001 biner 101011111001 ke bilangan oktal adalah 5371

---

### 5️⃣ **Konversi Oktal ke Biner**
**a.** 2170(8)
Jawab :
2 = 0.22 + 1.21 + 0.20
1 = 0.22 + 0.21 + 1.20
7 = 1.22 + 1.21 + 1.20
0 = 0.22 + 0.21 + 0.20

Jadi, hasil konversi bilangan oktal 2170(8) ke bilangan biner adalah 010001111000(2)


---

### 6️⃣ **Konversi Desimal ke Heksadesimal**
**a.** 1780(10)
Jawab :	1780	: 16 = 111 sisa 4
111	: 16 = 6	sisa 15
6	: 16 = 0	sisa 6
Jadi, hasil konversi bilangan desimal 1780(10) ke bilangan heksadesimal adalah 06F4(16)


---

### 7️⃣ **Konversi Heksadesimal ke Desimal**
**a.** ABCD(16)
Jawab  :	ABCD(16) = 10.163 + 11.162 + 12.161 + 13.160
= 40960 + 2816	+ 192	+ 13
= 43981(10)


---

### 8️⃣ **Konversi Pecahan Desimal ke Biner**
**a.** 0,3125(10)	
Jawab :	0,3125	. 2 = 0	sisa 0,625
	0,625	. 2 = 1	sisa 0,25
	0,25	. 2 = 0	sisa 0,5
	0,5	. 2 = 1	sisa 0
Jadi, hasil konversi bilangan desimal 0,3125(10) ke bilangan biner adalah 0,0101(2)


---

### 9️⃣ **Konversi Desimal ke Biner**
**a.** 11,625(10)
Jawab :	11	: 2 = 5 sisa 1
5	: 2 = 2 sisa 1
2	: 2 = 1 sisa 0
1	: 2 = 0 sisa 1

0,625	. 2 = 1	sisa 0,25
0,25	. 2 = 0	sisa 0,5
0,5	. 2 = 1	sisa 0
Jadi, hasil konversi bilangan desimal 11,625(10) ke bilangan biner adalah 1011,101(2) 
---

### 🔟 **Konversi Desimal ke Heksadesimal**
**a.** 348,654(10)
Jawab :	
348	: 16 = 21 sisa 12
21	: 16 = 1	sisa 5
1	: 16 = 0	sisa 1

0,654	. 16 = 10 sisa 0,464
0,464	. 16 = 7	sisa 0,424
0,424	. 16 = 6	sisa 0,784
Jadi, hasil konversi bilangan desimal 348,654(10) ke bilangan heksadesimal adalah 15C,A76(16)


---

### 1️⃣1️⃣ **Konversi ke Desimal**
**a.** 010100011,001111101₂ (Biner)
•	Konversi bilangan bulat:
0   1   0   1   0   0   0   1   1
2⁸  2⁷  2⁶  2⁵  2⁴  2³  2²  2¹  2⁰
(0 x 2⁸) + (1 x 2⁷) + (0 x 2⁶) + (1 x 2⁵) + (0 x 2⁴) + (0 x 2³) + (0 x 2²) + (1 x 2¹) + (1 x 2⁰) = 163
•	Konversi pecahan:
0   0   1   1   1   1   1   0   1
2⁻¹ 2⁻² 2⁻³ 2⁻⁴ 2⁻⁵ 2⁻⁶ 2⁻⁷ 2⁻⁸ 2⁻⁹
(0 x 2⁻¹) + (0 x 2⁻²) + (1 x 2⁻³) + (1 x 2⁻⁴) + (1 x 2⁻⁵) + (1 x 2⁻⁶) + (1 x 2⁻⁷) + (0 x 2⁻⁸) + (1 x 2⁻⁹) = 0,2451171875
•	Gabungkan: 163 + 0,2451171875 = 163,2451171875

---

### 1️⃣2️⃣ **Konversi Biner ke BCD**
**a.** 10100110000111₂
1.	kelompok 4 bit ke dalam angka desimal:
o	1010 = 10
o	0110 = 6
o	0001 = 1
o	1100 = 12 
2.	Gabungkan angka-angka desimal tersebut: 10 6 1 1 2
Jadi, 10100110000111₂ = 106112 (BCD)


---

### 1️⃣3️⃣ **Konversi BCD ke Biner**
**a.** 1987 (BCD)
•	digit desimal ke dalam 4 bit biner:
o	1 = 0001
o	9 = 1001
o	8 = 1000
o	7 = 0111
•	bit-bit biner: 0001 1001 1000 0111
Jadi, 1987 (BCD) = 1100110000111₂

---

### 1️⃣4️⃣ **Konversi Biner ke BCO**
**a.** A.  11111101001₂
001 111 110 100 
Konversi setiap kelompok ke oktal: 1 7 6 4
Hasilnya: 1764₈ (BCO)


---

### 1️⃣5️⃣ **Konversi Biner ke BCH**
**a.** 1101111100101110₂
1101 1111 0010 1110
Konversi setiap kelompok ke heksadesimal: D F 2 E
Hasilnya: DF2E₁₆ (BCH)


---

### 1️⃣6️⃣ **Konversi BCH ke Heksadesimal**
**a.** F0DE (BCH)
Karena F, D, dan E bukan digit desimal yang valid, ini bukan bilangan BCH yang benar. Bilangan BCH seharusnya hanya mengandung angka 0-9.


---

### 1️⃣7️⃣ **Menentukan Bilangan Positif atau Negatif**
**a.** 01111111 → **Positif (127₁₀)**  


---

### 1️⃣8️⃣ **Konversi Bilangan Negatif ke Desimal**
**a.** 1.	Balik semua bit (0 menjadi 1, 1 menjadi 0).
2.	Tambahkan 1.
3.	Konversi ke desimal.
4.	Tambahkan tanda negatif.
a. 10001000: -120₁₀ 


---

### 1️⃣9️⃣ **ASCII Code ke Karakter**
**a.** 41₁₆ → **A**   

---

### 2️⃣0️⃣ **Karakter ke ASCII Code**
**a.** a → **61₁₆**  

---

### 2️⃣1️⃣ **Kode ASCII pada Monitor**
"PRINT X" dikonversi ke ASCII menjadi:  
**P (1010000) R (1010010) I (1001001) N (1001110) T (1010100) Space (0100000) X (1011000)**  

---

✨ **Tugas ini dikerjakan oleh: [Khoirul Yardan Mauluddin Zhorif] - [3124521022] - [TI A PSDKU LA]** ✨

