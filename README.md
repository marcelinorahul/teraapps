# TERA — Laporan Losses & Rata-rata Kernel

TERA adalah aplikasi web sederhana untuk membantu menyiapkan laporan Oil Losses ke template Excel dan menghitung rata-rata sampling kernel per silo. Aplikasi dapat dijalankan langsung dari browser tanpa instalasi.

## Ringkasan fungsi

### 1. Laporan Losses

- Menerima teks laporan yang ditempel, termasuk format dengan tanda bintang dari WhatsApp.
- Mendeteksi tanggal, shift, titik sampling, serta nilai Moist, OWM, dan ODM.
- Menampilkan nilai yang dikenali dan memberi tanda untuk titik yang tidak dikenal.
- Menyediakan **Buat format kosong lengkap** untuk membuat format laporan yang dapat dilengkapi, disalin, atau dikirim melalui WhatsApp. Format ini terpisah dari laporan yang sedang ditempel sehingga tidak menghapus data tersebut.
- Membaca template `.xlsx`, menyiapkan perubahan, dan menampilkan sel serta nilai sebelum file diunduh.
- Melewati sel berisi rumus atau sel gabungan. Sel yang sudah berisi angka dilewati secara default; pengguna dapat memilih untuk menimpanya.
- Menyediakan batas Moist, OWM, dan ODM opsional sebagai pengingat nilai yang perlu diperiksa.

### 2. Rata-rata Kernel

- Membaca beberapa sampling dari teks WhatsApp, termasuk pesan dengan awalan waktu/pengirim.
- Memungkinkan sampling dipilih satu per satu atau berdasarkan rentang jam; rentang dapat melewati tengah malam.
- Menghitung rata-rata, nilai minimum, dan maksimum NU, NP, C, dan Total.
- Mengelompokkan hasil menurut silo, menandai data duplikat, dan mengingatkan jika Total berbeda dari NU + NP + C.
- Menyiapkan teks hasil untuk disalin atau dibagikan melalui WhatsApp.

## Cara menggunakan

### Mengisi laporan Losses ke Excel

1. Buka `index.html` di browser.
2. Pada tab **Laporan Losses**, tempel laporan ke kotak **Tempel laporan**. Sertakan tanggal seperti `03.11.2026`, shift seperti `Shift II (Malam)`, nama titik sampling, dan nilai yang tersedia.
3. Jika membutuhkan format untuk meminta/mengumpulkan data lengkap, tekan **Buat format kosong lengkap**. Tanggal dan shift akan diambil dari teks yang sudah ditempel bila terdeteksi. Lengkapi format pada kotak yang muncul, lalu salin atau kirim melalui WhatsApp.
4. Pilih template Excel `.xlsx` yang sesuai. File template dibaca di browser dan harus dipilih ulang jika halaman/sesi dimulai kembali.
5. Periksa titik dan angka yang terdeteksi. Pilih apakah angka yang sudah ada di sel Excel akan dilewati atau ditimpa.
6. Tekan **Isi & review**. Periksa ringkasan, alamat sel, nilai sebelumnya, dan status setiap perubahan.
7. Tekan **Download Excel** hanya setelah hasil review benar.

### Menghitung rata-rata Kernel

1. Buka tab **Rata-rata Kernel** dan tempel satu atau beberapa laporan sampling.
2. Pilih sampling yang ingin dihitung, atau gunakan pilihan rentang jam.
3. Tinjau hasil per silo dan catatan pemeriksaan data.
4. Salin teks hasil atau buka WhatsApp untuk membagikannya.

## Format laporan Losses

Nama titik yang dikenali antara lain Fibre/Fiber Press 1–6, Nut, Heavy Phase Centrifuge 1–5, Before BP, EBP 1–2, Crude EBP, Underflow Juice Tank, Condensat 1–2, Inlet Recovery, dan Final Effluent. Nama parameter yang diterima: `Moist`, `Moisture`, `Kadar Air`, `Owm`/`OWM`, dan `Odm`/`ODM`.

Contoh:

```text
Lap Oil Losses
Selasa, 03.11.2026
Shift II (Malam)

Line I
Fibre Press 2
Moist = 39.93
Owm = 3.97
Odm = 6.59

Nut
Owm = 0.84
Odm = 0.95
```

Nilai yang tidak disertakan tetap kosong dan tidak akan ditulis ke Excel. Format kosong lengkap mencantumkan semua titik sampling aplikasi; kolom Moist hanya ditampilkan pada titik yang menggunakan Moist pada format laporan.

## Cara aplikasi menentukan tujuan Excel

- Nama sheet mengikuti tanggal laporan: tanggal 3 masuk ke sheet `03`.
- Shift I menggunakan baris dasar 78 dan Shift II menggunakan baris dasar 144.
- Parameter ditulis pada tiga baris berurutan: Moist pada baris dasar, OWM pada baris berikutnya, dan ODM pada baris setelahnya.
- Kolom titik sampling: Fibre Press 1–6 (`C`–`H`), Nut Line I/II (`J`/`K`), Before BP (`M`), EBP 1–2 (`N`/`O`), Heavy Phase Centrifuge 1–5 (`S`–`W`), Crude EBP (`X`), Underflow Juice Tank (`Y`), Condensat 1–2 (`AA`/`AB`), Inlet Recovery (`AC`), dan Final Effluent (`AD`).
- Jika tanggal laporan dan bulan template tidak cocok, aplikasi meminta konfirmasi. Shift III belum tersedia pada pemetaan template.

## Privasi dan kebutuhan teknis

- Teks laporan dan preferensi disimpan di `localStorage` browser pada perangkat pengguna; proses Excel juga berjalan di browser. File template tidak disimpan sebagai preferensi dan hanya berada di memori selama halaman terbuka.
- Untuk memproses Excel, browser memuat JSZip dari jsDelivr saat fitur tersebut digunakan. Koneksi internet diperlukan untuk pemuatan ini. Font IBM Plex juga dimuat dari Google Fonts; tanpa koneksi, browser menggunakan font sistem.
- Gunakan browser modern yang mendukung JavaScript dan File API. Aplikasi menerima `.xlsx`, bukan format Excel lama `.xls`.
- Hasil Excel adalah salinan yang diunduh sebagai file baru dengan akhiran `-terisi.xlsx`; file sumber tidak ditimpa.

## Presentasi singkat

> “TERA membantu mempercepat pekerjaan laporan harian. Untuk Oil Losses, pengguna menempel data, memeriksa nilai yang terbaca, memilih template Excel, lalu meninjau perubahan sebelum mengunduh. Jika perlu mengumpulkan data, aplikasi juga membuat format kosong lengkap yang bisa disalin atau dikirim melalui WhatsApp. Untuk Kernel, beberapa sampling bisa dipilih dan dihitung rata-ratanya per silo, disertai pemeriksaan duplikat dan kecocokan total. Semua proses utama berjalan di browser, dan file Excel baru diunduh setelah diperiksa.”

## Berkas proyek

- `index.html` — antarmuka, gaya, logika pengenalan/penghitungan, serta ekspor Excel.
- `README.md` — panduan penggunaan dan penjelasan alur aplikasi.
