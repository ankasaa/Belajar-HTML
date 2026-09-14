# Catatan Belajar: Proyek Review Game Roblox

## Deskripsi Proyek

Kode HTML ini merupakan halaman ulasan sederhana untuk game **Roblox**. Halaman ini memanfaatkan beberapa fitur penting dalam HTML:

- **Semantic Tag**: Menggunakan tag `<header>`, `<footer>`, dan `<div>` untuk memberikan struktur yang bermakna pada konten.
- **Tabel (`<table>`)**: Menampilkan informasi game (rilis, genre, rating) dalam format baris dan kolom yang rapi.
- **Embed Media**: Menyisipkan video YouTube menggunakan tag `<iframe>` serta gambar dari URL eksternal menggunakan tag `<img>`.

---

## Review Kesalahan & Pelajaran Penting

### 1. Kesalahan Struktur Tabel: `<td>` di Dalam `<th>`

**Yang terjadi:**
Awalnya, saya memasukkan tag `<td>` ke dalam tag `<th>` di dalam satu baris tabel.

**Mengapa ini salah?**
Dalam HTML, `<th>` (table header) dan `<td>` (table data) adalah **saudara sejajar** di dalam satu `<tr>` (table row). Keduanya tidak boleh bertingkat (nested). `<th>` berfungsi sebagai judul kolom atau baris, sedangkan `<td>` berfungsi sebagai isi data. Jika `<td>` dimasukkan ke dalam `<th>`, maka secara semantik dan visual akan salah karena browser akan menganggap data tersebut sebagai bagian dari header.

**Struktur yang benar:**

```html
<tr>
  <th>Rilis :</th>
  <td>2010</td>
</tr>
```

**Prinsipnya:** Setiap `<tr>` berisi satu set `<th>` atau `<td>` yang **sejajar**, bukan saling bersarang.

---

### 2. Kesalahan Iframe YouTube: Link Watch vs Embed

**Yang terjadi:**
Awalnya saya menggunakan link YouTube dengan format watch, seperti:
```
https://www.youtube.com/watch?v=sme76WoJ_-U
```

**Mengapa ini salah?**
Link format `watch` adalah halaman video biasa (termasuk komentar, rekomendasi, dan UI YouTube). Tag `<iframe>` membutuhkan **link embed** yang dikhususkan untuk disematkan di halaman web. Jika link watch digunakan, video tidak akan bisa ditampilkan di dalam iframe.

**Solusi:**
Gunakan format embed:
```
https://www.youtube.com/embed/sme76WoJ_-U
```

**Cara mengubah:** Ganti `watch?v=` menjadi `embed/` pada URL video YouTube.

---

### 3. Penggunaan Semantic Tag yang Kurang Optimal

**Yang terjadi:**
Pada versi awal, seluruh konten hanya dibungkus `<div>` tanpa struktur semantik yang jelas.

**Mengapa ini penting?**
Tag semantik seperti `<article>`, `<section>`, dan `<main>` memberikan **makna** pada konten bagi browser, screen reader, dan mesin pencari (SEO). Tanpa tag semantik, struktur halaman sulit dipahami secara otomatis.

**Perbaikan yang diterapkan:**
- `<header>` digunakan untuk bagian judul halaman.
- `<footer>` digunakan untuk informasi hak cipta di akhir halaman.
- Konten utama sebaiknya dibungkus dengan `<main>` atau `<article>`.

**Contoh penulisan yang lebih baik:**

```html
<main>
  <article>
    <header>
      <h1>Ulasan tentang Game Roblox</h1>
    </header>
    <p>Ditulis oleh: Andika | September 2026</p>
    <!-- konten lainnya -->
  </article>
</main>
```

---

## Format Tabel yang Benar

Berikut contoh lengkap struktur tabel yang valid:

```html
<table border="1">
  <tr>
    <th>Rilis</th>
    <th>Genre</th>
    <th>Rating</th>
  </tr>
  <tr>
    <td>2010</td>
    <td>Sandbox</td>
    <td>Bintang 5</td>
  </tr>
</table>
```

| Tag    | Fungsi                        | Contoh Isi            |
| ------ | ----------------------------- | --------------------- |
| `<tr>` | Membungkus satu baris         | -                     |
| `<th>` | Header kolom/baris (tebal)    | Rilis, Genre, Rating  |
| `<td>` | Isi data sel                  | 2010, Sandbox, Bintang 5 |

---

## Refleksi Pribadi

> Saya menyadari bahwa detail kecil dalam HTML seperti struktur tabel dan URL embed sangat mempengaruhi hasil akhir. Saya belajar untuk selalu mengecek **validitas struktur tag** dan **format URL** sebelum menggunakannya. Selain itu, penggunaan semantic tag ternyata bukan hanya soal estetika kode, tapi juga penting untuk **aksesibilitas** dan **SEO**.
