# 01 - Struktur Dasar HTML

## Kerangka Dokumen

| Tag               | Penjelasan                                  | Contoh                              |
| ----------------- | ------------------------------------------- | ----------------------------------- |
| `<!DOCTYPE html>` | Deklarasi tipe dokumen HTML5                | `<!DOCTYPE html>`                   |
| `<html>`          | Elemen root yang membungkus seluruh dokumen | `<html lang="id">...</html>`        |
| `<head>`          | Metadata halaman, tidak tampil di browser   | `<head><title>Judul</title></head>` |
| `<body>`          | Semua konten yang tampil di browser         | `<body><h1>Judul</h1></body>`       |

Struktur lengkap:

```html
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <title>Judul Halaman</title>
  </head>
  <body>
    Konten halaman
  </body>
</html>
```

## Elemen & Atribut

| Tag              | Penjelasan                             | Contoh                                       |
| ---------------- | -------------------------------------- | -------------------------------------------- |
| Elemen HTML      | Tag pembuka, konten, tag penutup       | `<p>Ini paragraf</p>`                        |
| Self-Closing Tag | Void element tanpa konten              | `<br />`, `<hr />`, `<img src="foto.jpg" />` |
| Atribut          | Info tambahan pada elemen              | `<img src="gambar.jpg" alt="Deskripsi" />`   |
| Atribut Boolean  | Cukup ditulis tanpa nilai (ada = true) | `<input disabled />`                         |

Contoh elemen dan atribut:

```html
<a href="https://google.com" target="_blank">Link</a>
<input type="text" placeholder="Nama anda" required />
<details open>
  <summary>Judul</summary>
  Konten detail
</details>
```

## Tag Dasar

| Tag             | Penjelasan                                  | Contoh                 |
| --------------- | ------------------------------------------- | ---------------------- |
| `<h1>` - `<h6>` | Heading dari terbesar (h1) ke terkecil (h6) | `<h1>Judul Utama</h1>` |
| `<p>`           | Paragraf teks                               | `<p>Ini paragraf.</p>` |
| `<br>`          | Pindah baris dalam teks                     | `<br />`               |
| `<hr>`          | Garis pemisah horizontal                    | `<hr />`               |
| `<!-- -->`      | Komentar (tidak tampil di browser)          | `<!-- komentar -->`    |

Contoh heading:

```html
<h1>Judul Utama</h1>
<h2>Sub Judul</h2>
<h3>Sub Sub Judul</h3>
```

Contoh komentar:

```html
<!--
  Komentar
  Multi baris
-->
<p>Teks terlihat</p>
```

## Entitas & Karakter Spesial

| Entitas  | Penjelasan            | Contoh   |
| -------- | --------------------- | -------- |
| `&amp;`  | Ampersand (&)         | `&amp;`  |
| `&lt;`   | Kurung buka (<)       | `&lt;`   |
| `&gt;`   | Kurung tutup (>)      | `&gt;`   |
| `&quot;` | Kutip dua (")         | `&quot;` |
| `&#39;`  | Kutip satu (')        | `&#39;`  |
| `&nbsp;` | Spasi non-breaking    | `&nbsp;` |
| `&copy;` | Simbol copyright (©)  | `&copy;` |
| `&reg;`  | Simbol registered (®) | `&reg;`  |

```html
<p>10 &lt; 20 dan 20 &gt; 10</p>
<p>&copy; 2024 Perusahaan Kami</p>
```
