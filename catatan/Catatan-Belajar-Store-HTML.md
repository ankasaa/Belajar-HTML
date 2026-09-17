# Catatan Belajar: Product Page Toko Online (HTML5 + CSS Border)

## Deskripsi Proyek

Kode HTML ini membangun halaman **Product Page** untuk "Andika Tech Store" yang menjual laptop. Ini adalah latihan yang mencakup:

- **Struktur Semantik HTML5**: Penggunaan `<header>`, `<main>`, `<section>`, `<footer>` untuk membagi halaman menjadi area yang bermakna.
- **Tabel Spesifikasi**: Penggunaan `<table>` dengan `<thead>`, `<tbody>`, dan `<tfoot>` untuk menampilkan data spesifikasi produk secara terstruktur.
- **Form Pembelian**: Penggunaan `<fieldset>`, `<label>`, `<input>`, dan `<select>` untuk form pemesanan produk.
- **CSS Border Tabel**: Penggunaan `border`, `border-collapse`, dan `border-bottom` untuk memberi garis pada tabel.

### [Screenshot Hasil Akhir]

> _Sisipkan gambar tangkapan layar (screenshot) hasil render halaman ini di browser di sini._

````
[ Placeholder: Screenshot Store.html di browser ]
````

---

## Review Kesalahan & Pelajaran Penting

### 1. Kesalahan: `<h3>` di Dalam `<ul>`

**Yang terjadi:**
Awalnya saya menaruh tag `<h3>` sebagai **anak langsung** dari `<ul>`, tepatnya sebelum tag `<li>`.

**Mengapa ini salah?**
Dalam HTML, element yang boleh menjadi anak langsung dari `<ul>` hanyalah `<li>`. Element heading seperti `<h3>` **tidak valid** jika diletakkan di dalam `<ul>`. Browser akan tetap merender, tapi strukturnya tidak semantik dan bisa menyebabkan masalah styling.

**Snippet Kode:**

```html
<!-- ❌ SALAH: h3 di dalam ul -->
<ul>
    <h3>Fitur Utama:</h3>
    <li>Performa cepat dengan NVMe SSD</li>
    <li>Desain ringkas dan ringan</li>
</ul>
```

```html
<!-- ✔️ BENAR: h3 di luar ul -->
<h3>Fitur Utama:</h3>
<ul>
    <li>Performa cepat dengan NVMe SSD</li>
    <li>Desain ringkas dan ringan</li>
</ul>
```

**Aturan emas:**

```
<ul> atau <ol>
  └── <li>    (hanya <li> yang boleh menjadi anak langsung)
        └── <h3>, <p>, dll (heading/teks boleh di DALAM <li>)
```

---

### 2. Kesalahan: `type="angka"` Tidak Valid

**Yang terjadi:**
Awalnya saya menggunakan `type="angka"` pada element `<input>` untuk input jumlah pembelian.

**Mengapa ini salah?**
`type="angka"` **tidak ada** dalam spesifikasi HTML. Yang benar adalah `type="number"`. Browser akan mengabaikan type yang tidak dikenal dan memperlakukannya sebagai `type="text"`, sehingga tidak ada validasi angka atau tombol spin (+/-) yang muncul.

**Snippet Kode:**

```html
<!-- ❌ SALAH: type="angka" tidak ada -->
<input type="angka" id="angka">
```

```html
<!-- ✔️ BENAR: type="number" dengan validasi -->
<input type="number" id="angka" min="1" value="1">
```

**Tabel Referensi `type` Input:**

| `type` | Fungsi |
|--------|--------|
| `text` | Teks biasa |
| `number` | Hanya angka, muncul tombol +/- |
| `email` | Validasi format email |
| `password` | Teks tersembunyi (•••) |
| `button` | Tombol tanpa aksi default |

---

### 3. Kesalahan: `width: 15%` Terlalu Kecil

**Yang terjadi:**
Pada inline style `<table>`, saya menggunakan `width: 15%` yang membuat tabel menjadi sangat sempit.

**Mengapa ini masalah?**
Lebar 15% dari layar terlalu kecil untuk menampung konten seperti "Intel Core i3 11th Gen". Teks akan terpotong atau ter-wrap terlalu banyak, membuat tabel sulit dibaca.

**Snippet Kode:**

```html
<!-- ❌ SALAH: width terlalu kecil -->
<table style="border-collapse: collapse; width: 15%;">
```

```html
<!-- ✔️ BENAR: width sesuai kebutuhan -->
<table style="border-collapse: collapse; width: 100%;">
```

**Tips Memilih Width:**

| Nilai | Kapan Digunakan |
|-------|-----------------|
| `width: 100%` | Tabel mengisi seluruh lebar container |
| `width: 500px` | Lebar tetap, tidak berubah |
| `width: auto` | Lebar menyesuaikan konten |

---

### 4. Kesalahan: Inline Style Background Color

**Yang terjadi:**
Awalnya saya memberikan `background-color` langsung pada tag `<thead>`, `<tbody>`, dan `<tfoot>` menggunakan atribut `style`.

**Mengapa ini kurang baik?**
Inline style sulit dikelola jika ada banyak elemen. Jika ingin mengubah warna, harus mengubah satu per satu di setiap tag. Lebih baik gunakan CSS di `<head>` supaya terpusat dan mudah diubah.

**Snippet Kode:**

```html
<!-- ❌ KURANG BAIK: Inline style di setiap tag -->
<thead style="background-color: aqua;">
<tbody style="background-color: pink;">
<tfoot style="background-color: yellowgreen;">
```

```html
<!-- ✔️ LEBIH BAIK: CSS terpusat di <head> -->
<style>
    thead { background-color: #f0f0f0; }
    tbody { background-color: #ffffff; }
    tfoot { background-color: #f9f9f9; }
</style>
```

**Keuntungan CSS Terpusat:**
- Mudah diubah di satu tempat
- Konsisten di seluruh halaman
- Bisa menggunakan variabel CSS (nanti di materi lanjutan)

---

### 5. Kesalahan: `<blockquote>` untuk Review

**Yang terjadi:**
Awalnya saya menggunakan tag `<blockquote>` untuk menampilkan ulasan/preview dari pembeli.

**Mengapa ini kurang tepat?**
`<blockquote>` secara semantik digunakan untuk **kutipan panjang dari sumber lain** (misal: kutipan buku, artikel). Review produk lebih tepat menggunakan `<p>` atau `<div>` dengan class khusus.

**Snippet Kode:**

```html
<!-- ❌ KURANG TEPAT: blockquote untuk review -->
<blockquote>
    "Mantap!" - Budi
    "Pengiriman cepat!" - Siti
</blockquote>
```

```html
<!-- ✔️ LEBIH TEPAT: p untuk review -->
<div class="reviews">
    <p>"Mantap! Dipakai untuk buka banyak tab W3Schools dan koding di VS Code sangat lancar." - Budi</p>
    <p>"Pengiriman cepat, packing aman. Sangat direkomendasikan!" - Siti</p>
</div>
```

---

## Bedah Kode: CSS Border Tabel

### Masalah: Border di `<table>` Tidak Muncul di Cell

Banyak pemula (termasuk saya) mengira menambahkan `border` pada `<table>` akan membuat semua cell memiliki garis. **Tidak.** Border di `<table>` hanya membuat garis di **luar tabel saja**.

```html
<!-- ❌ INI TIDAK MEMBUAT GARIS DI DALAM TABEL -->
<table style="border: 1px solid black;">
    <td>Prosesor</td>        <!-- td ini TIDAK punya border -->
    <td>Intel Core i3</td>   <!-- td ini juga TIDAK punya border -->
</table>
```

### Solusi: Style `<td>` dan `<th>` secara Terpisah

```html
<!-- ✔️ BENAR: border diberikan ke td dan th -->
<table style="border-collapse: collapse;">
    <thead>
        <tr>
            <th>Komponen</th>
            <th>Keterangan</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Prosesor</td>
            <td>Intel Core i3 11th Gen</td>
        </tr>
    </tbody>
</table>
```

```css
th, td {
    border: 1px solid black;  /* garis di semua sisi */
    padding: 10px;
}
```

### Jenis Border yang Bisa Digunakan

| Properti | Hasil | Contoh Penggunaan |
|----------|-------|-------------------|
| `border: 1px solid black` | Kotak penuh (atas+bawah+kiri+kanan) | Tabel format kotak |
| `border-bottom: 1px solid black` | Garis bawah saja | Tabel minimalis seperti gambar |
| `border-top: 1px solid black` | Garis atas saja | Pisah section |
| `border-left: 1px solid black` | Garis kiri saja | Kolom pemisah |
| `border-right: 1px solid black` | Garis kanan saja | Kolom pemisah |

### Fungsi `border-collapse: collapse`

Tanpa `border-collapse: collapse`, setiap cell memiliki border sendiri-sendiri sehingga terlihat **ganda/tebel** di antara cell. Dengan `border-collapse: collapse`, border antar cell digabungkan menjadi satu garis tipis yang rapi.

```css
/* Tanpa border-collapse: border ganda */
th, td { border: 1px solid black; }

/* Dengan border-collapse: border rapi */
table { border-collapse: collapse; }
th, td { border: 1px solid black; }
```

### Contoh: Tabel dengan Horizontal Saja (Seperti Gambar)

```css
table {
    border-collapse: collapse;
    width: 100%;
}
th, td {
    border-bottom: 1px solid #aaa;  /* hanya garis bawah */
    padding: 10px 15px;
    text-align: left;
}
th {
    font-weight: bold;
    border-bottom: 2px solid #888;  /* garis header lebih tebal */
}
```

---

## Bedah Kode: Fungsi Tag Tabel

### `<thead>`

```html
<thead>
    <tr>
        <th>Komponen</th>
        <th>Keterangan</th>
    </tr>
</thead>
```

**Fungsi:** Membungkus baris **judul kolom** dari tabel.

**Penting untuk:**
- **SEO**: Google mengenali ini sebagai header tabel
- **Screen reader**: Saat navigasi tabel, pengguna langsung tahu kolom apa saja yang ada
- **CSS**: Bisa distyling terpisah dari data (misal: background berbeda, teks tebal)

---

### `<tbody>`

```html
<tbody>
    <tr>
        <td>Prosesor</td>
        <td>Intel Core i3 11th Gen</td>
    </tr>
</tbody>
```

**Fungsi:** Membungkus baris **isi data** dari tabel.

**Penting untuk:**
- **Struktur**: Memisahkan data dari header secara jelas
- **JavaScript**: Bisa diakses terpisah untuk manipulasi data
- **CSS**: Bisa distyling terpisah (zebra stripe, hover, dll)

**Penting:** Cukup **1 `<tbody>`** yang membungkus semua baris data. Jangan membuat banyak `<tbody>` terpisah.

---

### `<tfoot>`

```html
<tfoot>
    <tr>
        <td>Sistem Operasi</td>
        <td>Windows 11</td>
    </tr>
</tfoot>
```

**Fungsi:** Membungkus baris **footer/rekap** dari tabel (misal: total, kesimpulan).

**Penting untuk:**
- **Semantik**: Browser dan screen reader mengenali ini sebagai bagian akhir tabel
- **CSS**: Bisa distyling terpisah (background berbeda, teks tebal, dll)

---

### `<th>` vs `<td>`

| Tag | Fungsi | Default CSS |
|-----|--------|-------------|
| `<th>` | Header kolom (judul) | Tebal, center |
| `<td>` | Data cell (isi) | Normal, left |

**Aturan emas:**

```
<table>
  ├── <thead>    → baris judul pakai <th>
  ├── <tbody>    → baris data pakai <td>
  └── <tfoot>    → baris rekap pakai <td> atau <th>
</table>
```

---

## Refleksi Pribadi

> Latihan Product Page ini mengajarkan saya bahwa **border pada `<table>` tidak otomatis muncul di cell**. Saya harus memahami bahwa setiap element HTML memiliki scope styling masing-masing — border di parent tidak mewarisi ke child secara otomatis. Saya juga belajar bahwa **tidak semua tag bisa diletakkan di dalam tag lain** — `<h3>` tidak boleh di dalam `<ul>`, dan `<blockquote>` bukan untuk review produk. Yang paling penting: **struktur HTML yang benar adalah fondasi CSS yang rapi**. Jika HTML-nya berantakan, CSS-nya akan sulit.

---

## Jembatan ke Materi Selanjutnya (Next Steps)

Dengan struktur tabel yang sudah benar (`<thead>`, `<tbody>`, `<tfoot>`) dan pemahaman tentang CSS border, langkah selanjutnya adalah:

### 1. CSS Layout dengan Flexbox/Grid

```css
.product-overview {
    display: flex;
    gap: 20px;
}
.product-overview img {
    flex-shrink: 0;
}
```

### 2. CSS Variables untuk Warna Konsisten

```css
:root {
    --primary-color: #333;
    --border-color: #aaa;
    --bg-light: #f5f5f5;
}
th, td {
    border-bottom: 1px solid var(--border-color);
}
```

### 3. Responsive Table

```css
@media (max-width: 600px) {
    table {
        font-size: 14px;
    }
    th, td {
        padding: 8px;
    }
}
```

**Catatan untuk diri sendiri:** Susun HTML dengan benar terlebih dahulu, barulah CSS akan bekerja dengan mudah. HTML yang berantakan = CSS yang rumit. Dan ingat: **setiap tag punya aturan mainnya sendiri** — pelajari dulu siapa yang boleh menjadi anak siapa sebelum menulis kode.
