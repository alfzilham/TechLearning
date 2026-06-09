## Kenapa Semantic HTML?

Dulu orang bikin website pake <div> untuk semuanya. Hasilnya? Kode amburadul, susah dibaca, susah di-maintain, dan tidak accessible buat screen reader. HTML semantic datang untuk kasih makna ke setiap elemen.
Bandingkan:

<!-- ❌ Non-semantic -->
<div class="header">
<div class="nav">
<div class="main">

<!-- ✅ Semantic -->
<header>
<nav>
<main>

> Screen reader, search engine (SEO), dan developer lain bisa langsung paham struktur halaman tanpa perlu lihat CSS.

---

# Materi Hari ini:

## Elements dasar HTML

<header>           : Terletak di bagian atas halaman/section website.
<nav>              : Navigasi utama sebuah website.
<main>             : isi atau konten utama website.
<section>          : Pengelompokan Content website yang relate.
<article>          : Content untuk sebuah artikel, blog, atau post.
<aside>            : Navigasi samping website, atau sering disebut dengan sidebar.
<footer>           : Footer website, atau bagian bawah halaman/section website.
<h1> - <h6>        : Judul halaman atau section.
<p>                : Paragraf atau kalimat.
<a>                : Link atau hyperlink.
<img>              : Tag untuk input gambar. component wajib: src, alt.
<ul> / <ol> / <li> : list atau item list yang beraturan atau tidak beraturan.

## Contoh penggunaan:

<header>            <!-- Header website yang terletak setelah <body> yang diisi dengan navbar-->
    <nav>
        <li>...</li>
        <li>...</li>
    </nav>
</header>

<main>            <!-- Isi atau konten utama website yang diisi dengan section -->
    <section>
        <h1>Hero</h1>
        <p>...</p>
    </section>
</main>

<footer>            <!-- Footer website yang terletak di bagian bawah halaman/section website -->
    <p>...</p>
</footer>

---

# Catatan Koreksi AI:

1. <li> tanpa <ul> (baris 14-31)

<!-- ❌ Salah -->
<nav>
    <li>...</li>
    <li>...</li>
</nav>

<!-- ✅ Benar -->
<nav>
    <ul>
        <li>...</li>
        <li>...</li>
    </ul>
</nav>
<li> 

> tidak bisa berdiri sendiri — harus di dalam <ul>, <ol>, atau <menu>.

2. Semua heading <h1> (baris 39, 47, 55, 63, 71)
<!-- ❌ 5 buah <h1> dalam 1 halaman -->
<h1>Hero</h1>
<h1>About</h1>
<h1>Project</h1>

<!-- ✅ 1 <h1> saja, sisanya <h2> -->
<h1>Hero</h1>
<h2>About</h2>
<h2>Project</h2>

> Aturan: hanya SATU <h1> per halaman. <h1> adalah judul utama, <h2> untuk judul section.

3. type="text" untuk email (baris 80)

<!-- ❌ Tidak validasi format email -->
<input type="text" id="email">

<!-- ✅ Browser otomatis validasi email -->
<input type="email" id="email">
