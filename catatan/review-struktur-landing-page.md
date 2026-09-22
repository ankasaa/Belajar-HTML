# Catatan Belajar: Review Struktur Landing Page Portofolio

## Deskripsi Proyek

Proyek ini adalah **landing page portofolio sederhana** (`porto.html`) yang dibangun murni dengan HTML — tanpa CSS atau JavaScript. Halaman ini terdiri dari tiga bagian utama:

- **Hero** — perkenalan singkat ("Halo, Saya Andika") lengkap dengan foto profil dan tombol CTA.
- **Keahlian** — tiga kartu skill: Frontend Development, UI/UX Design, dan Eksplorasi AI.
- **Kontak** — form sederhana berisi nama, email, dan pesan.

Saat ini masih tahap **kerangka (skeleton)**, jadi fokusnya adalah memastikan struktur HTML valid dan sesuai standar sebelum masuk ke tahap styling CSS.

---

## Review Kesalahan & Standar Industri

### 1. Logika Penamaan Class

Untuk elemen yang **identik dan berulang** (misalnya tiga kartu skill), gunakan **satu nama class yang sama**:

```html
<!-- ✅ Benar: satu class dipakai berulang -->
<div class="skill-card">...</div>
<div class="skill-card">...</div>
<div class="skill-card">...</div>

<!-- ❌ Kurang tepat: nama unik tiap kartu -->
<div class="card-1">...</div>
<div class="card-2">...</div>
<div class="card-3">...</div>
```

**Kenapa begitu?**

- **DRY (Don't Repeat Yourself):** satu blok CSS `.skill-card { ... }` otomatis mengatur ketiga kartu sekaligus.
- **Mudah ditambah:** kartu ke-4, ke-5, dst. tinggal pakai class yang sama — tanpa perlu menulis style baru.
- **Konsisten:** semua kartu dijamin tampil sama. Kalau pakai `card-1/2/3`, ada risiko style tidak seragam dan CSS jadi bertumpuk-tumpuk.

> Aturan praktisnya: **nama class menjelaskan "apa" fungsinya** (skill-card), bukan "posisi keberapa" (card-1). Class unik hanya dipakai kalau memang ada perbedaan nyata (misalnya `featured-card` untuk kartu yang ditonjolkan).

---

### 2. Aturan Button & Anchor

**Jangan pernah membungkus tag `<a>` di dalam `<button>`** (atau sebaliknya):

```html
<!-- ❌ Tidak valid & ambigu -->
<button>
  <a href="#proyek">Lihat Proyek</a>
</button>

<!-- ❌ Salah juga -->
<a href="#proyek">
  <button>Lihat Proyek</button>
</a>
```

**Kenapa?**

- Keduanya adalah **elemen interaktif** yang saling bertabrakan — browser bisa bingung memproses klik, Enter, atau fokus keyboard.
- **Tidak valid menurut spesifikasi HTML** (`<button>` hanya boleh berisi teks/phrasing content, bukan elemen interaktif lain).
- **Merusak aksesibilitas:** pembaca layar bisa mengumumkan dua elemen sekaligus, dan perilaku keyboard jadi tidak terduga.

**Solusi terbaik** — pakai `<a>` saja dengan class, lalu bentuk seperti tombol pakai CSS:

```html
<a href="#proyek" class="btn">Lihat Proyek</a>
```

```css
.btn {
  display: inline-block;
  padding: 10px 20px;
  background-color: #2563eb;
  color: #fff;
  text-decoration: none;
  border-radius: 6px;
}
.btn:hover {
  background-color: #1d4ed8;
}
```

**Kapan pakai yang mana?**

| Elemen | Fungsi |
|---|---|
| `<a>` | **Navigasi** — pindah halaman / loncat ke anchor (`#section`) |
| `<button>` | **Aksi di halaman** — submit form, buka modal, toggle |

Di kode kita, tombol "Lihat proyek" mengarah ke anchor → jawaban yang benar adalah `<a class="btn">`, persis seperti yang sudah dipakai.

---

### 3. Atribut Form: `action` vs `method`

Kedua atribut punya peran berbeda:

```html
<form action="#" method="post">
```

| Atribut | Fungsi | Analogi |
|---|---|---|
| `action` | **Ke mana** data dikirim (URL tujuan) | Alamat rumah penerima surat |
| `method` | **Bagaimana** data dikirim (GET atau POST) | Cara surat dikirim (pos biasa vs kurir tertutup) |

**`method="get"` vs `method="post"`:**

- **GET** → data ditempel di **URL** (`?name=Andika&email=...`). Cocok untuk pencarian/filter. **Tidak cocok untuk form kontak** karena email & pesan bocor ke URL, history browser, dan log server.
- **POST** → data dikirim di **badan request** (tersembunyi). Inilah standar untuk form login, registrasi, dan kontak.

**Di kode kita sebelumnya pernah ada masalah:**

- `method="get"` → data form bocor ke URL. ✅ Sudah diperbaiki jadi `post`.
- `action="#"` → tujuan masih kosong, jadi pesan belum benar-benar terkirim ke mana pun. Ini **wajar untuk latihan HTML murni** (belum ada backend). Kalau nanti mau form-nya benar-benar jalan tanpa server sendiri, bisa diarahkan ke layanan gratis seperti Formspree.

---

### 4. Hierarki Heading (SEO & Aksesibilitas)

Setiap halaman web sebaiknya hanya punya **satu `<h1>`**, lalu sub-bagian memakai `<h2>`, dan sub-sub-bagian memakai `<h3>` — seperti kerangka daftar berpohon:

```html
<h1>Halo, Saya Andika</h1>          <!-- hanya 1 di seluruh halaman -->

  <h2>Keahlian Utama</h2>           <!-- bagian utama -->
    <h3>Frontend Development</h3>   <!-- isi dari bagian -->
    <h3>UI/UX Design</h3>
    <h3>Eksplorasi AI</h3>

  <h2>Mari Berkolaborasi!</h2>
```

**Kenapa penting?**

- **SEO:** Google memakai heading untuk memahami struktur & topik halaman. Banyak `<h1>` membuat mesin pencari bingung menentukan judul utama.
- **Aksesibilitas:** pembaca layar (screen reader) memakai heading untuk navigasi cepat. Pengguna tunanetra bisa "meloncati" antar bagian lewat heading — kalau hierarkinya berantakan, navigasi jadi kacau.
- **Keterbacaan kode:** developer lain (dan diri kita sendiri nanti) langsung paham struktur halaman hanya dengan melihat heading.

> **Mistake yang pernah terjadi di kode ini:** judul kartu skill awalnya pakai `<h2>` lagi (sama level dengan judul section "Keahlian Utama"). Padahal kartu adalah **isi dari** section tersebut → sudah diperbaiki jadi `<h3>`. ✅

---

## Masalah yang Sudah Dipecahkan (Riwayat Review)

Berikut daftar bug yang ditemukan dan sudah diperbaiki selama proses review:

| # | Masalah | Perbaikan |
|---|---|---|
| 1 | `<p>Portofolio Andika<p>` — tag tidak ditutup | Diperbaiki jadi `</p>` |
| 2 | `section.hero-section` tidak pernah ditutup | Ditambahkan `</section>` |
| 3 | `<h2>...</h1>` — closing tag salah di 2 tempat | Diperbaiki jadi `</h2>` |
| 4 | `<meta name="Deskripsi">` tanpa `content` + viewport hilang | Dipisah jadi `description` + `viewport` yang benar |
| 5 | Input `name` & `email` **tanpa atribut `name`** | Ditambahkan `name="name"`, `name="email"` — sekarang ikut terkirim |
| 6 | `method="get"` membocorkan data ke URL | Diganti `method="post"` |
| 7 | Form bisa dikirim kosong | Ditambahkan `required` di semua field |
| 8 | Judul kartu pakai `<h2>` (hierarki salah) | Diganti `<h3>` |
| 9 | Nav anchor `#Keahlian` dll. tapi section belum punya `id` | **Belum diperbaikan** — section perlu `id="keahlian"` dst. |
| 10 | `lang="en"` padahal konten bahasa Indonesia | **Belum diperbaikan** — seharusnya `lang="id"` |

**Masalah yang masih tersisa (target berikutnya):**

- [ ] Tambahkan `id` pada setiap `<section>` agar nav anchor berfungsi
- [ ] Ubah `<html lang="en">` → `<html lang="id">`
- [ ] Tulis CSS untuk class `hero-section`, `skill-card`, `btn` (halaman masih polos)
- [ ] Ganti gambar hotlink pngtree dengan file lokal (rawan mati)
- [ ] Rapikan label: `pesan :` → `Pesan:`, `kirim pesan` → `Kirim Pesan`
- [ ] Section "Proyek" belum ada — buat section-nya atau hapus menunya

---

## Kode HTML Final

> *Tempelkan versi final `porto.html` Anda di sini setelah semua perbaikan selesai.*
