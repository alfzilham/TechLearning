# Phase 1: HTML + CSS — Web Foundation

**Durasi:** 7 hari (Minggu 1)
**Tujuan:** Membuat landing page responsif tanpa bantuan AI

---

## Kenapa HTML + CSS Penting?

HTML dan CSS adalah fondasi dari semua yang akan Anda buat. React, Next.js, Vue — semuanya pada akhirnya menghasilkan HTML + CSS. Jika fondasi tidak kuat, bangunan di atasnya akan runtuh.

---

## Kurikulum Harian

### Hari 1: Semantic HTML

**Konsep:**
- Struktur dokumen HTML (`<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`)
- Tag semantic: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`
- Kenapa semantic? — Accessibility (screen reader), SEO, maintainability
- Attribute: `class`, `id`, `src`, `href`, `alt`, `title`
- Text: `<h1>`-`<h6>`, `<p>`, `<span>`, `<strong>`, `<em>`
- Link: `<a href="..." target="_blank">`
- Image: `<img src="..." alt="...">`

**Tugas:**
Buat file `index.html` dengan struktur semantic yang berisi:
- Header dengan judul website
- Navigasi (Home, About, Projects, Contact)
- Main content dengan 3 section
- Footer dengan copyright

**Checklist:**
- [ ] Bisa jelaskan perbedaan `<div>` dan `<section>`
- [ ] Tahu kapan pake `<article>` vs `<section>`
- [ ] Semua gambar punya `alt` text

---

### Hari 2: Forms & Tables

**Konsep:**
- `<form>`, `<input>` (text, email, password, number), `<textarea>`, `<select>`, `<button>`
- Form attribute: `action`, `method`, `required`, `placeholder`, `disabled`
- Label: `<label for="...">`
- Table: `<table>`, `<thead>`, `<tbody>`, `<tr>`, `<th>`, `<td>`

**Tugas:**
- Buat form kontak (nama, email, pesan, submit button)
- Buat table jadwal (hari, jam, kegiatan)

---

### Hari 3: CSS Dasar & Box Model

**Konsep:**
- Cara pasang CSS: inline, `<style>`, file `.css` eksternal
- Selector: element, class (`.`), id (`#`), descendant (` `), specificity
- Box Model: `content` → `padding` → `border` → `margin`
- `width`, `height`, `display` (block, inline, inline-block, none)
- Color: named, hex (`#ff0000`), rgb, hsl

**Visual Box Model:**
```
┌─────────────────────────────────┐
│          MARGIN (transparan)     │
│  ┌───────────────────────────┐  │
│  │       BORDER              │  │
│  │  ┌─────────────────────┐  │  │
│  │  │     PADDING          │  │  │
│  │  │  ┌───────────────┐  │  │  │
│  │  │  │    CONTENT    │  │  │  │
│  │  │  └───────────────┘  │  │  │
│  │  └─────────────────────┘  │  │
│  └───────────────────────────┘  │
└─────────────────────────────────┘
```

**Tugas:**
- Styling halaman hari 1 dengan CSS eksternal
- Bermain padding/margin untuk lihat perbedaan
- Buat card component dengan border, padding, margin

---

### Hari 4: Flexbox

**Konsep:**
- `display: flex`
- Main axis vs Cross axis
- `flex-direction`, `justify-content`, `align-items`
- `flex-wrap`, `gap`
- `flex`: grow, shrink, basis

**Tugas:**
- Buat navbar horizontal
- Buat grid 3 card yang rapi pakai flex
- Buat layout: sidebar kiri + konten kanan
- Buat card yang center horizontal & vertical

---

### Hari 5: CSS Grid

**Konsep:**
- `display: grid`
- `grid-template-columns`, `grid-template-rows`
- `grid-column`, `grid-row` (span)
- `gap`
- `grid-template-areas`

**Tugas:**
- Buat layout website lengkap dengan grid: header, nav, main, sidebar, footer
- Galeri foto 3 kolom
- Responsive grid yang berubah kolom berdasarkan lebar layar

---

### Hari 6: CSS Lanjutan & Responsive Design

**Konsep:**
- CSS Variables (`--primary-color: blue; var(--primary-color)`)
- Pseudo-class: `:hover`, `:focus`, `:nth-child()`, `:first-child`, `:last-child`
- Pseudo-element: `::before`, `::after`
- Media queries: `@media (max-width: 768px) { ... }`
- Mobile-first vs Desktop-first
- Unit: `px`, `rem`, `em`, `%`, `vh`, `vw`

**Tugas:**
- Buat komponen yang stylenya berubah saat di-hover
- Buat halaman yang responsif: desktop 3 kolom, tablet 2 kolom, mobile 1 kolom

---

### Hari 7: Mini Project — Landing Page Portfolio

**Spesifikasi:**
Buat landing page portfolio pribadi dengan:

1. **Header**: Nama + tagline
2. **Navbar**: Home, About, Skills, Projects, Contact — sticky di atas
3. **Hero section**: Foto (atau placeholder), nama, deskripsi singkat, CTA button
4. **About section**: Paragraf tentang diri
5. **Skills section**: Grid icons atau card skill
6. **Projects section**: Minimal 3 project card (gambar + judul + deskripsi + link)
7. **Contact section**: Form kontak (nama, email, pesan)
8. **Footer**: Copyright + social media links

**Teknis:**
- Responsive (desktop + tablet + mobile)
- Semantic HTML
- CSS Flexbox/Grid
- CSS Variables untuk warna
- Hover effect di card dan button
- Smooth scroll untuk navigasi

**DILARANG:**
- Framework CSS (Tailwind, Bootstrap, dll)
- JavaScript
- Copy-paste dari mana pun

---

## Referensi

- [MDN: HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [MDN: CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [Flexbox Froggy](https://flexboxfroggy.com/) — game belajar flexbox
- [CSS Grid Garden](https://cssgridgarden.com/) — game belajar grid
- [web.dev: Learn Responsive Design](https://web.dev/learn/design/)

## Checklist Penguasaan

Sebelum lanjut ke JavaScript, pastikan bisa:
- [ ] Membuat halaman HTML dengan struktur semantic
- [ ] Menjelaskan box model dan perbedaan padding/margin
- [ ] Membuat layout dengan Flexbox (navbar, card grid, centering)
- [ ] Membuat layout dengan Grid (halaman penuh)
- [ ] Membuat halaman yang responsif di 3 ukuran layar
- [ ] Menggunakan CSS Variables
- [ ] Membuat landing page dari 0 tanpa bantuan
