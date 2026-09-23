# Catatan Belajar: Review Company Profile (Nusantara Tech)

## Deskripsi Proyek

Halaman **company profile** untuk agensi fiktif "Nusantara Tech" (`companypro.html`), dibangun murni dengan **HTML** — belum ada CSS/JavaScript. Struktur halaman:

- **Header** — brand (`<h1>`), navigasi anchor, tombol CTA "Hubungi kami".
- **Hero** — tagline, deskripsi singkat, dua tombol CTA, dan gambar.
- **About** — "Siapa Nusantara Tech?" + kartu Visi & Misi.
- **Services** — tiga kartu layanan (Web Development, UI/UX Design, Integrasi AI).
- **Testimonial** — kutipan klien dalam `<blockquote>`.
- **Contact** — info kantor + form (nama, perusahaan, email, kebutuhan, pesan).
- **Footer** — kolom brand, menu, ikon sosial, hak cipta.

Saat ini masih tahap **kerangka (skeleton)** — fokus review-nya adalah memastikan **struktur HTML valid, semantik, dan anchor berfungsi** sebelum masuk ke styling CSS.

---

## Review Kesalahan & Pelajaran Penting

### 1. Tag Penutup Salah Urutan (`</main>` vs `</section>`)

**Yang terjadi:**
Section `contact-section` ditutup dengan `</main>` lalu `</section>` — urutan kebalikan, sehingga `<main>` yang dibuka di awal tidak pernah ditutup di tempat yang benar.

```html
<!-- ❌ SALAH: main ditutup sebelum section, lalu section menggantung -->
        </main>
    </section>
    <footer>...</footer>
</body>
```

```html
<!-- ✔️ BENAR: section ditutup dulu, baru main -->
        </section>
    </main>
    <footer>...</footer>
</body>
```

**Kenapa fatal?**

- **Outline dokumen rusak** — browser & screen reader kehilangan batas konten utama.
- **Styling CSS nanti kacau** — selector `main > section` tidak akan cocok.
- **Validasi HTML gagal** — tag bersarang harus ditutup dalam urutan LIFO (Last In, First Out).

**Aturan emas:** tag yang **dibuka terakhir** harus **ditutup pertama**.

---

### 2. Anchor `href` vs `id`: Harus Sama Persis (Case-Sensitive)

**Yang terjadi (berulang 3 kali):**

| Anchor (`href`) | `id` section | Hasil |
|---|---|---|
| `#tentang Kami` (ada spasi) | `tentang_kami` | ❌ rusak |
| `#klien` | `id="Klien"` (huruf besar K) | ❌ rusak |
| `#tentang_Kami` (footer) | `tentang_kami` | ❌ rusak |

```html
<!-- ❌ SALAH -->
<a href="#tentang Kami">Tentang Kami</a>   <!-- spasi tidak valid -->
<a href="#klien">Klien</a>
<section id="Klien">...</section>          <!-- beda kapital -->

<!-- ✔️ BENAR: huruf kecil semua, tanpa spasi -->
<a href="#tentang-kami">Tentang Kami</a>
<a href="#klien">Klien</a>
<section id="tentang-kami">...</section>
<section id="klien">...</section>
```

**Kenapa penting?**

- **Fragment identifier bersifat case-sensitive** — `#Klien` ≠ `#klien`. Browser mencocokkan **persis** dengan `id`.
- **Spasi di `href`** memecah URL — browser menganggapnya sebagai dua token.
- Nav yang kelihatan benar tapi **tidak melakukan apa-apa saat diklik** = bug paling menyebalkan karena tersembunyi.

**Tips:** seragamkan **semua** id & anchor dalam **huruf kecil + tanda minus** (`kebab-case`): `#beranda`, `#tentang-kami`, `#layanan`, `#klien`, `#kontak`.

---

### 3. `id` Harus Unik di Seluruh Dokumen

**Yang terjadi:**
`<select>` dan `<textarea>` sama-sama memakai `id="pesan"`:

```html
<!-- ❌ SALAH: id duplikat -->
<select name="pesan" id="pesan"></select>
<textarea name="pesan" id="pesan"></textarea>

<!-- ✔️ BENAR: satu id untuk satu elemen -->
<label for="pesan">Pesan :</label>
<textarea name="pesan" id="pesan"></textarea>
```

**Kenapa salah?**

- **`id` adalah identitas unik** — seperti NIK. Kalau ada dua, `label for="pesan"` dan JavaScript `document.getElementById('pesan')` hanya mengenali **elemen pertama**.
- Select-nya juga ternyata **kosong & tidak dibutuhkan** → solusinya: hapus, bukan dibiarkan.

---

### 4. `<label>` Wajib Punya Teks dan `for` yang Cocok

**Yang terjadi (2 kasus):**

```html
<!-- ❌ SALAH: for="name" tapi input-nya id="email" -->
<label for="name">Email :</label>
<input type="email" id="email" name="email">

<!-- ❌ SALAH: label kosong, tidak ada teks -->
<label for="kebutuhan"></label>
<select id="kebutuhan">...</select>
```

```html
<!-- ✔️ BENAR: teks jelas, for === id -->
<label for="email">Email :</label>
<input type="email" id="email" name="email" required>

<label for="kebutuhan">Kebutuhan :</label>
<select name="kebutuhan" id="kebutuhan">...</select>

<label for="pesan">Pesan :</label>
<textarea name="pesan" id="pesan" required></textarea>
```

**Kenapa penting?**

- **Klik label = fokus ke input** — target area jadi lebih besar, nyaman di mobile.
- **Screen reader membacakan label** sebelum input — tanpa label, pengguna tunanetra tidak tahu kolom itu untuk apa.
- `for` yang tidak cocok = label jadi hiasan mati.

> Aturan: **`for` pada label === `id` pada input**, dan label **tidak pernah kosong**.

---

### 5. Hierarki Heading: Satu `<h1>`, Jangan Lompat Level

**Yang terjadi:**

- Awalnya **tidak ada `<h1>` sama sekali** — hero langsung `<h2>`.
- Heading di `contact-section` pakai `<h3>` (lompat dari `<h2>` section ke `<h3>` tanpa `<h2>` pengganti).
- Brand di footer pakai `<h2>` — bersaing dengan heading halaman padahal bukan struktur konten.

```html
<!-- ✔️ BENAR: hierarki rapi -->
<header>
  <h1>Nusantara Tech</h1>          <!-- hanya 1 di seluruh halaman -->
</header>
<main>
  <section><h2>Solusi Digital...</h2>...</section>
  <section><h2>Siapa Nusantara Tech?</h2>...</section>
  <section>
    <h2>Kunjungi Kantor Kami</h2>  <!-- bukan h3 -->
  </section>
</main>
<footer>
  <p class="footer-title">Nusantara Tech</p>  <!-- bukan heading -->
</footer>
```

**Kenapa penting?**

- **SEO:** Google pakai heading untuk memahami struktur — banyak `<h1>` = bingung menentukan judul utama.
- **Aksesibilitas:** screen reader navigasi cepat antar bagian lewat heading.
- **Footer brand bukan konten utama** → pakai `<p>`, bukan `<h2>`.

---

### 6. `<button>` vs `<a>` — Navigasi atau Aksi?

**Yang terjadi:** CTA hero memakai `<button>` tanpa `type`, padahal tombol itu berfungsi untuk **navigasi/scroll**, bukan aksi form.

```html
<!-- ❌ ambigu: button untuk navigasi -->
<button>Konsultasi Gratis</button>

<!-- ✔️ BENAR -->
<!-- Navigasi (pindah halaman / loncat ke anchor) → <a> -->
<a href="#kontak" class="btn">Konsultasi Gratis</a>

<!-- Aksi di halaman (submit, modal, toggle) → <button> -->
<button type="button">Pelajari Lebih Lanjut</button>
```

| Elemen | Fungsi | Contoh |
|---|---|---|
| `<a>` | **Navigasi** | loncat ke `#kontak`, buka halaman lain |
| `<button>` | **Aksi di halaman** | submit form, buka modal, toggle menu |

Bonus: selalu tulis `type` secara eksplisit — default-nya `submit`, yang **bisa tidak sengaja mengirim form** jika berada di dalam `<form>`.

---

### 7. `<html lang="en">` pada Konten Bahasa Indonesia

```html
<!-- ❌ SALAH -->
<html lang="en">

<!-- ✔️ BENAR -->
<html lang="id">
```

**Kenapa penting?**

- **Screen reader** memakai `lang` untuk memilih mesin & aturan pelafalan yang benar.
- **SEO regional** — Google menggunakan `lang` untuk memetakan konten ke bahasa/lokasi.
- Konsistensi: konten berbahasa Indonesia → `lang="id"`.

---

## Riwayat Review (Status Perbaikan)

### ✅ Sudah Diperbaiki

| # | Masalah | Perbaikan |
|---|---|---|
| 1 | `</main>` & `</section>` salah urutan di `contact-section` | Ditukar: `</section>` → `</main>` |
| 2 | Tidak ada `<h1>` — hero langsung `<h2>` | `<p>` brand diganti `<h1>` di header |
| 3 | Nav `href="#tentang Kami"` (ada spasi) | Diganti `#tentang_kami` |
| 4 | Section tidak punya `id` — semua anchor mati | Ditambahkan `id`: `beranda`, `tentang_kami`, `layanan`, `klien`, `kontak` |
| 5 | `id="Klien"` vs `href="#klien"` (beda kapital) | Diseragamkan huruf kecil semua |
| 6 | Footer `href="#tentang_Kami"` tidak cocok | Diganti `#tentang_kami` |
| 7 | `<label for="name">Email` tapi `id="email"` | Diganti `for="email"` |
| 8 | `<label>` untuk select & textarea kosong/tidak ada | Ditambahkan "Kebutuhan :" & "Pesan :" |
| 9 | Duplikat `id="pesan"` (`<select>` kosong + textarea) | Select kosong dihapus |
| 10 | Select tanpa placeholder | Ditambahkan `<option disabled selected>Pilih kebutuhan</option>` |
| 11 | Heading contact `<h3>` (lompat level) | Diganti `<h2>` |
| 12 | `value="submit"` (tidak informatif) | Diganti `"Kirim Pesan"` |
| 13 | CTA hero `<button>` tanpa `type` | Ditambahkan `type="button"` |

### ❌ Belum Diperbaiki (Target Berikutnya)

- [ ] `<html lang="en">` → `<html lang="id">` (baris 2)
- [ ] Brand footer `<h2>` → `<p class="footer-title">`
- [ ] Alt ikon salah tulis: `"linkind"` → `"linkedin"`
- [ ] Ikon sosial belum dibungkus `<a href="...">` — belum bisa diklik
- [ ] Gambar hotlink Bing/rawan mati → pindahkan ke folder `assets/`
- [ ] `meta description` masih generik → buat lebih deskriptif untuk SEO
- [ ] Penamaan class `col_1/col_2/col_3` (snake) tidak konsisten dengan `hero-text` (kebab) → seragamkan kebab-case
- [ ] Hero CTA masih `<button>` — kalau tujuannya navigasi, ganti `<a class="btn">`
- [ ] Belum ada CSS sama sekali → buat `css/style.css`

---

## Refleksi Pribadi

> Review company profile ini mengajarkan saya bahwa **detail kecil yang tidak terlihat justru paling berbahaya**. Tag penutup yang salah urutan merusak seluruh outline dokumen tanpa bikin halaman "error" secara mencolok. Anchor yang beda kapital membuat nav yang *kelihatan* benar tapi **tidak melakukan apa-apa** saat diklik — saya tidak akan pernah tahu tanpa mengkliknya satu per satu. Dari sini saya sadar: **HTML yang "jalan" belum tentu HTML yang benar**. Validasi struktur, kecocokan `id`↔`for`↔`href`, dan hierarki heading adalah fondasi yang harus beres **sebelum** satu baris CSS pun ditulis — karena CSS yang rapi tidak akan pernah menyelamatkan HTML yang berantakan.

---

## Jembatan ke Materi Selanjutnya (Kerangka Dasar Web)

Struktur HTML yang sudah valid ini adalah **prasyarat** untuk styling. Langkah berikutnya:

**Fase 1 — Rapikan sisa checklist ❌ di atas** (perbaikan HTML murni).

**Fase 2 — Buat kerangka CSS** (`css/style.css`):

```css
/* Custom properties = "design token" */
:root {
  --color-primary: #2563eb;
  --font-body: "Segoe UI", sans-serif;
}

/* Hero: 2 kolom dengan Flexbox */
.hero-section {
  display: flex;
  align-items: center;
  gap: 2rem;
}

/* Layanan: kartu grid */
.services-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
}

/* Footer: 3 kolom */
.footer-columns {
  display: flex;
  justify-content: space-between;
}

/* Responsif */
@media (max-width: 768px) {
  .hero-section,
  .footer-columns { flex-direction: column; }
  .services-grid { grid-template-columns: 1fr; }
}
```

**Fase 3 — Opsional:** pindah gambar ke `assets/`, favicon + Open Graph, smooth scroll.

**Catatan untuk diri sendiri:** semua class di HTML ini (`hero-section`, `services-grid`, `service-card`, `card-visi`, `footer-columns`, `btn`, dst.) **sudah siap dituju oleh CSS** — jangan ganti nama class saat styling, atau style akan pecah.
