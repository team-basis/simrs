# Cara berpartisipasi

Terima kasih sudah tertarik pada SIMRS.

**Kode sumber aplikasi tidak dibuka, jadi pull request tidak dipakai.** Yang kami butuhkan
dari Anda adalah **masukan**: temuan galat, ide, dan cerita dari lapangan. Itu bukan
kontribusi kelas dua. Sistem rumah sakit yang tidak pernah dicoba orang rumah sakit
hampir pasti salah di tempat yang tidak terlihat dari meja pengembang.

## Mau menyampaikan apa, ke mana

| Anda ingin | Pakai | Alasannya |
|---|---|---|
| Melaporkan sesuatu yang **rusak** | [Issue: Laporan galat](https://github.com/team-basis/simrs/issues/new?template=bug.yml) | Perlu langkah dan versi supaya bisa diulang |
| Melaporkan sesuatu yang **membingungkan** atau terlalu panjang | [Issue: Pengalaman mencoba](https://github.com/team-basis/simrs/issues/new?template=pengalaman-uji.yml) | Layar yang tidak jelas sama seriusnya dengan layar yang rusak |
| Mengusulkan **fitur atau perubahan alur** | [Issue: Saran](https://github.com/team-basis/simrs/issues/new?template=saran.yml) | Satu usulan satu issue, supaya bisa dilacak |
| **Bertanya**, berdiskusi, atau berbagi cerita | [Discussions](https://github.com/team-basis/simrs/discussions) | Tidak semua hal perlu jadi pekerjaan |
| Melaporkan **kerentanan keamanan** | [Kebijakan keamanan](SECURITY.md) | Jangan di issue publik |
| Membicarakan **pemakaian sungguhan** di rumah sakit Anda | Surel ke basisapp.admin@gmail.com | Butuh kesepakatan terpisah, lihat [LICENSE.txt](LICENSE.txt) butir 8 |

Bingung memilih? Mulailah di Discussions. Kami bisa memindahkannya menjadi issue.

## Laporan galat yang mudah dikerjakan

Sertakan ketujuh hal ini. Templatnya sudah menanyakannya satu per satu.

1. **Versi.** Tertulis di bawah layar masuk, dan di berkas `VERSI.txt` dalam paket.
2. **Sistem operasi.** Windows atau Linux, beserta versinya.
3. **Layar.** Nama menunya, atau alamat di bilah peramban.
4. **Langkah demi langkah** sampai masalahnya muncul.
5. **Yang terjadi.**
6. **Yang Anda harapkan.**
7. **Teks di jendela konsol**, bila aplikasi berhenti atau menampilkan galat.

Tangkapan layar membantu, asal datanya karangan.

## Yang jangan pernah dilampirkan

- Data pasien sungguhan. Paket ini hanya untuk uji coba dengan data karangan.
- Isi `setelan.json`. Di dalamnya ada sandi.
- Kata sandi, token, Client Secret, User Key, atau kredensial apa pun.
- Log yang memuat salah satu di atas. Periksa dulu sebelum menempelkannya.

Bila terlanjur terkirim, hapus komentarnya atau beri tahu kami, dan **ganti kredensialnya**.

## Masukan yang paling kami cari

Anda tidak perlu paham teknologi untuk memberi masukan yang berharga. Yang paling
berguna datang dari orang yang bekerja di rumah sakit:

- **Alur yang tidak sesuai kenyataan** di unit Anda. Urutan kerjanya berbeda, atau ada
  langkah yang di tempat Anda tidak pernah terjadi.
- **Istilah** yang tidak dipakai di rumah sakit Anda, atau dipakai dengan arti lain.
- **Laporan** yang Anda butuhkan tetapi belum ada, atau angkanya tidak cocok dengan hitungan Anda.
- **Aturan regulasi** yang kami tafsirkan keliru. Sebutkan peraturannya bila tahu.
- **Isian yang terlalu banyak** atau layar yang terlalu panjang untuk dikerjakan sambil berdiri.
- **Akun dan hak akses**: pekerjaan yang seharusnya bisa dikerjakan satu peran tetapi tidak bisa.

Beri tahu **peran Anda** (dokter, perawat, apoteker, kasir, administrator, manajemen).
Layar yang sama terlihat sangat berbeda dari tiap meja.

## Yang terjadi sesudah Anda menulis

- Kami membaca semuanya.
- Kami **tidak menjanjikan waktu tanggapan**, dan tidak semua usulan akan dikerjakan.
- Bila kami menolak sebuah usulan, kami menyebut alasannya.
- Bila laporan kurang lengkap, kami bertanya. Mohon dijawab di issue yang sama.
- Perbaikan tercatat di catatan rilis. Rilis bertanda **preview**, jadi sesuatu bisa
  berubah antarversi.

## Sikap saling menghormati

Kritik pada sistem dipersilakan sekeras apa pun. Serangan pada orang tidak. Tulislah
seperti Anda ingin laporan Anda dibaca: jelas, sopan, dan tanpa asumsi buruk.
Komentar yang melecehkan, mengancam, atau mempromosikan produk lain akan dihapus.
