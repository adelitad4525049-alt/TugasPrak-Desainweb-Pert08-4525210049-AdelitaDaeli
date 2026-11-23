# Form Registrasi Event — Validasi Form Web

Proyek ini merupakan *form* registrasi *event* berbasis HTML5, CSS3, dan JavaScript yang dirancang responsif untuk tampilan *desktop* maupun *mobile*. Formulir ini mencakup komponen input teks, email, `select`, `radio`, `checkbox`, `upload` berkas (`input type="file"`), serta `textarea` yang dilengkapi dengan enam aturan validasi pada sisi klien.

## Ringkasan Pengembangan, Masalah, dan Solusi

Proyek ini membangun *form* registrasi *event* menggunakan HTML5, CSS3, dan JavaScript yang memuat elemen *text*, *email*, *select*, *radio*, *checkbox*, *upload* file, dan *textarea* beserta enam aturan validasi pada sisi klien untuk memastikan kelengkapan data pendaftar sebelum formulir dikirimkan.

Selama proses pengembangan, ditemukan beberapa kendala teknis yang memengaruhi kenyamanan serta kejelasan umpan balik bagi pengguna. Pertama, validasi bawaan *browser* saja menghasilkan tampilan peringatan yang berbeda-beda antarperamban sehingga pesan kesalahan terasa kurang konsisten dan sulit dikontrol penempatannya. Kedua, elemen pilihan seperti *radio* dan *checkbox* tidak memiliki satu kotak input tunggal layaknya input teks, sehingga indikator kesalahan perlu ditempatkan secara terpisah agar pengguna langsung mengetahui bagian mana yang belum diisi. Ketiga, pada bagian unggahan berkas, pengguna berpotensi memilih format file yang tidak didukung atau ukuran file yang terlalu besar. Keempat, pada layar sempit (*mobile*), susunan tombol aksi berpotensi terlihat sempit jika tetap disejajarkan secara horizontal.

Untuk mengatasi permasalahan tersebut, ditambahkan fungsi validasi JavaScript terpusat yang menampilkan pesan kesalahan khusus pada setiap *field* serta memberi penanda visual berwarna merah pada input yang tidak valid. Selain itu, diterapkan pengecekan tipe berkas (PDF, JPG, PNG) dan batas ukuran maksimal 2 MB, serta pengaturan *media query* CSS agar tata letak kartu dan tombol tetap rapi di layar *desktop* maupun *mobile*.

## Struktur Folder

```text
registrasi-event/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── script.js
├── Dokumentasi/
│   ├── desktop.png
│   └── mobile.png
└── README.md
```

## Test Case Validasi (5 Skenario Input Salah)

| No | Field | Input Uji | Hasil yang Diharapkan | Hasil Aktual |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `namaLengkap` | `"Ad"` (2 karakter) | Ditolak; tampil pesan wajib minimal 3 karakter pada `#err-namaLengkap` | Ditolak; muncul pesan error dan penanda merah pada input nama |
| 2 | `emailPeserta` | `"adelita-tanpa-domain"` | Ditolak; tampil pesan format email tidak valid pada `#err-emailPeserta` | Ditolak; muncul pesan error dan penanda merah pada input email |
| 3 | `topik` (checkbox) | Tidak ada topik yang dicentang | Ditolak; tampil pesan pilih minimal satu topik pada `#err-topik` | Ditolak; muncul pesan error di bawah daftar checkbox topik |
| 4 | `buktiFile` (upload) | File `.exe` atau file berukuran `3.5 MB` | Ditolak; tampil pesan format harus PDF/JPG/PNG atau ukuran maksimal 2 MB | Ditolak; muncul pesan error sesuai pelanggaran pada `#err-buktiFile` |
| 5 | `catatan` (textarea) | `"Halo"` (4 karakter) | Ditolak; tampil pesan catatan minimal 10 karakter pada `#err-catatan` | Ditolak; muncul pesan error dan penanda merah pada textarea |

## Validasi yang Tetap Wajib Dilakukan di Server

1. **Verifikasi tipe MIME, ekstensi, dan isi file unggahan:** Server tetap wajib memeriksa tipe file sebenarnya agar berkas berbahaya tidak lolos ke penyimpanan server meskipun validasi *browser* dilewati.
2. **Batas ukuran file & sanitasi teks:** Server harus membatasi ukuran unggahan serta membersihkan karakter pada input teks dan `textarea` untuk mencegah injeksi data.
3. **Kewajiban field, format email, dan daftar opsi valid (`select` & `radio`):** Server wajib memastikan nilai yang dikirim sesuai daftar opsi yang sah karena permintaan bisa dikirim langsung di luar formulir HTML.
4. **Aturan bisnis & kuota peserta:** Pengecekan ketersediaan kuota kehadiran *offline*/*online* maupun duplikasi pendaftaran hanya dapat dipastikan secara akurat di sisi server dan *database*.

## Dokumentasi Hasil Website

### Tampilan Desktop
![Tampilan Desktop](Dokumentasi/Desktop.jpeg)

### Tampilan Mobile
![Tampilan Mobile](Dokumentasi/mobile.jpeg)

## Catatan Tugas

* **Jenis Tugas:** Tugas Individu (dikerjakan secara mandiri).
* **Bukti Kelengkapan:** *Source code* project, *screenshot* tampilan *desktop* dan *mobile*, tabel *test case* validasi, pembahasan validasi server, serta ringkasan pengembangan.