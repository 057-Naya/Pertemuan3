# Jawaban Tugas Bootstrap, Tailwind, JWT, Authentication, dan Authorization

## Soal 1 — Bandingkan Bootstrap dan Tailwind

Bootstrap menggunakan pendekatan **component-based**, yaitu komponen seperti card dan button sudah disediakan oleh framework. Sedangkan Tailwind CSS menggunakan pendekatan **utility-first**, yaitu tampilan dibuat dengan menggabungkan banyak class utility.

### Class utama Bootstrap

| Kebutuhan    | Bootstrap     |
| ------------ | ------------- |
| Card         | `card`        |
| Isi card     | `card-body`   |
| Judul        | `card-title`  |
| Teks         | `card-text`   |
| Tombol       | `btn`         |
| Tombol utama | `btn-primary` |

Contoh:

```html
<div class="card">
  <div class="card-body">
    <h5 class="card-title">Biodata Mahasiswa</h5>
    <p class="card-text">Nama: Naya</p>
    <button class="btn btn-primary">Lihat Biodata</button>
  </div>
</div>
```

### Class utama Tailwind CSS

Tailwind tidak menyediakan class khusus seperti `card` atau `btn`. Tampilan dibuat menggunakan utility class.

Contoh:

```html
<div class="bg-white rounded-lg shadow p-4">
  <h5 class="text-xl font-bold">Biodata Mahasiswa</h5>
  <p class="text-gray-600">Nama: Naya</p>
  <button class="bg-blue-500 text-white px-4 py-2 rounded">
    Lihat Biodata
  </button>
</div>
```

Menurut saya, **Bootstrap lebih mudah digunakan oleh pemula** karena komponen seperti card dan button sudah tersedia sehingga tidak perlu menulis banyak class utility. Tailwind lebih fleksibel untuk membuat desain khusus, tetapi membutuhkan pemahaman lebih banyak terhadap utility class.

---

## Soal 2 — Rancang Satu Kartu Biodata dengan Dua Pendekatan

### Sketsa Kartu Biodata

```text
┌─────────────────────────────┐
│                             │
│          [ FOTO ]           │
│                             │
│     Nurul Maudy Apriyani    │
│     NIM: 2024520057         │
│                             │
│      [ Lihat Biodata ]      │
│                             │
└─────────────────────────────┘
```

### Versi Component

Contoh menggunakan Bootstrap:

```html
<div class="card" style="width: 18rem;">
  <img src="foto.jpg" class="card-img-top" alt="Foto">

  <div class="card-body">
    <h5 class="card-title">Nurul Maudy Apriyani</h5>
    <p class="card-text">NIM: 2024520057</p>

    <button class="btn btn-primary">
      Lihat Biodata
    </button>
  </div>
</div>
```

Class yang digunakan adalah:

```text
card
card-img-top
card-body
card-title
card-text
btn
btn-primary
```

Pada Bootstrap, aturan CSS tambahan yang perlu ditulis sendiri untuk tampilan dasar adalah **0 aturan**, karena Bootstrap sudah menyediakan CSS untuk komponen tersebut.

### Versi Utility

Contoh menggunakan Tailwind CSS:

```html
<div class="w-72 bg-white rounded-lg shadow-md overflow-hidden">
  <img
    src="foto.jpg"
    alt="Foto"
    class="w-full h-48 object-cover"
  >

  <div class="p-4">
    <h5 class="text-xl font-bold text-gray-800">
      Nurul Maudy Apriyani
    </h5>

    <p class="text-gray-600">
      NIM: 2024520057
    </p>

    <button
      class="mt-3 px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
    >
      Lihat Biodata
    </button>
  </div>
</div>
```

Jumlah utility class pada contoh tersebut adalah **20 class**, yaitu:

* Container: 5 class
* Gambar: 4 class
* Isi: 1 class
* Judul: 3 class
* Teks: 1 class
* Tombol: 6 class

**Total: 20 class utility.**

Versi **Tailwind lebih mudah diubah warnanya** karena warna dapat langsung diubah melalui utility class, misalnya `bg-blue-500` menjadi `bg-red-500`.

---

## Soal 3 — Amati Isi Token JWT

Token yang diberikan:

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

JWT memiliki **3 bagian** yang dipisahkan oleh tanda titik (`.`), yaitu:

```text
HEADER.PAYLOAD.SIGNATURE
```

### Header

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

Header menunjukkan algoritma yang digunakan yaitu `HS256` dan tipe token yaitu `JWT`.

### Payload

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
```

Nama data yang terlihat pada payload adalah:

* `sub`
* `name`
* `iat`

### Signature

Bagian ketiga adalah signature:

```text
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

Signature digunakan untuk membantu memastikan bahwa token tidak dimodifikasi.

Password tidak boleh disimpan di dalam payload JWT karena payload JWT dapat di-decode dan dibaca oleh pihak yang memperoleh token. Payload bukan tempat penyimpanan data rahasia. Password seharusnya disimpan di database dalam bentuk **password hash** menggunakan algoritma yang aman seperti Argon2id atau bcrypt.

Jadi, **password tidak boleh dimasukkan ke dalam JWT karena isi payload dapat dibaca dan bukan merupakan penyimpanan terenkripsi.**

---

## Soal 4 — Analogi Gerbang Kampus

Authentication adalah proses untuk memeriksa **identitas seseorang**.

Dalam analogi gerbang UNIRA, mahasiswa menunjukkan KTM atau identitas kepada petugas. Petugas kemudian memeriksa apakah identitas tersebut valid.

```text
Mahasiswa
    ↓
Menunjukkan KTM
    ↓
Identitas diperiksa
    ↓
Identitas valid
    ↓
Authentication berhasil
```

Authentication menjawab pertanyaan:

> **"Kamu siapa?"**

Sedangkan authorization adalah proses untuk memeriksa **hak akses seseorang**.

Setelah identitas mahasiswa diketahui, ketika mahasiswa ingin masuk ke ruang server laboratorium, petugas memeriksa apakah mahasiswa tersebut memiliki izin untuk masuk.

```text
Identitas sudah diketahui
          ↓
     Cek role/izin
          ↓
  Memiliki izin server?
       ↙       ↘
     Ya        Tidak
      ↓          ↓
  Diizinkan    Ditolak
```

Authorization menjawab pertanyaan:

> **"Kamu boleh melakukan apa?"**

Contohnya, seorang mahasiswa berhasil login menggunakan NIM dan password yang benar sehingga authentication berhasil. Namun, mahasiswa tersebut memiliki role `mahasiswa` dan tidak mempunyai permission untuk membuka ruang server yang hanya dapat diakses oleh `admin`.

Maka:

```text
Authentication = Berhasil
Authorization  = Gagal
```

Akses tetap ditolak.

---

## Soal 5 — Peran di Aplikasi Nyata

Saya memilih **GitHub** sebagai contoh aplikasi.

### Role dan Fitur

| Role                  | Contoh kemampuan                             |
| --------------------- | -------------------------------------------- |
| Owner                 | Mengelola repository dan pengaturan utama    |
| Admin/Maintainer      | Mengelola repository dan pengaturan tertentu |
| Contributor/Developer | Membuat perubahan kode dan Pull Request      |

Contoh fitur yang hanya boleh digunakan oleh role tertentu adalah **mengubah pengaturan repository atau menghapus repository**. Fitur tersebut tidak boleh diberikan kepada contributor biasa.

### Pengguna Belum Login

Jika pengguna belum login dan mencoba mengakses endpoint yang membutuhkan authentication, server dapat memberikan:

```http
401 Unauthorized
```

Alasannya adalah identitas pengguna belum berhasil diverifikasi.

```text
Request
   ↓
Tidak ada session/token valid
   ↓
Authentication gagal
   ↓
401 Unauthorized
```

### Pengguna Sudah Login Tetapi Tidak Memiliki Izin

Jika pengguna sudah login tetapi mencoba mengakses fitur yang tidak sesuai dengan role atau permission-nya, server memberikan:

```http
403 Forbidden
```

Alasannya adalah identitas pengguna sudah diketahui, tetapi pengguna tidak mempunyai hak untuk melakukan tindakan tersebut.

```text
Request
   ↓
Token valid
   ↓
Authentication berhasil
   ↓
Role tidak memiliki permission
   ↓
403 Forbidden
```

### Perbedaan 401 dan 403

| Status | Kondisi                                | Keterangan           |
| ------ | -------------------------------------- | -------------------- |
| `401`  | Belum login atau token tidak valid     | Authentication gagal |
| `403`  | Sudah login tetapi tidak memiliki izin | Authorization gagal  |

### Kesimpulan

**401 Unauthorized** digunakan ketika pengguna belum berhasil melakukan authentication, sedangkan **403 Forbidden** digunakan ketika pengguna sudah terautentikasi tetapi tidak mempunyai authorization atau hak akses terhadap resource yang diminta.
