# Catatan Belajar: Struktur Halaman Blog Teknologi (Artikel & Sidebar)

## Deskripsi Proyek

Kode HTML ini membangun halaman blog sederhana bernama **DevBlog - Catatan Koding**. Fokus utamanya adalah penerapan **HTML5 Semantic Tags** untuk membuat layout web yang terstruktur.

Terdapat tiga bagian utama: navigasi di atas, konten artikel utama di tengah, dan footer di bawah. Di dalam artikel juga terdapat sidebar (`<aside`) yang memuat profil penulis. Penggunaan tag semantik membuat struktur ini mudah dipahami oleh browser, mesin pencari (SEO), dan screen reader.

---

## Review Kesalahan & Pelajaran Penting
Bertindaklah sebagai mentor Web Development. Saya baru saja menyelesaikan latihan menyusun "Struktur Halaman Blog Teknologi (Artikel & Sidebar)" menggunakan HTML Semantic. Tolong buatkan saya dokumen catatan belajar dalam format Markdown (.md) berdasarkan kode akhir saya.

Tolong susun file .md tersebut dengan kerangka berikut:

Deskripsi Proyek: Penjelasan singkat tentang apa yang dibuat oleh kode HTML ini (fokus pada penggunaan HTML5 Semantic Tags untuk layout dasar web).

Review Kesalahan & Pelajaran Penting: Tolong buatkan bagian khusus yang menyoroti dua hal yang sempat terlewat saat saya menyusun kode ini, agar saya bisa mengingatnya:

Posisi Elemen <footer>: Awalnya saya menaruh <footer> di dalam tag <main>. Jelaskan mengapa secara hierarki standar web, <footer> sebaiknya diletakkan sejajar dengan <header> dan <main> (langsung di dalam <body>).

Teks Formatting yang Terlupa: Saya lupa menggunakan tag <strong> pada bagian tanggal publikasi dan nama penulis. Ingatkan saya pentingnya tag ini untuk penekanan teks.

Bedah Kode & Fungsi Semantic (Baris per Baris): Jelaskan fungsi dari tag-tag semantik yang ada di kode saya dan mengapa mereka penting untuk SEO atau screen reader. Tolong bedah tag ini: <header>, <nav>, <main>, <article>, <aside>, dan <blockquote>.

Gunakan bahasa Indonesia yang santai, terstruktur rapi, dan mudah dipahami.

Berikut adalah kode HTML final saya yang sudah diperbaiki:
### 1. Posisi Elemen `<footer>` yang Salah

**Yang terjadi:**
Awalnya saya menaruh `<footer>` di **dalam** tag `<main>`.

**Mengapa ini salah?**
Secara hierarki standar web, `<header>`, `<main>`, dan `<footer>` adalah **elemen sejajar** yang masing-masing merepresentasikan bagian berbeda dari halaman:

```
<body>
  <header>   ← bagian atas (judul, logo)
  <nav>      ← navigasi
  <main>     ← konten utama
  <footer>   ← bagian bawah (hak cipta, kontak)
</body>
```

Jika `<footer>` dimasukkan ke dalam `<main>`, maka footer dianggap sebagai **bagian dari konten utama**, bukan sebagai penutup halaman secara keseluruhan. Ini akan membingungkan screen reader yang membantu tunanetra dalam menavigasi halaman.

**Yang benar:**
`<footer>` harus diletakkan **sejajar** dengan `<header>` dan `<main>`, langsung di dalam `<body>`.

---

### 2. Penggunaan `<b>` vs `<strong>` untuk Penekanan Teks

**Yang terjadi:**
Pada kode awal, saya menggunakan tag `<b>` pada tanggal publikasi dan nama penulis:

```html
<p>Dipublikasikan pada: <b>14 September 2026</b></p>
<p><b>Andika</b></p>
```

**Mengapa ini kurang tepat?**
Tag `<b>` hanya memberikan **efek tebal secara visual** tanpa makna semantik. Sedangkan `<strong>` memberikan **penekanan kuat** yang secara semantik memberitahu browser dan screen reader bahwa teks tersebut penting.

| Tag        | Fungsi                                | Semantik |
| ---------- | ------------------------------------- | -------- |
| `<b>`      | Teks tebal (visual saja)              | Tidak    |
| `<strong>` | Penekanan kuat (penting secara makna) | Ya       |

**Yang benar:**

```html
<p>Dipublikasikan pada: <strong>14 September 2026</strong></p>
<p><strong>Andika</strong></p>
```

---

## Bedah Kode & Fungsi Semantic

Berikut penjelasan tiap tag semantik yang digunakan dalam kode:

### `<header>`
```html
<header>
    <h1>DevBlog - Catatan Koding</h1>
</header>
```
**Fungsi:** Menandai bagian **awal** atau judul dari halaman/sebuah section.

**Penting untuk:**
- **SEO**: Mesin pencari mengenali ini sebagai judul utama halaman.
- **Screen reader**: Pengguna bisa langsung melompat ke bagian header tanpa scroll.

---

### `<nav>`
```html
<nav>
    <ul>
        <li>Beranda</li>
        <li>Artikel</li>
        <li>Portofolio</li>
        <li>Kontak</li>
    </ul>
</nav>
```
**Fungsi:** Menandai area **navigasi** utama situs.

**Penting untuk:**
- **SEO**: Google mengenali link navigasi dan menggunakannya untuk memahami struktur situs.
- **Screen reader**: Pengguna bisa langsung menuju ke bagian navigasi tanpa mendengarkan konten lainnya.

---

### `<main>`
```html
<main>
    <article>...</article>
</main>
```
**Fungsi:** Membungkus **konten utama** dari seluruh halaman. Hanya boleh ada **satu** `<main>` per halaman.

**Penting untuk:**
- **SEO**: Mesin pencari tahu bahwa di sinilah konten inti berada.
- **Screen reader**: Pengguna bisa langsung melompat ke konten utama, melewati header dan navigasi.

---

### `<article>`
```html
<article>
    <h2>Mengapa Memilih React dan Next.js di 2026?</h2>
    ...
</article>
```
**Fungsi:** Menandai konten yang **berdiri sendiri** dan bisa dibaca secara terpisah dari konteks lainnya — seperti artikel blog, berita, atau postingan forum.

**Penting untuk:**
- **SEO**: Google mengenali ini sebagai artikel utama dan menampilkannya di hasil pencarian.
- **Screen reader**: Pengguna bisa memahami bahwa ini adalah satu kesatuan konten yang utuh.

---

### `<aside>`
```html
<aside>
    <div class="author-profile">
        <h3>Tentang Penulis</h3>
        <p><b>Andika</b></p>
    </div>
</aside>
```
**Fungsi:** Menandai konten **sampingan** yang berhubungan dengan konten utama tetapi bisa dipisahkan — seperti profil penulis, sidebar, atau iklan.

**Penting untuk:**
- **SEO**: Mesin pencari tahu bahwa konten ini bersifat pendukung, bukan inti dari artikel.
- **Screen reader**: Pengguna bisa memilih untuk melewati atau membaca konten sampingan ini.

---

### `<blockquote>`
```html
<blockquote>"Mempelajari fundamental HTML dan CSS secara mendalam adalah kunci sebelum melompat ke framework."</blockquote>
```
**Fungsi:** Menandai **kutipan** dari sumber lain. Secara visual biasanya ditampilkan dengan indentasi.

**Penting untuk:**
- **SEO**: Google mengenali ini sebagai kutipan dan bisa menampilkannya di fitur "featured snippet".
- **Screen reader**: Pengguna bisa mendengar bahwa ini adalah kutipan, bukan bagian dari tulisan penulis.

---

## Refleksi Pribadi

> Dari latihan ini saya belajar bahwa setiap tag semantik punya **tempat dan maknanya masing-masing**. Menempatkan `<footer>` di tempat yang salah bisa mengubah arti struktur halaman. Saya juga menyadari perbedaan antara `<b>` dan `<strong>` — sesuatu yang dulu saya anggap sepele ternyata berpengaruh pada aksesibilitas. Mulai sekarang, saya akan lebih memperhatikan **makna**, bukan hanya **tampilan visual** saat menulis HTML.
