# Komponen pihak ketiga dan atribusi

SIMRS memuat dan memakai karya pihak lain. Tiap karya tunduk pada lisensinya sendiri.
Lisensi uji coba SIMRS (berkas `LISENSI.txt` di dalam zip, `LICENSE.txt` di repositori)
**tidak mengubah hak Anda** atas komponen di bawah ini.

Daftar ini diperiksa pada **27 Oktober 2026** langsung dari berkas lisensi tiap paket
(`nuspec` dan `package.json`), bukan dari ingatan. Berkas ini ikut di dalam zip unduhan.

| Bagian | Isinya |
|---|---|
| [1. Komponen yang ikut dalam paket](#1-komponen-yang-ikut-dalam-paket) | Pustaka .NET, JavaScript, font, dan ikon |
| [2. Yang Anda pasang sendiri](#2-yang-anda-pasang-sendiri) | .NET runtime, PostgreSQL, peramban |
| [3. Katalog terminologi yang ditanam](#3-katalog-terminologi-yang-ditanam) | ICD, LOINC, SNOMED CT, KFA, KPTL, wilayah, dan pemberitahuan wajibnya |
| [4. Layanan luar yang butuh izin penyelenggaranya](#4-layanan-luar-yang-butuh-izin-penyelenggaranya) | SATUSEHAT, BPJS, E-Klaim, dan lainnya |
| [5. Nama dan merek](#5-nama-dan-merek) | Siapa pemilik nama yang disebut di sini |

## 1. Komponen yang ikut dalam paket

### Pustaka .NET

| Komponen | Dipakai untuk | Lisensi | Hak cipta |
|---|---|---|---|
| Entity Framework Core | Akses basis data | MIT | Microsoft Corporation |
| Npgsql, Npgsql.EntityFrameworkCore.PostgreSQL | Penghubung ke PostgreSQL | PostgreSQL License | The Npgsql Development Team |
| EFCore.NamingConventions | Penamaan tabel dan kolom | Apache-2.0 | Shay Rojansky |
| Firely SDK (Hl7.Fhir.R4, Hl7.Fhir.Base, Hl7.Fhir.Conformance, Fhir.Metrics) | Menyusun dan memvalidasi resource FHIR R4 | BSD-3-Clause | Firely, memuat materi HL7 International |
| Newtonsoft.Json | Pembaca JSON yang dipakai Firely SDK | MIT | James Newton-King |
| BouncyCastle.Cryptography | Kriptografi penerima webhook SATUSEHAT (HPKE) | MIT | Legion of the Bouncy Castle Inc. |
| ClosedXML, ClosedXML.Parser | Ekspor dan impor Excel | MIT | Para pengembang ClosedXML |
| DocumentFormat.OpenXml | Dipakai ClosedXML | MIT | Microsoft Corporation |
| ExcelNumberFormat | Dipakai ClosedXML | MIT | Para pengembang ExcelNumberFormat |
| SixLabors.Fonts (versi 1.0.0) | Dipakai ClosedXML untuk mengukur teks | Apache-2.0 | Six Labors |
| RBush.Signed | Dipakai ClosedXML | MIT | Turning Code, LLC dan lainnya |
| QRCoder | Kode QR pemasangan aplikasi autentikator | MIT | Raffael Herrmann, Shane Krueger |

### JavaScript, gaya, font, dan ikon

| Komponen | Dipakai untuk | Lisensi | Hak cipta |
|---|---|---|---|
| Tabulator | Tabel data besar | MIT | Oli Folkerd |
| Tailwind CSS | Gaya tampilan (sudah dikompilasi ke satu berkas CSS) | MIT | Tailwind Labs, Inc. |
| IBM Plex Sans dan IBM Plex Mono | Huruf | SIL Open Font License 1.1 | IBM Corp. |
| Material Symbols | Ikon | Apache-2.0 | Google |

Teks lisensi font dan ikon ikut di dalam paket, di folder `wwwroot/lib`
(`LICENSE-ibm-plex-sans.txt`, `LICENSE-ibm-plex-mono.txt`, `LICENSE-material-symbols.txt`).

Seluruh pustaka di atas dibawa dalam bentuk biner (DLL) tanpa perubahan.

## 2. Yang Anda pasang sendiri

Tiga hal ini **tidak ikut dalam paket**. Anda memasangnya sendiri dan tunduk pada lisensinya.

| Komponen | Lisensi | Sumber |
|---|---|---|
| ASP.NET Core Runtime 10 (termasuk Blazor) | MIT | <https://dotnet.microsoft.com/download/dotnet/10.0> |
| PostgreSQL 16 atau 17 | PostgreSQL License | <https://www.postgresql.org/download/> |
| Peramban (Chrome, Edge, Firefox) | Menurut penerbitnya | |

## 3. Katalog terminologi yang ditanam

Aplikasi menanam katalog kode supaya petugas bisa memilih diagnosis, obat, dan layanan
dari daftar baku. **Katalog ini milik penerbitnya**, bukan milik SIMRS.

| Katalog | Dipakai untuk | Penerbit | Sumber yang kami pakai |
|---|---|---|---|
| ICD-10 | Diagnosis | World Health Organization | Berkas e-Klaim yang diterbitkan Kemenkes |
| ICD-9-CM | Prosedur | U.S. National Center for Health Statistics | Berkas e-Klaim yang diterbitkan Kemenkes |
| LOINC | Pemeriksaan laboratorium dan observasi | Regenstrief Institute | Terminologi yang diterbitkan Kemenkes (lihat catatan di bawah) |
| SNOMED CT | Sebagian kecil kode: jenis spesimen dan zat penyebab alergi | SNOMED International | Lampiran terminologi resmi SATUSEHAT |
| KFA | Obat, vaksin, dan alat kesehatan | Kemenkes | API SATUSEHAT |
| KPTL | Kode pembiayaan tindakan dan layanan | Kemenkes | Master Data API SATUSEHAT |
| Kewilayahan | Provinsi sampai kelurahan | Kemenkes | API SATUSEHAT |

Paket **tidak** memuat rilis penuh SNOMED CT.

### Pemberitahuan LOINC

> This material contains content from LOINC (http://loinc.org). LOINC is copyright ©
> Regenstrief Institute, Inc. and the Logical Observation Identifiers Names and Codes
> (LOINC) Committee and is available at no cost under the license at
> http://loinc.org/license. LOINC® is a registered United States trademark of
> Regenstrief Institute, Inc.

Daftar LOINC di SIMRS berasal dari terminologi Kemenkes, **bukan** dari rilis Regenstrief.
Ia memuat kode LOINC sungguhan **beserta kode tambahan Kemenkes** untuk pemeriksaan yang
belum punya padanan LOINC. Kode tambahan itu bukan bagian dari LOINC.

### Pemberitahuan SNOMED CT

SNOMED CT® adalah merek dagang terdaftar milik SNOMED International
(<https://www.snomed.org>). Indonesia adalah negara anggota SNOMED International, diwakili
Kementerian Kesehatan. Pemakaian SNOMED CT di negara anggota **tidak dikenai biaya**, dan
pemakaiannya didaftarkan lewat kanal resmi negara itu. Rumah sakit yang memakai SIMRS di
Indonesia bertanggung jawab mendaftarkan pemakaiannya sendiri.

## 4. Layanan luar yang butuh izin penyelenggaranya

SIMRS **tidak membawa kredensial siapa pun** dan **tidak mengirim apa pun ke luar** sampai
Anda sendiri menyalakan sebuah integrasi dan mengisi kredensialnya. Kredensial itu
diterbitkan penyelenggara layanannya, tidak oleh SIMRS.

| Layanan | Penyelenggara | Yang perlu Anda miliki |
|---|---|---|
| SATUSEHAT (FHIR, webhook) | Kemenkes | Client ID, Client Secret, dan Organization ID. Untuk mencoba, akun pengembang sandbox milik Anda sendiri sudah cukup |
| BPJS VClaim, Antrean Online, Aplicares, i-Care JKN | BPJS Kesehatan | Fasilitas yang bekerja sama dengan BPJS Kesehatan, beserta Consumer ID, Consumer Secret, User Key, dan kode fasilitas dari BPJS |
| E-Klaim (grouper INA-CBG) | Kemenkes | Aplikasi E-Klaim dipasang sendiri di jaringan rumah sakit, beserta kunci enkripsi web service-nya. SIMRS hanya memanggilnya |
| SISRUTE | Kemenkes | Consumer ID, kata sandi, dan kode fasilitas |
| SIRANAP | Kemenkes | ID rumah sakit dan kata sandi |
| DICOM Router (untuk ImagingStudy) | Kemenkes | Komponen dipasang terpisah di jaringan rumah sakit |
| Alat laboratorium dan modalitas radiologi | Vendor alat | Alat yang mendukung HL7 v2 atau DICOM Modality Worklist |

Playbook, petunjuk teknis, dan koleksi Postman SATUSEHAT adalah terbitan Kemenkes. SIMRS
memakainya sebagai **acuan rancangan** dan tidak menyertakannya, baik dalam paket maupun di
repositori ini. Unduh versi terbarunya dari Kemenkes.

Memakai integrasi pada data pasien sungguhan di luar uji coba memerlukan **kesepakatan
tersendiri** dengan pemegang hak cipta SIMRS. Lihat butir 8 pada lisensi uji coba.

## 5. Nama dan merek

SATUSEHAT, E-Klaim, INA-CBG, SISRUTE, SIRANAP, dan nama sejenis dimiliki Kemenkes.
BPJS Kesehatan, VClaim, Antrean Online, Aplicares, dan i-Care JKN dimiliki BPJS Kesehatan.
HL7® dan FHIR® adalah merek dagang terdaftar HL7 International. LOINC® dan SNOMED CT®
dimiliki penerbitnya masing-masing.

SIMRS dibuat secara mandiri. Ia **tidak berafiliasi dengan, dan tidak disahkan oleh,**
Kemenkes, BPJS Kesehatan, atau pemilik nama-nama itu. Nama-nama tersebut disebut semata
untuk menjelaskan sistem mana yang dapat disambungi.
