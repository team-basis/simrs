# SIMRS — Panduan Penguji

Terima kasih sudah mau mencoba. Aplikasi ini sistem informasi manajemen rumah sakit
(pendaftaran, rekam medis, farmasi, penunjang, kasir, akuntansi, dan lainnya). Anda diminta
mencobanya dan memberi masukan, **bukan memakainya untuk pasien**.

> **Jangan memasukkan data pasien sungguhan.** Ini versi uji. Pakai nama dan nomor karangan.

## Yang perlu ada di komputer Anda

| Kebutuhan | Keterangan |
|---|---|
| **ASP.NET Core Runtime 10** | Runtime, bukan SDK. [Unduh](https://dotnet.microsoft.com/download/dotnet/10.0). Di Windows, pilih **Hosting Bundle** atau **ASP.NET Core Runtime** |
| **PostgreSQL 16 atau 17** | Di komputer ini, atau di server lain yang bisa dijangkau. Versi lain belum diuji |
| Peramban modern | Chrome, Edge, atau Firefox |

Aplikasi tidak memasang apa pun ke sistem Anda. Ia hanya folder yang dijalankan.

### Memasang keduanya di komputer yang masih bersih

**Windows 10/11.** Buka *Terminal* atau *PowerShell*, lalu:

```
winget install -e --id Microsoft.DotNet.AspNetCore.10
winget install -e -i --id PostgreSQL.PostgreSQL.17
```

Perintah kedua membuka pemasang PostgreSQL. Ia meminta Anda menetapkan **sandi pengguna
`postgres`**: catat, karena itulah yang diisikan ke `setelan.json`. Biarkan portnya `5432`.
Tutup lalu buka lagi terminalnya sesudah memasang, supaya perintah `dotnet` dikenali.

**Ubuntu 24.04** (juga di dalam WSL):

```
sudo apt update
sudo apt install -y aspnetcore-runtime-10.0 postgresql unzip
sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'sandi-pilihan-anda'"
pg_lsclusters
```

Baris terakhir menampilkan **port** PostgreSQL. Lazimnya `5432`. Bila tertulis angka lain
(mis. `5433`, terjadi bila `5432` sudah dipakai, termasuk oleh PostgreSQL di Windows saat Anda
memakai WSL), ganti `Port=5432` di `setelan.json` dengan angka itu, dan tambahkan `-p 5433`
pada perintah `psql` di atas.

Di Linux aplikasinya dijalankan dengan `bash jalankan.sh`.

**Distribusi Linux lain.** Pasang *ASP.NET Core Runtime 10* dan PostgreSQL menurut petunjuk
distribusinya ([.NET di Linux](https://learn.microsoft.com/dotnet/core/install/linux),
[PostgreSQL](https://www.postgresql.org/download/linux/)).

Periksa hasilnya dengan `dotnet --list-runtimes`: harus ada baris
`Microsoft.AspNetCore.App 10.…`.

> Langkah Ubuntu 24.04 sudah kami jalankan dari distro bersih sampai data contoh tertanam.
> Langkah Windows baru diperiksa terhadap katalog `winget`; distribusi Linux lain belum dicoba.

## Menjalankan

1. **Bongkar zip** ke folder biasa.
2. **Jalankan sekali** (`jalankan.bat` di Windows, `bash jalankan.sh` di Linux atau macOS).
   Ia membuat `setelan.json` dari contohnya lalu berhenti.
3. **Buka `setelan.json`** dan isi dua hal:
   - `ConnectionStrings` → `Hospital`: alamat PostgreSQL Anda (`Host`, `Port`, `Username`,
     `Password`). Nama basis data (`simrs`) **dibuat otomatis**.
   - `Hospital` → `InitialAdmin` → `Password`: sandi akun administrator pertama, **minimal 10
     karakter**.
4. **Jalankan lagi.** Start pertama memakan **beberapa menit**: aplikasi membuat basis data,
   menerapkan skemanya, lalu menanam katalog (ICD-10, ICD-9-CM, LOINC, KFA obat, wilayah).
   Selesai bila konsol menampilkan `Now listening on: http://localhost:5000`.
5. **Buka <http://localhost:5000>** di peramban. Masuk sebagai `admin` dengan sandi tadi. Anda
   diminta menggantinya, lalu **memasang aplikasi autentikator** (Google Authenticator,
   Microsoft Authenticator, atau sejenisnya) dengan memindai kode QR di layar. Simpan delapan
   kode pemulihan yang tampil. Sesudahnya, tiap kali `admin` masuk, sistem meminta enam digit
   dari ponsel itu.
6. **Isi data contoh** (disarankan): buka **Pengaturan → Data contoh**, lalu tekan **Isi Data
   Contoh**. Dalam kira-kira satu menit basis data terisi poliklinik, dokter, jadwal, stok,
   40 pasien karangan, dan satu akun per peran. Layar itu menampilkan daftar akun beserta
   sandinya.

Biarkan jendela konsol terbuka selama aplikasi dipakai. Menutupnya menghentikan aplikasi.

**Pengguna PostgreSQL** perlu hak **membuat basis data** (`CREATEDB`). Bila tim IT Anda yang
menyiapkan basis datanya, minta mereka membuatnya dan menjadikan penggunanya sebagai pemilik;
aplikasi lalu hanya mengisinya.

## Yang perlu diketahui

- **Data contoh hanya bisa ditanam sekali, pada basis data yang belum berisi pasien.** Begitu
  ada pasien, tombolnya menolak. Untuk mulai lagi dari awal, ganti nama basis data di
  `ConnectionStrings` (mis. `Database=simrs2`) lalu jalankan ulang.
- **Akun demo bersandi sama dan sandinya tertulis di layar.** Itu memudahkan berganti peran
  (dokter, perawat, kasir, apotek, dan seterusnya), dan berarti siapa pun yang bisa menjangkau
  aplikasi ini bisa masuk. Jangan membukanya ke jaringan yang tidak Anda percayai.
- **Tanpa data contoh, aplikasi mulai dari kosong.** Administrator membuat akun di
  **Pengaturan → Pengguna**, dan data dasar (poliklinik, tenaga kesehatan, layanan, tarif,
  obat) di **Master data**. Nama rumah sakit bawaannya *RS Sehat Sentosa*; gantilah di
  **Master data → Lokasi**.
- **Sandi baru administrator tidak boleh memuat kata `admin`**, minimal 10 karakter, dan
  tidak boleh angka saja. Layar ganti sandi menyebutkan syarat mana yang belum terpenuhi.
- **Autentikator hanya diwajibkan bagi akun pengelola pengguna** (`admin`). Akun demo per peran
  masuk dengan sandi saja, kecuali pemiliknya memasangnya sendiri lewat nama akun di pojok kanan
  atas. Tidak punya ponsel untuk dipakai? Tambahkan
  `"Security": { "RequireAuthenticatorForAdministrators": false }` di dalam bagian `Hospital`
  pada `setelan.json`, lalu jalankan ulang.
- **Akun `admin` tidak bisa mengerjakan pelayanan.** Ia mengelola pengguna dan pengaturan
  saja; pendaftaran, pemeriksaan, apotek, dan kasir dikerjakan akun perannya masing-masing.
  Itu pemisahan kewenangan yang disengaja.
- **Integrasi ke luar mati bawaannya.** SATUSEHAT, BPJS, E-Klaim, SISRUTE, SIRANAP, alat
  laboratorium, dan DICOM Router baru bekerja bila Anda menyalakannya di `setelan.json` dan
  mengisi kredensialnya, yang diterbitkan Kemenkes dan BPJS, bukan oleh paket ini. Aplikasi
  berjalan penuh tanpa semuanya. Statusnya terbaca di **Pengaturan → Antrean integrasi**,
  beserta tombol **Uji** untuk memeriksa sambungannya.
- **Mengakses dari komputer lain.** Lewat `http://localhost` di komputer yang sama, aplikasi
  tidak memerlukan sertifikat. Dari komputer lain, aplikasi **menolak masuk lewat HTTP** dan
  meminta HTTPS (sertifikat atau reverse proxy). Itu disengaja: isi rekam medis tidak boleh
  lewat jaringan tanpa enkripsi.
- **Zona waktu.** Bawaannya WIB (`Asia/Jakarta`). Bila komputer Anda berzona lain, aplikasi
  berhenti dengan pesan tentang zona waktu. Ubah `TimeZone` di `setelan.json`:
  `Asia/Makassar` untuk WITA, `Asia/Jayapura` untuk WIT.

## Menyambungkan ke SATUSEHAT sandbox (opsional)

Untuk melihat data pelayanan sampai di Kemenkes, Anda memerlukan **akun pengembang SATUSEHAT
sandbox** milik Anda sendiri: Client ID, Client Secret, dan Organization ID. Paket ini tidak
membawa kredensial siapa pun.

- **Paket demo** (namanya berakhiran `-demo`) membawa kit penyiap dan **`SKENARIO.md`**: isi
  kredensial di `setelan.json`, jalankan `siapkan-demo`, lalu ikuti `SKENARIO.md`. Kit menanam
  sepuluh tenaga kesehatan uji Kemenkes, akun dokternya, kode obat dan layanan yang diterima
  Kemenkes, serta mendaftarkan pasien acak ke sandbox Anda.
- **Paket biasa** tidak membawa kit. Menyalakan SATUSEHAT di sana tetap boleh, tetapi dokter
  data contoh tidak dikenal Kemenkes, sehingga kunjungannya tertahan di **Antrean integrasi**
  dengan alasan yang tertulis.

Pengiriman selalu berjalan di latar belakang. Pelayanan tidak pernah menunggu Kemenkes, juga
saat internet putus: kirimannya menyusul sendiri.

## Memberi masukan

Tulis di **<https://github.com/team-basis/simrs>**:

- **Galat atau yang membingungkan**: buka *Issues*, lalu pilih templatnya.
- **Pertanyaan, ide, atau cerita**: buka *Discussions*.
- **Dugaan kerentanan keamanan**, atau hal yang tidak boleh terbaca publik: kirim surel ke
  **basisapp.admin@gmail.com**, jangan lewat Issues.

Masukan paling berguna bila memuat:

1. **Versi**, tertulis di bagian bawah layar masuk (juga di `VERSI.txt`).
2. **Layar** tempat terjadinya (alamat di peramban, atau nama menunya).
3. **Yang Anda lakukan**, langkah demi langkah.
4. **Yang terjadi**, dan **yang Anda harapkan**.
5. Bila aplikasi berhenti atau menampilkan galat: **teks di jendela konsol**.

Masukan tentang yang *membingungkan* sama berharganya dengan yang *rusak*: layar yang tidak
jelas harus mengisi apa, istilah yang tidak Anda kenal, atau langkah yang terasa terlalu
panjang.

**Jangan melampirkan data pasien sungguhan** atau isi `setelan.json` Anda (di dalamnya ada
sandi).

## Lisensi

Paket ini gratis untuk dicoba, dan boleh Anda bagikan utuh kepada orang lain. Ia **bukan**
untuk pelayanan pasien sungguhan, tidak boleh dijual, dan tidak boleh diubah atau dibongkar.
Ketentuan lengkapnya ada di `LISENSI.txt`.

## Memperbarui ke versi baru

1. Bongkar zip baru ke **folder baru** (jangan menimpa yang lama).
2. Salin `setelan.json` dari folder lama ke folder baru.
3. Jalankan. **Basis data diperbarui otomatis**, dan konsol mencatat peringatan bahwa skemanya
   dimutakhirkan.

Bila datanya berharga, buat cadangan lebih dulu (`pg_dump`). Aplikasi **tidak menurunkan
skema**: setelah basis data dimutakhirkan, versi yang lebih lama menolak menyala di atasnya.

## Bila ada masalah

| Yang terlihat | Penyebab dan jalan keluarnya |
|---|---|
| `.NET belum terpasang` atau `Runtime versi 10 tidak ditemukan` | Pasang ASP.NET Core Runtime 10 (tautan di atas) |
| `PostgreSQL di … tidak bisa dihubungi` | PostgreSQL belum berjalan, atau alamat, port, pengguna, atau sandi di `ConnectionStrings` keliru |
| `PostgreSQL menolak pengguna …` | Nama pengguna atau sandi PostgreSQL keliru |
| `… tidak berwenang membuatnya` | Pengguna PostgreSQL tidak boleh membuat basis data. Pesannya memuat perintah `CREATE DATABASE` yang bisa dijalankan administrator PostgreSQL |
| `Basis data … sudah dimutakhirkan oleh versi aplikasi yang lebih baru` | Anda menjalankan versi lama di atas basis data versi baru. Pakai versi yang sama atau lebih baru, atau arahkan ke basis data lain |
| `Zona waktu sistem operasi … berbeda` | Ubah `TimeZone` di `setelan.json` (lihat di atas) |
| Tidak bisa masuk, konsol menyebut `Akun administrator awal belum dikonfigurasi` | `InitialAdmin` → `Password` di `setelan.json` masih kosong. Isi, lalu jalankan ulang. Akun hanya dibuat bila belum ada satu pengguna pun |
| Layar masuk menyebut aplikasi dilayani lewat HTTP | Anda membuka lewat alamat selain `localhost`. Buka `http://localhost:5000`, atau pasang HTTPS |
| **Pengaturan → Data contoh** menyebut penanaman tidak dinyalakan | `Hospital` → `DemoData` → `Enabled` di `setelan.json` bernilai `false` atau terhapus. Jadikan `true`, lalu jalankan ulang |
| Data contoh ditolak karena basis data sudah berisi pasien | Data contoh hanya untuk basis data kosong. Ganti nama basis data di `ConnectionStrings`, lalu jalankan ulang |
| `address already in use` | Port 5000 dipakai program lain. Ubah `Urls` di `setelan.json`, mis. `http://localhost:5050` |
