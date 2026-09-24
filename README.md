# Dokumentasi API Pelaporan ASM

Dokumentasi ini menjelaskan endpoint-endpoint API yang digunakan pada alur **Pelaporan Klaim via API** untuk PT Asuransi Sinar Mas (ASM), meliputi environment GOLANG DEV.

## Daftar Isi

- [Get Token](#get-token)
- [Generate No Pelaporan](#generate-no-pelaporan)
- [Regis Pelaporan](#regis-pelaporan)
- [Upload Dokumen Pelaporan](#upload-dokumen-pelaporan)
- [Wilayah Bengkel](#wilayah-bengkel)
- [List Bengkel](#list-bengkel)
- [Pindah Bengkel](#pindah-bengkel)
- [Info Keunggulan Bengkel Tekno](#info-keunggulan-bengkel-tekno)
- [Pelaporan Stolen](#pelaporan-stolen)

---

## Get Token

### URL

| Environment | URL |
| --- | --- |
| GOLANG DEV | `http://192.168.10.210:8080/api/pelaporan/v1/token` |

### Auth

| Field | Value |
| --- | --- |
| Username | `serviceclaimq` |
| Password | `serviceclaimq` |

### Request Body (khusus GOLANG DEV)

```json
{ "USER_INPUT": "BARCODE" }
```

### Response

```json
{
    "AccessToken": "7d49287814c68dfced97439feca2129960438e2c10f2a4d1229f917e3cfd30a2"
}
```

---

## Generate No Pelaporan

### URL

| Environment | URL |
| --- | --- |
| GOLANG DEV | `http://192.168.10.210:8080/api/pelaporan/v1/nomor` |

### Request Body

```json
{
  "AccessToken": "7d49287814c68dfced97439feca2129960438e2c10f2a4d1229f917e3cfd302",
  "App": "BARCODE",
  "NoReferensiKlaim": "20242281531-f95036df-c270-7182-b60d-12c6f81ad603",
  "NoTelepon": "082173733675",
  "Sourcecode": "PT ASM",
  "NoPlat": "B1234ABC",
  "KodeWilayah": "B",
  "CabangKlaim": "DKI JAKARTA"
}
```

### Keterangan Field

| Field | Keterangan |
| --- | --- |
| App | Diisi Nama Aplikasi: `BARCODE` |
| NoTelepon | Diisi dengan Nomor Telepon Tertanggung |
| Sourcecode | Diisi dengan Nama Asuransi: `PT ASM` (server Testing) / `PT ASURANSI SINAR MAS` (server LIVE) |
| NoPlat | Diisi dengan Nomor Plat Kendaraan |
| NoReferensiKlaim | Diisi uniq ID dari Aplikasi Website |
| CabangKlaim | Diisi cabang klaim yang dipilih |

### Response

```json
{
    "Response": {
        "Status": "true",
        "pzInsKey": "PLP-03476",
        "CaseID": "PLP-03476",
        "NoReferensiKlaim": "17122025",
        "DokumenKTP": "TIDAK ADA / ADA",
        "DokumenSIM": "TIDAK ADA / ADA",
        "DokumenSTNK": "TIDAK ADA / ADA"
    }
}
```

---

## Regis Pelaporan

### URL

| Environment | URL |
| --- | --- |
| GOLANG DEV | `http://192.168.10.210:8080/api/pelaporan/v1/registrasi` |

### Request Body

```json
{
  "AccessToken": "7d49287814c68dfced97439feca2129960438e2c10f2a4d1229f917e3cfd302",
  "App": "BARCODE",
  "NoPelaporan": "PLP-03312",
  "EmailPelapor": "slamet.riyanto@qoala.id",
  "JenisKejadian": "Menabrak",
  "JenisKelamin": "PRIA",
  "JenisKerugian": "GABUNGAN",
  "JenisKlaim": "1",
  "CabangKlaim": "DKI JAKARTA",
  "Kronologis": "MENGHINDARI MONYET MENYEBRANG JALAN KEMUDIAN BANTING SETIR (MENGHINDAR) KE KIRI LALU MENYEREMPET BATU PIC : 082173733675 REQUEST BENGKEL TUJUAN : AMAN BERKAT MOTOR JL. GATOT SUBROTO NO. 13 TANJUNG PINANG KOTA TANJUNG PINANG",
  "Lokasi": "LAGOI",
  "NamaTertanggung": "PT MANDIRI PERDANA LESTARI",
  "NamaPelapor": "YORDAN",
  "NoReferensiKlaim": "20242281531-f95036df-c270-7182-b60d-12c6f81ad603",
  "NoTelepon": "082173733675",
  "Sourcecode": "PT ASM",
  "TanggalKejadian": "20251110T012638.000 GMT",
  "TanggalLapor": "20251109T012638.000 GMT",
  "NoPolis": "02910202300139",
  "NoPlat": "B1234ABC",
  "JenisSosmed": "INSTAGRAM",
  "UsernameSosmed": "@INSTAGRAM",
  "TanggalEstimasiMasukBengkel": "20251117T012638.000 GMT",
  "JenisPenggunaanKendaraan": "PRIBADI/DINAS",
  "StatusKepemilikanKendaraan": "MILIK SENDIRI",
  "KecepatanKendaraan": "20",
  "AlamatDomisili": "Jl. H. Fachrudin No.18 9, RT.9/RW.5 Kota Jakarta Pusat"
}
```

### Keterangan Field

| Field | Keterangan |
| --- | --- |
| App | Diisi Nama Aplikasi: `BARCODE` |
| EmailPelapor | Diisi Data Email Pelapor |
| NoPelaporan | Diisi No Pelaporan |
| JenisKejadian | Diisi dengan jenis kejadian: Ditabrak, Menabrak, Hilang, Lain-lain, Benturan, Terbalik, Tergelincir, Terperosok, Perbuatan Jahat, Kerusakan Diatas Kapal, Kebakaran, Kriminalitas, Huru Hara Dan SRCC, Terorisme Dan Sabotase, Gempa/Tsunami/Letusan Gunung, Banjir/Topan/Badai/Hujan Es/Tanah Longsor, Kerusakan Hanya Ban Velg/Dop, Penggunaan Komersial |
| JenisKelamin | Diisi Jenis Kelamin Tertanggung: PRIA, WANITA |
| JenisKerugian | Diisi dengan Coverage Klaim: GABUNGAN, KERUGIAN TOTAL |
| JenisKlaim | `1` = klaim Partial, `2` = klaim Stolen |
| Kronologis | Diisi dengan Kronologis Kejadian Klaim |
| Lokasi | Diisi dengan Lokasi Saat Kejadian |
| NamaTertanggung | Diisi dengan Nama Tertanggung |
| NamaPelapor | Diisi dengan Nama Pelapor |
| NoTelepon | Diisi dengan Nomor Telepon Tertanggung |
| Sourcecode | Diisi dengan Nama Asuransi: `PT ASM` (Testing) / `PT ASURANSI SINAR MAS` (LIVE) |
| TanggalKejadian | Diisi dengan Tanggal Terjadinya Kejadian |
| TanggalLapor | Diisi dengan Tanggal Lapor Klaim |
| JenisSosmed | Diisi Dengan Jenis Sosial Media: INSTAGRAM, FACEBOOK, TIKTOK |
| UsernameSosmed | Diisi Dengan Username Sosial Media |
| TanggalEstimasiMasukBengkel | Diisi dengan Estimasi Tanggal Kendaraan Masuk ke Bengkel |
| JenisPenggunaanKendaraan | Diisi dengan: PRIBADI/DINAS, KOMERSIL |
| StatusKepemilikanKendaraan | Diisi dengan: MILIK SENDIRI, SEWA/PINJAM |
| KecepatanKendaraan | Diisi Dengan Kecepatan Kendaraan saat terjadinya kecelakaan |
| AlamatDomisili | Diisi Dengan Alamat Domisili Tertanggung |

### Response (Sukses)

```json
{
    "Response": {
        "pzInsKey": "PLP-03474",
        "CaseID": "PLP-03474",
        "Status": "true",
        "NoReferensiKlaim": "17122025",
        "Note": "Data berhasil diperbarui untuk ID_PELAPORAN = PLP-03474",
        "IdBengkel": "0010003943",
        "NamaBengkel": "AUTO KOOL PRIMA, CV (CIREBON)",
        "AlamatBengkel": "JL. RAWA BALI I KAV.A NO.9 KIP RAWA TERATE CAKUNG",
        "NoTelepon": "33436",
        "IsTekno": "1"
    }
}
```

### Response (Gagal — Token tidak ditemukan)

```json
{
    "Response": {
        "Note": "Access Token Tidak Di Temukan",
        "Status": "false"
    }
}
```

---

## Upload Dokumen Pelaporan

### URL

| Environment | URL |
| --- | --- |
| GOLANG DEV | `http://192.168.10.210:8080/api/pelaporan/v1/dokumen` |

### Request Body

```json
{
    "NoPelaporan": "PLP-03312",
    "AccessToken": "12345",
    "Base64": "12345",
    "JenisDokumen": "KTP",
    "NamaDokumen": "FOTOKTP",
    "ExtensiDokumen": "jpeg",
    "SisiFotoKerusakan": "KANAN"
}
```

> `SisiFotoKerusakan` hanya digunakan khusus untuk Foto Sisi Kerusakan dan Foto Panel Kerusakan.

### Nilai `JenisDokumen`

- `KTP`
- `SIM`
- `STNK`
- `FOTO FULL KERUSAKAN`
- `FOTO KERUSAKAN`

### Foto Sisi Kerusakan (untuk `JenisDokumen: FOTO FULL KERUSAKAN`)

- KANAN
- KIRI
- DEPAN
- BELAKANG
- ATAS

### Foto Panel Kerusakan (untuk `JenisDokumen: FOTO KERUSAKAN`)

- Tampak Jauh
- Tampak Dekat

### Response

```json
{
    "Response": {
        "Status": "true",
        "JenisDokumen": "KTP",
        "NoPelaporan": "PLP-03312"
    }
}
```

---

## Wilayah Bengkel

### URL (GET)

| Environment | URL |
| --- | --- |
| GOLANG DEV | `http://192.168.10.210:8080/api/pelaporan/v1/kota` |

### Response

```json
{
  "Kota": "",
  "Response": {
    "Status": "true"
  },
  "DataAlamat": [
    {
      "Desc_Kota": "KAB. PASURUAN",
      "IdKota": "10055"
    }
  ]
}
```

---

## List Bengkel

### URL

| Environment | URL |
| --- | --- |
| GOLANG DEV | `http://192.168.10.210:8080/api/pelaporan/v1/bengkel` |

### Request Body (contoh)

```json
{
  "NoKlaim": "CLM-1121030",
  "NoPelaporan": "PLP-03889",
  "Wilayah": "10631",
  "NamaBengkel": "AUTO 2222"
}
```

| Field | Keterangan |
| --- | --- |
| NoKlaim | Return `CLM` jika ada |
| NoPelaporan | Return `PLP`, pasti ada |
| Wilayah | ID Kota yang sudah dipilih dari dropdown Pilih Wilayah (bisa kosong) |
| NamaBengkel | Nama Bengkel yang diketik (bisa kosong) |

### Response

```json
{
  "NoKlaim": "CLM-1121030",
  "NoPelaporan": "PLP-03889",
  "Wilayah": "10631",
  "DataBengkel": [
    {
      "Alamat": "Jln. Cilenggang 2 No. 30, Bsd",
      "IdBengkel": "0010002537",
      "NamaBengkel": "PUSAKA SATRIA UTAMA, PT - BLUE BIRD (NR - BSD)",
      "pxObjClass": "ASM-FW-ICMS-Data-Bengkel",
      "StsRekananBengkel": "0",
      "TELEPHONE": "021-53154444",
      "WilayahBengkel": "TANGERANG"
    }
  ],
  "Response": {
    "pxObjClass": "ASM-FW-ICMS-Data-ServiceFormClaim",
    "Status": "true"
  }
}
```

---

## Pindah Bengkel

### URL

| Environment | URL |
| --- | --- |
| GOLANG DEV | `http://192.168.10.210:8080/api/pelaporan/v1/pindah-bengkel` |

### Request Body

```json
{
  "AccessToken": "4fe40b15511f5265395a8bbfa4094ae2657e307b5f5eaeff070f3dfb2b8c62d1",
  "NoPelaporan": "PLP-03649",
  "NoPlat": "P1907KY",
  "DataBengkel": [
    {
      "IdBengkel": "0010001368",
      "NamaBengkel": "Arif Byna Selaras, Pt (Ahass Honda)",
      "WilayahBengkel": "JAKARTA TIMUR",
      "TELEPHONE": "085164545181",
      "Alamat": "JAKARTA TIMUR",
      "AlasanPindahBengkel": "ok pindah"
    }
  ]
}
```

### Response

```json
{
  "Response": {
    "NoPelaporan": "PLP-03649",
    "Status": "true"
  }
}
```

---

## Info Keunggulan Bengkel Tekno

Mengapa Bengkel Tekno?

1. Memiliki fasilitas *pick up & delivery service* — kendaraan bisa diambil, dibawa ke bengkel, atau diantar kembali tanpa perlu repot.
2. Fasilitas bengkel:
   - Luas 42.000 m², bisa menampung hingga 1.000 kendaraan.
   - Fasilitas perbaikan lengkap dengan 12 unit oven/spraybooth dan alat perbaikan rangka body/chasis (Car-O-Liner) teknologi Swedia yang terkomputerisasi.
   - Tenaga mekanik profesional, didukung pusat pelatihan dan pengembangan internal.
3. Fasilitas Online Tracking System melalui aplikasi mobile **e-Tekno** dan website `www.teknobodyrepair.id`, untuk:
   - Registrasi klaim
   - Booking pick up, delivery service, dan derek kendaraan
   - Memantau progress perbaikan kendaraan
   - Booking Tekno Home Service untuk maintenance di rumah nasabah
   - Mendapatkan informasi terbaru dari Bengkel Tekno
4. Menggunakan produk Roberlo untuk dempul — tipis, cepat kering, mempercepat proses perbaikan.
5. Menggunakan produk Roberlo untuk cat (*base coat*) dan pernis (*clear coat*) untuk hasil pengecatan maksimal.
6. Jaminan/garansi seumur hidup atas hasil pengecatan perbaikan kendaraan.
7. Perbaikan ulang gratis apabila ada keluhan/komplain terhadap hasil pengerjaan.
8. Tersedia fasilitas derek.
9. Benefit pengurangan 1x OR (Own Risk / Resiko Sendiri).

---

## Pelaporan Stolen

### Regis Pelaporan (Stolen)

#### URL

| Environment | URL |
| --- | --- |
| GOLANG DEV | `http://192.168.10.210:8080/api/pelaporan/v1/registrasi-stolen` |

#### Request Body

```json
{
  "App": "BARCODE",
  "AccessToken": "5b5e8b524df25f39cea8f3375b7cb55fd36a5f6124aaf9e61943fcf445a074a7",
  "EmailPelapor": "LAURENCIA.JORDAN@GMAIL.COM",
  "NoReferensiKlaim": "2025326143716-2008d870-a5d8-7c8e-a8f0-648695679d19",
  "TanggalKejadian": "20251211T134500.000 GMT",
  "CabangKlaim": "DKI JAKARTA",
  "Sourcecode": "PT ASM",
  "Kronologis": "Kendaraan hilang di parkiran",
  "NoTelepon": "0857346434643",
  "NamaTertanggung": "ADI SANTOSO",
  "NoPlat": "B572TQW",
  "NoPelaporan": "PLP-04119",
  "TanggalLapor": "20260203T084634.000 GMT",
  "NamaPengemudi": "Adi Santoso",
  "NoTelpPengemudi": "0824619737946",
  "AlamatPengemudi": "Jl. Berkah III No. 40 RT.01/RW. 10 Sudimara Timur, Ciledug, Tangerang",
  "ClaimQuestion": [
    {
      "Jawaban": "Pergi ke mall",
      "Label": "aktivitasTerakhir"
    },
    {
      "Jawaban": "Saya",
      "Label": "orangPertama"
    }
  ],
  "HubTertanggungPengemudi": null,
  "NamaPelapor": "Adi Santoso",
  "NoTelpPelapor": "0824619737946",
  "AlamatPelapor": "Jl. Berkah III No. 40 RT.01/RW. 10 Sudimara Timur, Ciledug, Tangerang",
  "HubTertanggungPengemudiLainnya": null,
  "EmailTertanggung": "Adisasa@gmail.com",
  "NoHPTertanggung": "0824619737946",
  "AlamatTertanggung": "Jl. Berkah III No. 40 RT.01/RW. 10 Sudimara Timur, Ciledug, Tangerang",
  "HubTertanggungPelapor": null,
  "HubTertanggungPelaporLainnya": null,
  "NoTelpKantor": null,
  "EmailPengemudi": "Adisasa@gmail.com"
}
```

> Catatan: `NoPelaporan` bisa diisi `null` jika ingin dibuatkan nomor baru secara otomatis.

#### Keterangan Field

| Property | Keterangan | Mandatory |
| --- | --- | --- |
| App | Diisi Nama Aplikasi: `BARCODE` | YA |
| AccessToken | Diisi Token | YA |
| NoPelaporan | Diisi No Pelaporan PLP | YA |
| NoPlat | Diisi No Plat | YA |
| NoReferensiKlaim | Diisi No Referensi dari setiap aplikasi | YA |
| CabangKlaim | Diisi Cabang Klaim yang dipilih | YA |
| Kronologis | Diisi Dengan Kronologis Kejadian Klaim | YA |
| NamaTertanggung | Diisi dengan Nama Tertanggung | YA |
| EmailTertanggung | Diisi dengan Email Tertanggung | YA |
| NoHPTertanggung | Diisi dengan No HP Tertanggung | YA |
| AlamatTertanggung | Diisi dengan Alamat Tertanggung | YA |
| HubTertanggungPelapor | `1` jika Ya, `0` jika Tidak | YA |
| HubTertanggungPelaporLainnya | Diisi sesuai pilihan jika `HubTertanggungPelapor` = Tidak | YA |
| NamaPelapor | Diisi dengan Nama Pelapor | YA |
| NoTelpPelapor | Diisi dengan No Telp Pelapor | YA |
| EmailPelapor | Diisi Data Email Pelapor | YA |
| AlamatPelapor | Diisi Data Alamat Pelapor | YA |
| NoTelepon | Diisi dengan Nomor Telepon Tertanggung | YA |
| Sourcecode | Diisi dengan Nama Asuransi: `PT ASM` (Testing) / `PT ASURANSI SINAR MAS` (LIVE) | YA |
| TanggalKejadian | Diisi dengan Tanggal Terjadinya Kejadian | YA |
| TanggalLapor | Diisi dengan Tanggal Lapor Klaim | YA |
| JenisSosmed | Diisi Dengan Jenis Sosial Media: INSTAGRAM, FACEBOOK, TIKTOK | YA |
| UsernameSosmed | Diisi Dengan Username Sosial Media | YA |
| AlamatDomisili | Diisi Dengan Alamat Domisili Tertanggung | YA |
| HubTertanggungPengemudi | `1` jika Ya, `0` jika Tidak | YA |
| HubTertanggungPengemudiLainnya | Diisi sesuai pilihan jika `HubTertanggungPengemudi` = Tidak | YA |
| NamaPengemudi | Diisi dengan data Nama Pengemudi | YA |
| NoTelpPengemudi | Diisi dengan data No Telp Pengemudi | YA |
| AlamatPengemudi | Diisi dengan data Alamat Pengemudi | YA |
| EmailPengemudi | Diisi dengan data Email Pengemudi | YA |
| ClaimQuestion | Lihat detail pertanyaan di bawah | YA |

##### Detail `ClaimQuestion`

Daftar pertanyaan (label, tipe input, dan opsi jika ada):

1. Aktivitas Terakhir Digunakan — *InputText* — label: `aktivitasTerakhir`
2. Orang pertama yang mengetahui kendaraan hilang? — *InputText* — label: `orangPertama`
3. Yang dilakukan pertama kali saat tahu kendaraan hilang? — *InputText* — label: `ygdilakukan`
4. Siapakah yang diminta bantuan pada saat kejadian? — *InputText* — label: `dimintabantuan`
5. Jumlah Kunci Kendaraan — *Picker* (`1`; `2`) — label: `jumlahKunci`
6. Apakah jenis kunci kendaraan Anda? — *RadioButton* (`Asli`; `Duplikat`) — label: `jenisKunciHilang`
7. Alasan Jumlah Kunci Kendaraan Tidak 2 — *InputText* — label: `alasanKunci`
8. Penggunaan Mobil — *RadioButton* (`Pribadi/Dinas`; `Komersil`) — label: `penggunaan`
9. Status Kepemilikan Kendaraan — *RadioButton* (`Milik Sendiri`; `Bukan Milik Sendiri`) — label: `kepemilikan`
10. Saksi Di Sekitar Lokasi Kejadian — *RadioButton* (`Ada`; `Tidak Ada`) — label: `saksi`
11. Nama Saksi — *InputText* — label: `namaSaksi`
12. Orang Yang Dicurigai Terkait Kejadian — *RadioButton* (`Ada`; `Tidak Ada`) — label: `orgdicurigai`
13. Nama Orang Yang Dicurigai — *InputText* — label: `namaOrgdicurigai`
14. Stang Dikunci Saat Terparkir — *RadioButton* (`Ya`; `Tidak`) — label: `stangdikunci`
15. Bagaimana keadaan/posisi kendaraan sebelum hilang? — *InputText* — label: `posisiKendaraan`

#### Response

```json
{
   "Response": {
          "CaseID": "PLP-04119",
          "NoReferensiKlaim": "2025326143716-2008d870-a5d8-7c8e-a8f0-648695679d19",
          "pzInsKey": "PLP-04119",
          "Status": "true"
    }
}
```

---

## Catatan Umum

- Semua endpoint bertipe REST dan berkomunikasi menggunakan format JSON.
- Setiap request (kecuali Get Token) memerlukan `AccessToken` yang didapat dari endpoint **Get Token**.
- `Sourcecode` membedakan environment: `PT ASM` untuk server Testing dan `PT ASURANSI SINAR MAS` untuk server LIVE.
- Contoh nilai (nomor telepon, token, alamat, dsb.) pada dokumen ini bersifat data uji (dummy) dan tidak boleh digunakan sebagai kredensial produksi.
