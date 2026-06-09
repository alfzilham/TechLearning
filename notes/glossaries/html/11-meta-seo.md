# 11 - Meta, SEO & Head Elements

## `<head>` Elements

| Tag                  | Penjelasan                                    | Contoh                                                                     |
| -------------------- | --------------------------------------------- | -------------------------------------------------------------------------- |
| `<title>`            | Judul halaman (tab browser + hasil pencarian) | `<title>Belajar HTML - Tutorial Lengkap</title>`                           |
| `<meta charset>`     | Character set halaman                         | `<meta charset="UTF-8" />`                                                 |
| `<meta viewport>`    | Pengaturan responsive                         | `<meta name="viewport" content="width=device-width, initial-scale=1.0" />` |
| `<meta description>` | Deskripsi (tampil di hasil pencarian)         | `<meta name="description" content="Tutorial HTML lengkap" />`              |
| `<meta keywords>`    | Keywords (kurang penting sekarang)            | `<meta name="keywords" content="HTML, CSS, JavaScript" />`                 |
| `<meta author>`      | Pembuat halaman                               | `<meta name="author" content="Rizky" />`                                   |
| `<meta robots>`      | Aturan untuk search engine                    | `<meta name="robots" content="index, follow" />`                           |
| `<meta refresh>`     | Redirect/refresh otomatis                     | `<meta http-equiv="refresh" content="5; url=https://example.com" />`       |

Nilai `robots`: `index` / `noindex`, `follow` / `nofollow`, `noarchive`.

### Meta HTTP-Equiv

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
<meta http-equiv="cache-control" content="no-cache" />
```

## Social Media (Open Graph)

| Tag              | Penjelasan                   | Contoh                                                                     |
| ---------------- | ---------------------------- | -------------------------------------------------------------------------- |
| `og:title`       | Judul untuk sosial media     | `<meta property="og:title" content="Judul Halaman" />`                     |
| `og:description` | Deskripsi untuk sosial media | `<meta property="og:description" content="Deskripsi singkat" />`           |
| `og:image`       | Thumbnail untuk sosial media | `<meta property="og:image" content="https://example.com/thumbnail.jpg" />` |
| `og:url`         | URL kanonikal                | `<meta property="og:url" content="https://example.com" />`                 |
| `og:type`        | Tipe konten                  | `<meta property="og:type" content="website" />`                            |

```html
<meta property="og:title" content="Judul Halaman" />
<meta property="og:description" content="Deskripsi singkat" />
<meta property="og:image" content="https://example.com/thumbnail.jpg" />
<meta property="og:url" content="https://example.com" />
<meta property="og:type" content="website" />
<meta property="og:site_name" content="Nama Situs" />
<meta property="og:locale" content="id_ID" />
```

### Twitter Card

```html
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="Judul Halaman" />
<meta name="twitter:description" content="Deskripsi singkat" />
<meta name="twitter:image" content="https://example.com/thumbnail.jpg" />
<meta name="twitter:site" content="@username" />
<meta name="twitter:creator" content="@creator" />
```

## Link Elements

| Tag                               | Penjelasan                        | Contoh                                                                 |
| --------------------------------- | --------------------------------- | ---------------------------------------------------------------------- |
| `<link rel="stylesheet">`         | CSS stylesheet eksternal          | `<link rel="stylesheet" href="style.css" />`                           |
| `<link rel="icon">`               | Favicon                           | `<link rel="icon" href="favicon.ico" type="image/x-icon" />`           |
| `<link rel="apple-touch-icon">`   | Icon untuk iOS                    | `<link rel="apple-touch-icon" href="icon-192.png" />`                  |
| `<link rel="preconnect">`         | Koneksi awal ke server (optimasi) | `<link rel="preconnect" href="https://fonts.googleapis.com" />`        |
| `<link rel="preload">`            | Preload resource penting          | `<link rel="preload" href="font.woff2" as="font" />`                   |
| `<link rel="prefetch">`           | Prefetch halaman berikutnya       | `<link rel="prefetch" href="halaman-lain.html" />`                     |
| `<link rel="canonical">`          | Hindari duplicate content         | `<link rel="canonical" href="https://example.com/halaman" />`          |
| `<link rel="alternate" hreflang>` | Bahasa alternatif                 | `<link rel="alternate" hreflang="en" href="https://example.com/en" />` |
| `<link rel="manifest">`           | Manifest untuk PWA                | `<link rel="manifest" href="/manifest.json" />`                        |

## Script Elements

| Tag / Atribut   | Penjelasan                            | Contoh                                          |
| --------------- | ------------------------------------- | ----------------------------------------------- |
| `<script>`      | JavaScript inline atau eksternal      | `<script src="script.js"></script>`             |
| `defer`         | Jalan setelah HTML selesai diparse    | `<script src="script.js" defer></script>`       |
| `async`         | Jalan segera setelah download selesai | `<script src="analytics.js" async></script>`    |
| `type="module"` | ES6 module                            | `<script type="module" src="main.js"></script>` |
| `nomodule`      | Fallback untuk browser lama           | `<script nomodule src="legacy.js"></script>`    |

## Struktur Head Lengkap

```html
<!DOCTYPE html>
<html lang="id">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <!-- SEO -->
    <title>Judul Halaman | Nama Situs</title>
    <meta name="description" content="Deskripsi halaman untuk SEO" />
    <meta name="robots" content="index, follow" />
    <link rel="canonical" href="https://example.com/halaman" />

    <!-- Open Graph -->
    <meta property="og:title" content="Judul Halaman" />
    <meta property="og:description" content="Deskripsi" />
    <meta property="og:image" content="https://example.com/og-image.jpg" />
    <meta property="og:url" content="https://example.com/halaman" />
    <meta property="og:type" content="website" />

    <!-- Twitter -->
    <meta name="twitter:card" content="summary_large_image" />

    <!-- Icons -->
    <link rel="icon" href="/favicon.ico" type="image/x-icon" />
    <link rel="apple-touch-icon" href="/icon-192.png" />

    <!-- CSS & Fonts -->
    <link rel="stylesheet" href="/style.css" />
    <link rel="preconnect" href="https://fonts.googleapis.com" />

    <!-- PWA -->
    <link rel="manifest" href="/manifest.json" />

    <!-- JavaScript -->
    <script src="/app.js" defer></script>
  </head>
  <body>
    <!-- Konten halaman -->
  </body>
</html>
```
