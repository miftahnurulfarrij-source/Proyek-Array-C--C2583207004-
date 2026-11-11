# Proyek-Array-C--C2583207004-
# Sistem Monitoring Stok dan Penjualan Kantin Kampus

| | |
|---|---|
| **Nama Lengkap** | Miftah Nurul Farrij
| **NIM** | C2583207004
| **Kelas** | PTI3A 
| **Mata Kuliah** | Algoritma dan Pemrograman Lanjutan |
| **Dosen Pengampu** | Taofik Muhammad, M.Kom |
| **Nama Proyek** | Proyek-Array-C- C2583207004 |

## Deskripsi Singkat

Aplikasi console berbahasa C untuk membantu pengelola kantin kampus memantau stok, memproses transaksi penjualan beberapa produk, mencari dan mengurutkan produk, serta melihat laporan penjualan. Seluruh data disimpan dalam array selama program berjalan (tanpa database atau file eksternal). Kapasitas maksimal 50 produk dan tersedia 6 produk sebagai data awal.

## Daftar Fitur

| Menu | Fitur |
|---|---|
| 1 | Lihat daftar produk (nama, harga, stok) |
| 2 | Tambah produk baru (validasi nama kosong, duplikat, harga, stok, kapasitas penuh) |
| 3 | Ubah harga dan stok produk |
| 4 | Transaksi penjualan beberapa produk dalam satu transaksi, dengan rincian subtotal dan total, serta konfirmasi sebelum stok dikurangi |
| 5 | Tambah stok |
| 6 | Cari produk berdasarkan nama (tidak membedakan huruf besar/kecil, mendukung sebagian kata) |
| 7 | Urutkan produk berdasarkan harga termurah atau jumlah terjual terbanyak |
| 8 | Laporan penjualan: jumlah terjual per produk, total unit, total pendapatan, produk terlaris |
| 9 | Cek stok menipis (stok kurang dari 5) |
| 0 | Keluar |

## Penjelasan Penggunaan Array

| Array | Tipe | Fungsi |
|---|---|---|
| `char nama[50][30]` | array karakter 2 dimensi | menyimpan nama produk; baris = produk, kolom = karakter |
| `int harga[50]` | array 1 dimensi | harga satuan tiap produk |
| `int stok[50]` | array 1 dimensi | stok tersedia tiap produk |
| `int terjual[50]` | array 1 dimensi | jumlah unit terjual tiap produk |
| `int pendapatan[50]` | array 1 dimensi | akumulasi pendapatan tiap produk |
| `int jumlah` | variabel | jumlah data aktif; data valid berada pada indeks `0` sampai `jumlah-1` |

Semua array sejajar: indeks yang sama menunjuk produk yang sama. Penambahan produk memakai `jumlah` sebagai indeks berikutnya dan ditolak bila `jumlah >= 50`. Saat transaksi, jumlah beli sementara disimpan di array lokal `keranjang[50]` dan baru mengubah `stok`, `terjual`, serta `pendapatan` setelah transaksi dikonfirmasi. Pengurutan memakai array indeks (`urut[]`) dengan *selection sort*, sehingga nomor produk pada array asli tidak berubah.

## Cara Kompilasi dan Menjalankan

Memerlukan compiler GCC.

```bash
gcc -Wall -Wextra -o kantin main.c
./kantin          # Linux/macOS
kantin.exe        # Windows
```

## Skenario Pengujian

> Ganti setiap `screenshots/...png` dengan tangkapan layar Anda sendiri, simpan di folder `screenshots/` pada repository.

| No | Skenario | Input atau Tindakan | Hasil yang Diharapkan | Bukti |
|---|---|---|---|---|
| 1 | Tambah produk | Menu 2, masukkan produk baru | Produk muncul dalam daftar | ![Uji 1](screenshots/uji1-tambah-produk.png) |
| 2 | Transaksi | Menu 4, beli beberapa produk | Subtotal dan total benar | ![Uji 2](screenshots/uji2-transaksi.png) |
| 3 | Pembaruan stok | Selesaikan transaksi (konfirmasi `y`) | Stok dan jumlah terjual berubah | ![Uji 3](screenshots/uji3-pembaruan-stok.png) |
| 4 | Stok tidak cukup | Beli melebihi stok | Transaksi ditolak; stok tetap | ![Uji 4](screenshots/uji4-stok-tidak-cukup.png) |
| 5 | Laporan | Menu 8 | Unit, pendapatan, dan terlaris benar | ![Uji 5](screenshots/uji5-laporan.png) |
| 6 | Pengurutan | Menu 7 pilihan 1 dan 2 | Urutan sesuai ketentuan | ![Uji 6](screenshots/uji6-pengurutan.png) |
| 7 | Pencarian dan stok | Menu 6 lalu menu 9 | Hasil dan peringatan tepat | ![Uji 7](screenshots/uji7-cari-dan-stok.png) |

### Keterangan Singkat Tiap Pengujian

1. **Tambah produk.** Input: nama, harga, stok. Proses: data disimpan pada indeks `jumlah`, lalu `jumlah` bertambah. Output: produk tampil di menu 1. *(tulis ulang dengan kata-kata Anda)*
2. **Transaksi.** Input: nomor produk dan jumlah (berulang sampai `0`). Proses: validasi stok, hitung subtotal = harga x jumlah, total = jumlah semua subtotal. Output: rincian dan total pembayaran.
3. **Pembaruan stok.** Setelah konfirmasi, `stok` berkurang dan `terjual` bertambah sebesar jumlah beli.
4. **Stok tidak cukup.** Jumlah beli melebihi stok ditolak dengan pesan; stok tidak berubah.
5. **Laporan.** Total unit = jumlah seluruh `terjual`; pendapatan = jumlah seluruh `pendapatan`; terlaris = produk dengan `terjual` tertinggi.
6. **Pengurutan.** Menampilkan produk berurutan harga naik atau terjual turun tanpa mengubah susunan array asli.
7. **Pencarian dan stok.** Pencarian menemukan kecocokan sebagian nama; menu 9 menampilkan produk dengan stok < 5 beserta peringatan.

## Validasi Input yang Ditangani

- Pilihan menu tidak tersedia atau bukan angka
- Nomor produk tidak ditemukan
- Jumlah pembelian nol atau negatif
- Harga atau stok negatif
- Jumlah pembelian melebihi stok (termasuk akumulasi di keranjang)
- Kapasitas array penuh (50 produk)
  

- <img width="598" height="672" alt="image" src="https://github.com/user-attachments/assets/5ff055e4-7e87-4011-895d-dd97cb7c7b12" />


- <img width="597" height="682" alt="image" src="https://github.com/user-attachments/assets/de77b28e-87e8-4fc4-9c82-d10589ff01a7" />


- <img width="597" height="682" alt="image" src="https://github.com/user-attachments/assets/b8509867-8c02-42dd-b2f3-7ae991e5e34f" />


- <img width="595" height="676" alt="image" src="https://github.com/user-attachments/assets/fe20dbd8-b798-49cb-bd0f-11490d8f5607" />


- <img width="600" height="679" alt="image" src="https://github.com/user-attachments/assets/06733a7f-00c5-4ca3-a045-9f2ef4a76879" />


- <img width="655" height="676" alt="image" src="https://github.com/user-attachments/assets/913337a5-3d33-4838-8cf8-0e78019383e3" />


- <img width="550" height="523" alt="image" src="https://github.com/user-attachments/assets/c0d98b9a-f0f8-453c-89d3-850183d93e1b" />







