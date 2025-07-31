# 📝 Laporan Tugas Akhir

**Mata Kuliah**: Sistem Operasi

**Semester**: Genap / Tahun Ajaran 2024–2025

**Nama**: Wahyu septiyan

**NIM**: 240202846

**Modul yang Dikerjakan**:
`Modul 4 – Subsistem Kernel Alternatif`

---

## 📌 Deskripsi Singkat Tugas

* Membuat syscall `chmod(path, mode)` untuk mengatur mode file (read-only / read-write)
* Menambahkan device pseudo `/dev/random` yang menghasilkan byte acak

---

## 🛠️ Rincian Implementasi

* Menambahkan field `short mode` pada `struct inode` di `fs.h`
* Memodifikasi `file.c` agar `filewrite()` memeriksa mode read-only
* Implementasi syscall `chmod()` di `sysfile.c`, didaftarkan di `syscall.c`, `syscall.h`, `user.h`, `usys.S`
* Membuat driver baru `random.c` yang mengisi buffer dengan byte acak
* Menambahkan handler `randomread()` ke `devsw[]` di `file.c`
* Menambahkan device node `/dev/random` lewat `mknod` di `init.c`
* Menulis program uji `chmodtest.c` dan `randomtest.c`

---

## ✅ Uji Fungsionalitas

* `chmodtest`: menguji pemblokiran penulisan ke file yang di-set read-only
* `randomtest`: membaca byte acak dari `/dev/random`

---

## 📷 Hasil Uji

### 📍 Output `chmodtest`:

```
Write blocked as expected
```

### 📍 Output `randomtest`:

```
219 34 101 88 200 12 9 56
```


---

## ⚠️ Kendala yang Dihadapi

* Kesulitan menangani pointer dari user space menggunakan `argptr()` / `argstr()`
* Lupa menyertakan `#include "spinlock.h"` saat akses inode
* Salah akses anggota struct (`.` vs `->`)
* Program uji gagal karena salah definisi parameter syscall
* Device tidak terdaftar karena dev major tidak cocok

---

## 📚 Referensi

* [Buku xv6 MIT](https://pdos.csail.mit.edu/6.828/2018/xv6/book-rev11.pdf)
* [Repositori xv6-public MIT](https://github.com/mit-pdos/xv6-public)
* Stack Overflow, diskusi kelas, dokumentasi praktikum
* chat gpt

---
