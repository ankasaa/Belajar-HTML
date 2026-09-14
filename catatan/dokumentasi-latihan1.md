# Dokumentasi Kode HTML - Latihan 1

## 1. Penjelasan Singkat

Halaman ini adalah halaman **profil pribadi sederhana** yang berisi perkenalan diri, daftar hobi/interest dalam bentuk list, dan sebuah gambar. Tujuannya untuk melatih penggunaan tag-tag dasar HTML seperti heading, paragraph, list, dan image.

---

## 2. Cara Membaca Kode

Alur pembacaan kode HTML selalu dari **atas ke bawah**:

1. `<!DOCTYPE html>` → Pemberitahuan ke browser: "Ini adalah dokumen HTML5"
2. `<html>` → Tag pembuka, seluruh konten halaman ada di dalamnya
3. `<head>` → Bagian "kepala" dokumen, berisi info untuk browser (bukan konten yang terlihat)
4. `<meta charset="UTF-8">` → Setting karakter encoding
5. `<meta name="viewport" ...>` → Setting agar tampilan responsif di mobile
6. `<title>` → Judul yang muncul di tab browser
7. `</head>` → Penutup bagian kepala
8. `<body>` → Bagian "tubuh", berisi semua konten yang **terlihat** oleh pengguna
9. `<h1>`, `<p>`, `<h2>`, `<ul>`, `<li>`, `<img>` → Konten yang ditampilkan
10. `</body>`, `</html>` → Penutup

---

## 3. Logika Struktur (Parent-Child)

```
<html>                          ← Parent (induk) dari semua
├── <head>                      ← Anak dari <html>
│   ├── <meta charset>
│   ├── <meta viewport>
│   └── <title>
└── <body>                      ← Anak dari <html>
    ├── <h1>Andika</h1>
    ├── <p>...</p>
    ├── <p>...</p>
    ├── <h2>Game & Waktu Luang</h2>
    ├── <ul>                    ← Anak dari <body>
    │   ├── <li>Bermain Dead by Daylight</li>    ← Anak dari <ul>
    │   ├── <li>Bermain Roblox...</li>
    │   └── <li>Menjelajahi teknologi AI...</li>
    ├── <h2>Game & Waktu Luang</h2>
    ├── <ul>
    │   ├── <li>Malibu Nights</li>
    │   ├── <li>ILYSB</li>
    │   └── <li>Thru These Tears</li>
    └── <img src="..." alt="..." />
</body>
```

Setiap tag yang dibuka **harus ditutup**. Isi di antara tag pembuka dan penutup disebut **konten** atau **child** (anak).

---

## 4. Fungsi Masing-Masing Tag

| Baris | Tag | Fungsi |
|-------|-----|--------|
| 1 | `<!DOCTYPE html>` | Mendeklarasikan dokumen sebagai HTML5 |
| 2 | `<html lang="en">` | Tag root, `lang="en"` menandakan bahasa konten adalah Inggris |
| 3 | `<head>` | Container untuk metadata (info untuk browser) |
| 4 | `<meta charset="UTF-8">` | Setting encoding karakter agar teks tampil benar (termasuk karakter Indonesia) |
| 5 | `<meta name="viewport" ...>` | Agar halaman responsif/adaptive di layar HP dan desktop |
| 6 | `<title>latihan1</title>` | Judul halaman di tab browser |
| 9 | `<h1>Andika</h1>` | Heading level 1, judul utama (paling besar) |
| 10-11 | `<p>...</p>` | Paragraph, berisi teks paragraf |
| 13 | `<h2>Game & Waktu Luang</h2>` | Heading level 2, sub-judul |
| 14-18 | `<ul>` + `<li>` | **Unordered list** (list tak berurut) dengan item-item di dalamnya |
| 25 | `<img>` | Menampilkan gambar dari URL |

---

## 5. Kenapa Harus Begitu? (Best Practices)

### `meta name="viewport"` — Wajib ada!
Tanpa ini, tampilan di HP akan "kecil" karena browser mengira halaman ini untuk layar lebar. Tag ini memaksa browser menyesuaikan ukuran layar perangkat.

### `alt` pada `<img>` — Wajib ada!
- **Aksesibilitas**: Pembaca layar (screen reader) untuk tuna netra akan membacakan teks `alt` sebagai pengganti gambar.
- **Fallback**: Jika gambar gagal dimuat, teks `alt` yang muncul.
- **SEO**: Mesin pencari Google membaca `alt` untuk memahami isi gambar.

### `border="1px solid black"` di `<img>` — Kurang tepat!
Di kode ini, `border="1px solid black"` ditulis langsung di tag `<img>`. Ini sebenarnya **sudah tidak direkomendasikan** karena:
- `border` di HTML hanya menerima nilai angka (misal `border="1"`), bukan CSS syntax.
- Untuk styling seperti warna, gaya, dan ketebalan border, sebaiknya gunakan **CSS** (inline `style` atau file `.css` terpisah).

Contoh perbaikan:
```html
<!-- Sebelum (kurang tepat) -->
<img src="..." border="1px solid black">

<!-- Sesudah (lebih baik) -->
<img src="..." style="border: 1px solid black;">
```

### `lang="en"` di `<html>`
Membantu search engine dan screen reader mengetahui bahasa konten. Karena kontennya campuran Indonesia-Inggris, bisa juga diganti `lang="id"`.
