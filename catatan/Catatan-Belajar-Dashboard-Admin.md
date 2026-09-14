# Catatan Belajar: Struktur Dashboard Admin (HTML5 Lanjutan)

## Deskripsi Proyek

Kode HTML ini membangun halaman **Dashboard Admin** untuk sistem informasi akademik. Ini adalah latihan tingkat lanjut yang mencakup:

- **Layout Bersarang (Nested Layout)**: Struktur `<div>` bertingkat untuk membagi halaman menjadi area header, sidebar, dan konten utama — persiapan untuk styling CSS nanti.
- **Tabel Tingkat Lanjut**: Penggunaan `<thead>` dan `<tbody>` untuk memisahkan judul kolom dari isi data secara semantik.
- **Formulir Tingkat Lanjut**: Penggunaan `<fieldset>` dan `<legend>` untuk mengelompokkan input, serta radio button dan checkbox untuk input interaktif.

### [Screenshot Hasil Akhir]
> _Sisipkan gambar tangkapan layar (screenshot) hasil render halaman ini di browser di sini. Programmer sangat visual — melihat layout akan langsung memancing ingatan tentang bagaimana struktur HTML-nya dibangun._

```
[ Placeholder: Screenshot Dashboard Admin di browser ]
```

---

## Review Kesalahan & Pelajaran Penting

### 1. Kesalahan Hierarki Tabel

**Yang terjadi:**
Awalnya saya menaruh `<section>` di **dalam** `<thead>`, dan menaruh `<table>` di **dalam** `<tbody>`.

**Mengapa ini salah?**
Dalam HTML, `<thead>` dan `<tbody>` adalah **anak langsung** dari `<table>`. Mereka tidak boleh membungkus elemen lain di luar tabel. Yang terjadi pada kode lama adalah kebalikan dari hierarki yang benar.

**Snippet Kode:**

```html
<!-- ❌ SALAH: Section di dalam thead, table di dalam tbody -->
<thead>
    Data Mahasiswa Aktif
    <section class="form-section">
        <tbody>
            <table>
                ...
            </table>
        </tbody>
    </section>
</thead>
```

```html
<!-- ✔️ BENAR: thead dan tbody adalah anak dari table -->
<table>
    <thead>
        <tr>
            <th>NIM</th>
            <th>Nama</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>26001</td>
            <td>Budi</td>
        </tr>
    </tbody>
</table>
```

**Aturan emas:**
```
<table>
  ├── <thead>   (hanya berisi baris judul <tr> + <th>)
  ├── <tbody>   (hanya berisi baris data <tr> + <td>)
  └── <tfoot>   (opsional: total/rekap)
</table>
```

---

### 2. Kesalahan Logika Radio Button

**Yang terjadi:**
Awalnya saya memberikan atribut `name` yang **berbeda** pada setiap radio button:
- Radio "Reguler" → `name="Reguler"`
- Radio "Beasiswa" → `name="Beasiswa"`

**Mengapa ini salah?**
Radio button bekerja dengan prinsip **satu grup, satu pilihan**. Grup ditentukan oleh kesamaan atribut `name`. Jika `name`-nya berbeda, maka keduanya bisa dipilih **bersamaan** — padahal konsep radio button adalah memilih **salah satu saja**.

**Snippet Kode:**

```html
<!-- ❌ SALAH: name berbeda, bisa pilih keduanya sekaligus -->
<input type="radio" name="Reguler" id="reguler">
<input type="radio" name="Beasiswa" id="beasiswa">
```

```html
<!-- ✔️ BENAR: name sama, hanya bisa pilih salah satu -->
<input type="radio" name="jalur_masuk" id="reguler" value="Reguler">
<label for="reguler">Reguler</label>

<input type="radio" name="jalur_masuk" id="beasiswa" value="Beasiswa">
<label for="beasiswa">Beasiswa</label>
```

**Prinsipnya:**
| Atribut | Fungsi |
|---------|--------|
| `name` | Menentukan **grup** radio button (wajib sama untuk satu grup) |
| `value` | Nilai yang dikirim saat form disubmit |
| `id` | Untuk menghubungkan dengan `<label>` via atribut `for` |

---

### 3. Lupa Tag `<form>`

**Yang terjadi:**
Awalnya saya membuat input-formulir dan fieldset tapi **lupa membungkusnya** dengan tag `<form>`.

**Mengapa ini krusial?**
Tag `<form>` adalah **wadah** yang memberitahu browser bahwa semua input di dalamnya adalah bagian dari satu form yang akan dikirim ke server. Tanpa `<form>`:

- Tombol `<input type="submit">` **tidak akan berfungsi**
- Data **tidak akan dikirim** ke mana pun
- Atribut `action` dan `method` **tidak bisa diterapkan**

**Snippet Kode:**

```html
<!-- ❌ SALAH: Input tanpa pembungkus form -->
<section>
    <fieldset>
        <legend>Form Registrasi</legend>
        <input type="number" name="nim">
        <input type="submit" value="Simpan">
    </fieldset>
</section>
```

```html
<!-- ✔️ BENAR: Semua input dibungkus dengan form -->
<form action="#" method="POST">
    <fieldset>
        <legend>Form Registrasi</legend>
        <input type="number" name="nim">
        <input type="submit" value="Simpan">
    </fieldset>
</form>
```

---

### 4. Kesalahan Penutup `<div>` Layout

**Yang terjadi:**
Awalnya saya menutup `<div class="app-container">` terlalu cepat (di baris 28), sehingga `<main>` dan `<footer>` **terlempar keluar** dari layout utama.

**Mengapa ini fatal untuk CSS?**
Ketika nanti kita styling dengan CSS Flexbox atau Grid, parent container `<div class="app-container">` dan `<div class="dashboard-layout">` harus **membungkus semua elemen** yang ingin diatur tata letaknya. Jika ditutup terlalu cepat, elemen di luar tidak akan terpengaruh styling.

**Snippet Kode:**

```html
<!-- ❌ SALAH: app-container ditutup sebelum main & footer -->
<div class="app-container">
    <header>...</header>
    <div class="dashboard-layout">
        <aside>...</aside>
    </div>
</div>  <!-- ← ditutup terlalu cepat! -->
<main class="main-content">...</main>  <!-- keluar dari layout -->
<footer>...</footer>  <!-- keluar dari layout -->
```

```html
<!-- ✔️ BENAR: Semua elemen di dalam app-container -->
<div class="app-container">
    <header>...</header>
    <div class="dashboard-layout">
        <aside>...</aside>
        <main class="main-content">...</main>
    </div>  <!-- penutup dashboard-layout -->
    <footer>...</footer>
</div>  <!-- penutup app-container, TUTUP DI SINI -->
```

**Tips:** Saat menulis HTML bersarang, **selalu komentari** setiap tag penutup:

```html
</div> <!-- Penutup dashboard-layout -->
</div> <!-- Penutup app-container -->
```

---

## Bedah Kode: Fungsi Tag Lanjutan

### `<fieldset>`
```html
<fieldset>
    <legend>Form Registrasi</legend>
    <!-- input-input di sini -->
</fieldset>
```
**Fungsi:** Membungkus sekelompok input yang **saling berkaitan** secara visual dan semantik. Browser biasanya menampilkannya dengan border di sekeliling grup input.

**Penting untuk:**
- **Aksesibilitas**: Screen reader mengenali ini sebagai satu grup input
- **SEO**: Mesin pemaham struktur form
- **Visual**: Memudahkan pengguna memahami pengelompokan form

---

### `<legend>`
```html
<legend>Form Registrasi</legend>
```
**Fungsi:** Memberikan **judul** atau label pada `<fieldset>`. Biasanya muncul di tepi border fieldset.

**Penting untuk:**
- **Screen reader**: Membacakan judul grup sebelum masuk ke input
- **Konteks**: Pengguna langsung tahu grup input ini untuk apa

---

### `<thead>`
```html
<thead>
    <tr>
        <th>NIM</th>
        <th>Nama</th>
    </tr>
</thead>
```
**Fungsi:** Membungkus baris **judul kolom** dari tabel.

**Penting untuk:**
- **SEO**: Google mengenali ini sebagai header tabel
- **Screen reader**: Saat navigasi tabel, pengguna langsung tahu kolom apa saja yang ada
- **CSS**: Bisa distyling terpisah dari data (misal: background berbeda)

---

### `<tbody>`
```html
<tbody>
    <tr>
        <td>26001</td>
        <td>Budi Santoso</td>
    </tr>
</tbody>
```
**Fungsi:** Membungkus baris **isi data** dari tabel.

**Penting untuk:**
- **Struktur**: Memisahkan data dari header secara jelas
- **JavaScript**: Bisa diakses terpisah untuk manipulasi data
- **CSS**: Bisa distyling terpisah (zebra stripe, hover, dll)

---

## Refleksi Pribadi

> Latihan Dashboard Admin ini mengajarkan saya bahwa **ketelitian menutup tag** sama pentingnya dengan ketelitian membuka tag. Kesalahan kecil seperti menutup `<div>` terlalu cepat bisa merusak seluruh struktur layout. Saya juga belajar bahwa radio button punya logika khusus — atribut `name` bukan sekadar penamaan, tapi menentukan **grup** pilihan. Dan yang paling mendasar: **tidak ada yang namanya form tanpa tag `<form>`**. Semua input harus punya wadah.

---

## Jembatan ke Materi Selanjutnya (Next Steps)

Pembungkusan elemen dengan `<div class="dashboard-layout">` bukan tanpa alasan. Ini adalah **persiapan krusial** untuk langkah selanjutnya: **CSS Flexbox dan CSS Grid**.

Dengan struktur yang sudah benar:
```html
<div class="dashboard-layout">
    <aside class="side-bar">...</aside>
    <main class="main-content">...</main>
</div>
```

Kita bisa dengan mudah membuat sidebar dan konten utama **berdampingan** menggunakan:
```css
.dashboard-layout {
    display: flex;        /* atau display: grid; */
}
.side-bar { width: 250px; }
.main-content { flex: 1; }
```

**Catatan untuk diri sendiri:** Susun HTML dengan benar terlebih dahulu, barulah CSS akan bekerja dengan mudah. HTML yang berantakan = CSS yang rumit.
