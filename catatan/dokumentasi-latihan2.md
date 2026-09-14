# Dokumentasi Kode HTML - Latihan 2 (Formulir)

## 1. Penjelasan Singkat

Halaman ini adalah **halaman formulir pemesanan proyek web**. Tujuannya untuk melatih penggunaan tag-tag form dalam HTML, seperti input teks, email, dropdown, radio button, textarea, dan tombol submit. Formulir ini nantinya akan digunakan untuk mengirim data pengguna ke server (misalnya dengan PHP).

---

## 2. Cara Membaca Kode

Alur pembacaan kode HTML dari **atas ke bawah**:

1. `<!DOCTYPE html>` → Deklarasi dokumen HTML5
2. `<html lang="en">` → Tag root dengan bahasa Inggris
3. `<head>` → Metadata untuk browser
4. `<meta charset="UTF-8">` → Encoding karakter
5. `<meta name="viewport" ...>` → Tampilan responsif di mobile
6. `<title>latihan2</title>` → Judul di tab browser
7. `</head>` → Penutup head
8. `<body>` → Mulai konten yang terlihat
9. `<h1>` → Judul utama formulir
10. `<p>` → Paragraf penjelasan
11. `<form action="#">` → Container semua elemen form
12. `<label>`, `<input>`, `<select>`, `<textarea>` → Elemen-elemen form
13. `</form>` → Penutup form
14. `</body>`, `</html>` → Penutup

---

## 3. Logika Struktur (Parent-Child)

```
<html>
├── <head>
│   ├── <meta charset>
│   ├── <meta viewport>
│   └── <title>
└── <body>
    ├── <h1>Formulir Permintaan Proyek Web</h1>
    ├── <p>Silakan isi data...</p>
    └── <form action="#">              ← Container utama form
        ├── <label for="name">         ← Label untuk input nama
        ├── <input type="text">        ← Input teks nama
        ├── <label for="email">        ← Label untuk input email
        ├── <input type="email">       ← Input email
        ├── <label for="dropdown">     ← Label untuk dropdown
        ├── <select name="Dropdown">   ← Dropdown/jenis proyek
        │   ├── <option value="landing_page">
        │   ├── <option value="sistem_informasi">
        │   └── <option value="e_commerce">
        ├── <h3>Tingkat Urgensi:</h3>
        ├── <label for="santai">       ← Label radio "Santai"
        ├── <input type="radio">       ← Radio button "Santai"
        ├── <label for="segera">       ← Label radio "Segera"
        ├── <input type="radio">       ← Radio button "Segera"
        ├── <textarea>                 ← Area teks panjang
        └── <input type="submit">      ← Tombol kirim
    </form>
</body>
```

---

## 4. Fungsi Masing-Masing Tag

| Baris | Tag | Fungsi |
|-------|-----|--------|
| 9 | `<h1>Formulir Permintaan Proyek Web</h1>` | Judul utama halaman formulir |
| 10 | `<p>"Silakan isi data..."</p>` | Paragraf penjelasan singkat |
| 11 | `<form action="#">` | Container semua elemen form, `action="#"` = URL tujuan data dikirim |
| 12 | `<label for="name">` | Label yang terhubung ke input `id="name"`, klik label → cursor pindah ke input |
| 13 | `<input type="text" name="name" id="name">` | Kotak input teks biasa untuk nama lengkap |
| 15 | `<label for="email">` | Label untuk input email |
| 16 | `<input type="email" name="email" id="email">` | Input khusus email (otomatis validasi format email) |
| 18 | `<label for="dropdown">` | Label untuk dropdown |
| 19-23 | `<select name="Dropdown">` + `<option>` | Dropdown pilihan: Landing Page, Sistem Informasi, E-Commerce |
| 24 | `<h3>Tingkat Urgensi:</h3>` | Sub-judul bagian urgensi |
| 25 | `<label for="santai">Santai</label>` | Label untuk radio button "Santai" |
| 26 | `<input type="radio" name="Urgensi" id="santai" value="santai">` | Radio button "Santai" (hanya bisa pilih 1) |
| 27 | `<label for="segera">Segera</label>` | Label untuk radio button "Segera" |
| 28 | `<input type="radio" name="Urgensi" id="segera" value="segera">` | Radio button "Segera" |
| 30 | `<textarea name="kebutuhan_fitur" id="fitur" rows="5">` | Kotak teks panjang 5 baris untuk menjelaskan kebutuhan |
| 31 | `<input type="submit" value="Kirim Permintaan">` | Tombol kirim form |

---

## 5. Kenapa Harus Begitu? (Best Practices)

### `for` di `<label>` dan `id` di `<input>` — Harus cocok!
- `for="name"` di label harus sama dengan `id="name"` di input.
- Fungsinya: saat teks label diklik, cursor otomatis pindah ke input yang sesuai.
- Ini penting untuk **aksesibilitas** (screen reader bisa membantu pengguna tunanetra).

### `name` di `<input>` — Wajib diisi!
- `name` adalah "nama kolom" yang akan dikirim ke server.
- Contoh: jika `name="name"` dan pengguna mengetik "Budi", maka data yang dikirim = `name=Budi`.
- Tanpa `name`, data **tidak akan terkirim** ke server.

### Radio button harus punya `name` yang sama
- Semua radio button dalam satu grup harus punya `name` yang sama (misal `name="Urgensi"`).
- Ini yang membuat hanya **satu yang bisa dipilih**. Jika `name` berbeda, semua radio bisa dipilih sekaligus.

### `value` di radio button — Wajib diisi!
- `value` adalah nilai yang dikirim ke server saat radio button dipilih.
- Contoh: jika "Santai" dipilih, data yang dikirim = `Urgensi=santai`.

### `type="email"` vs `type="text"`
- `type="email"` memberikan **validasi otomatis** oleh browser.
- Jika pengguna mengetik email format salah (misal tanpa `@`), browser akan menolak form-nya.
- `type="text"` tidak ada validasi, jadi gunakan `type="email"` untuk field email.

### `<select>` dan `<option>` — Dropdown
- `<select>` adalah container dropdown.
- `<option>` adalah setiap opsi di dalamnya.
- Setiap `<option>` harus punya `value` yang berbeda.

### `rows="5"` di `<textarea>`
- `rows="5"` menentukan tinggi textarea sebesar 5 baris teks.
- Tanpa atribut ini, textarea akan tampil dengan ukuran default (biasanya kecil).

### `action="#"` di `<form>`
- `action` menentukan **URL tujuan** data form dikirim.
- `#` berarti tidak dikirim ke mana-mana (untuk sementara).
- Nanti saat belajar PHP, ganti dengan path file PHP yang akan memproses data.

### `<br>` — Tag line break
- Digunakan untuk membuat baris baru tanpa membuat paragraph baru.
- Berguna untuk memisahkan elemen form agar lebih rapi.
