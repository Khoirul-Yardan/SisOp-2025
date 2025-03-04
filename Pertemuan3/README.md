# 🚀 Linux Boot Process

## 🖥️ Overview
Linux Boot Process adalah tahapan yang terjadi ketika komputer dinyalakan hingga sistem operasi siap digunakan. Proses ini terdiri dari beberapa langkah utama, mulai dari **Power On** hingga **System Ready**.

---

## 🏁 Flowchart
<p align="center">
  <img src="flowchart.png" alt="Linux Boot Process Flowchart" width="600">
</p>

---

## 🔥 Tahapan Booting Linux

| 🔢 **Step** | 📝 **Deskripsi** |
|------------|----------------|
| **1. Power On** ⚡ | Ketika tombol daya ditekan, listrik mulai menyuplai semua komponen perangkat keras (CPU, RAM, HDD/SSD, dll.). |
| **2. BIOS/UEFI Initialization** 🛠️ | BIOS (Basic Input/Output System) atau UEFI (Unified Extensible Firmware Interface) menginisialisasi perangkat keras dan melakukan pengecekan awal. |
| **3. POST (Power-On Self Test)** ✅ | Sistem menjalankan tes mandiri untuk memastikan semua komponen perangkat keras bekerja dengan baik. Jika gagal, sistem akan menampilkan error atau beep code. |
| **4. Bootstrap Loader** 🔍 | BIOS/UEFI mencari bootloader di perangkat penyimpanan utama (HDD/SSD) dan mengeksekusinya. |
| **5. Bootloader (GRUB/LILO)** 🏗️ | Bootloader seperti GRUB (Grand Unified Bootloader) atau LILO (Linux Loader) memungkinkan pemilihan sistem operasi jika ada lebih dari satu OS. |
| **6. Load Kernel** 🖥️ | Kernel Linux dimuat ke dalam memori untuk mulai menjalankan sistem operasi. |
| **7. Initramfs (Initial RAM Filesystem)** 🧩 | Sistem memuat filesystem awal sementara yang berisi driver dan modul penting untuk melanjutkan proses booting. |
| **8. Kernel Initialization** 🏎️ | Kernel menginisialisasi semua modul perangkat keras, subsistem, dan driver yang dibutuhkan. |
| **9. Init System (Systemd/SysVinit)** 🔄 | Proses `init` seperti systemd atau SysVinit mulai berjalan untuk mengelola sistem dan layanan. |
| **10. Determine Runlevel/Target** 🎯 | Sistem menentukan runlevel (pada SysVinit) atau target (pada systemd) untuk menentukan mode operasi sistem. |
| **11. Mount Filesystems** 📂 | Sistem file utama (`/` root) dan partisi lainnya (`/home`, `/var`, dll.) dimuat ke dalam sistem. |
| **12. Start System Services** ⚙️ | Proses dan layanan latar belakang seperti networking, logging, dan daemon lainnya dimulai. |
| **13. User Login Prompt (TTY/GUI)** 🔑 | Sistem menampilkan antarmuka login (mode teks `TTY` atau GUI seperti GDM, SDDM, LightDM, dll.). |
| **14. System Ready** 🎉 | Sistem siap digunakan oleh pengguna! 🎊 |

---

## 📖 Referensi
- **Unix and Linux System Administration Handbook** by Evi Nemeth, Garth Snyder, Trent R. Hein, Ben Whaley, Dan Mackin
- Linux Documentation Project ([tldp.org](https://tldp.org))
- Official GNU GRUB Documentation ([gnu.org](https://www.gnu.org/software/grub/manual/grub.html))

---

## 💡 Notes
- **GRUB** adalah bootloader paling umum digunakan di Linux.
- **Systemd** adalah sistem `init` modern yang menggantikan SysVinit di banyak distribusi Linux.
- Untuk troubleshooting booting, gunakan `journalctl -b` untuk melihat log boot terakhir.

---

🔥 *Now your system is up and running! Enjoy Linux!* 🐧💻
