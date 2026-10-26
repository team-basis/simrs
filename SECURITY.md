# Kebijakan keamanan

Terima kasih sudah memeriksa keamanan SIMRS.

**Jangan melaporkan dugaan kerentanan lewat issue atau diskusi publik.** Yang tertulis di
sana terbaca semua orang, termasuk sebelum perbaikannya ada.

## Cara melapor

Kirim surel ke **basisapp.admin@gmail.com** dengan:

1. Ringkasan **dampaknya**: apa yang bisa dilakukan penyerang.
2. **Langkah minimal** untuk mengulangnya.
3. **Versi** paket yang Anda uji (di bawah layar masuk, atau `VERSI.txt`).
4. Sistem operasi dan cara Anda menjalankan aplikasinya.

Jangan menyertakan data pasien, isi `setelan.json`, kata sandi, token, atau kredensial.

## Yang kami lakukan

- Kami mengonfirmasi bahwa laporan Anda sudah diterima.
- Kami menilai dan memperbaikinya, lalu berkoordinasi dengan Anda soal waktu pengungkapan.
- Bila Anda berkenan, kami menyebut nama Anda pada catatan rilis yang memuat perbaikannya.

Kami tidak menjanjikan batas waktu tanggapan, dan tidak ada program imbalan.

## Cakupan

| Termasuk | Tidak termasuk |
|---|---|
| Aplikasi SIMRS dalam paket rilis terbaru: autentikasi, hak akses, pengamanan data, jejak audit | Sistem milik pihak lain (SATUSEHAT, BPJS, E-Klaim, dan seterusnya) |
| Cara pemasangan dan setelan bawaan yang tidak aman | Kelemahan di .NET, PostgreSQL, atau peramban. Laporkan ke penyelenggaranya |
| Kebocoran data antarperan atau antarpasien | Serangan yang butuh akses fisik ke server atau akun administrator yang sudah dikuasai |
| | Akun demo bersandi sama pada data contoh. Itu disengaja dan sudah tertulis di layarnya |

## Aturan main

- Uji hanya pada **pemasangan milik Anda sendiri**, dengan data karangan.
- Jangan mengakses, mengubah, atau menghapus data milik orang lain.
- Jangan menjalankan serangan penolakan layanan.

Paket ini **bukan untuk pelayanan pasien sungguhan**. Pemasangan yang memuat data pasien
sungguhan berada di luar lisensi uji coba, dan keamanannya menjadi tanggung jawab
pemasangnya.

## Versi yang didukung

Hanya rilis terbaru. Rilis ditandai preview.
