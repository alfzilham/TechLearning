# 08 - Semantic HTML

## Struktur Halaman

| Tag         | Penjelasan                                     | Contoh                                                   |
| ----------- | ---------------------------------------------- | -------------------------------------------------------- |
| `<header>`  | Bagian kepala halaman/section (logo, navigasi) | `<header><img src="logo.png" /><nav>...</nav></header>`  |
| `<nav>`     | Navigasi — menu utama, daftar link             | `<nav><ul><li><a href="/">Beranda</a></li></ul></nav>`   |
| `<main>`    | Konten utama (hanya SATU per halaman)          | `<main><h1>Judul</h1><p>Konten...</p></main>`            |
| `<section>` | Kelompok konten yang tematis                   | `<section><h2>Fitur Produk</h2><p>...</p></section>`     |
| `<article>` | Konten independen yang bisa berdiri sendiri    | `<article><h2>Judul Artikel</h2><p>Isi...</p></article>` |
| `<aside>`   | Konten sampingan (sidebar, iklan)              | `<aside><h3>Artikel Terkait</h3><ul>...</ul></aside>`    |
| `<footer>`  | Bagian kaki halaman (copyright, link)          | `<footer><p>&copy; 2024 Perusahaan Kami</p></footer>`    |

## Struktur Halaman Lengkap

```html
<body>
  <header>
    <nav>
      <ul>
        <li><a href="/">Beranda</a></li>
        <li><a href="/blog">Blog</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <article>
      <header>
        <h1>Judul Artikel Blog</h1>
        <p>Penulis: Rizky | <time>15 Jan 2024</time></p>
      </header>
      <section>
        <h2>Pendahuluan</h2>
        <p>Isi pendahuluan...</p>
      </section>
      <section>
        <h2>Pembahasan</h2>
        <p>Detail pembahasan...</p>
      </section>
      <footer>
        <p>Tag: <a href="#">html</a>, <a href="#">web</a></p>
      </footer>
    </article>

    <aside>
      <h3>Artikel Populer</h3>
      <ul>
        <li><a href="#">Belajar CSS</a></li>
        <li><a href="#">JavaScript Dasar</a></li>
      </ul>
    </aside>
  </main>

  <footer><p>&copy; 2024 Blog Belajar</p></footer>
</body>
```

## Semantic Lainnya

| Tag            | Penjelasan                                 | Contoh                                                                         |
| -------------- | ------------------------------------------ | ------------------------------------------------------------------------------ |
| `<figure>`     | Konten ilustrasi dengan keterangan         | `<figure><img src="grafik.png" /><figcaption>Keterangan</figcaption></figure>` |
| `<figcaption>` | Keterangan untuk figure                    | `<figcaption>Grafik penjualan Q1 2024</figcaption>`                            |
| `<details>`    | Konten collapsible (buka/tutup)            | `<details><summary>Klik</summary><p>Konten</p></details>`                      |
| `<summary>`    | Judul yang diklik untuk buka/tutup details | `<summary>Klik untuk lihat detail</summary>`                                   |
| `<dialog>`     | Modal/popup dialog                         | `<dialog id="modal"><h2>Konfirmasi</h2><p>Yakin?</p></dialog>`                 |
| `<mark>`       | Teks ditandai/di-highlight                 | `<mark>paling penting</mark>`                                                  |
| `<time>`       | Waktu machine-readable                     | `<time datetime="2024-12-25T19:00:00+07:00">25 Des 2024</time>`                |

```html
<details>
  <summary>Klik untuk lihat detail</summary>
  <p>Ini konten yang tersembunyi sampai diklik.</p>
  <ul>
    <li>Detail 1</li>
    <li>Detail 2</li>
  </ul>
</details>
```

```html
<dialog id="modal">
  <h2>Konfirmasi</h2>
  <p>Apakah anda yakin?</p>
  <button onclick="this.closest('dialog').close()">Ya</button>
  <button onclick="this.closest('dialog').close()">Tidak</button>
</dialog>
<button onclick="document.getElementById('modal').showModal()">
  Buka Modal
</button>
```

## Non-Semantic (Tapi Berguna)

| Tag      | Penjelasan                                         | Contoh                                    |
| -------- | -------------------------------------------------- | ----------------------------------------- |
| `<div>`  | Container block tanpa makna (untuk layout/styling) | `<div class="container">...</div>`        |
| `<span>` | Container inline tanpa makna (untuk teks styling)  | `<span class="highlight">berwarna</span>` |

## Perbandingan Semantic vs Non-Semantic

| Semantic    | Non-Semantic            | Fungsi            |
| ----------- | ----------------------- | ----------------- |
| `<header>`  | `<div class="header">`  | Bagian atas       |
| `<nav>`     | `<div class="nav">`     | Navigasi          |
| `<main>`    | `<div class="main">`    | Konten utama      |
| `<section>` | `<div class="section">` | Kelompok konten   |
| `<article>` | `<div class="article">` | Konten independen |
| `<aside>`   | `<div class="sidebar">` | Sampingan         |
| `<footer>`  | `<div class="footer">`  | Bagian bawah      |
| `<figure>`  | `<div class="figure">`  | Gambar + caption  |
