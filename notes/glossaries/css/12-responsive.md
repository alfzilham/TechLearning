# 12 - Responsive Design

## Viewport Meta Tag

Wajib untuk responsive:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

- `width=device-width` → lebar = lebar device
- `initial-scale=1.0` → zoom level awal

---

## Media Queries

| Properti | Penjelasan                               | Contoh                              |
| -------- | ---------------------------------------- | ----------------------------------- |
| `@media` | Menerapkan CSS berdasarkan kondisi layar | `@media (min-width: 768px) { ... }` |

### Jenis Media Query

| Tipe                     | Penjelasan                     | Contoh                                                      |
| ------------------------ | ------------------------------ | ----------------------------------------------------------- |
| `max-width`              | Desktop-first                  | `@media (max-width: 767px) { ... }`                         |
| `min-width`              | Mobile-first                   | `@media (min-width: 768px) { ... }`                         |
| Range                    | Antara dua ukuran              | `@media (min-width: 768px) and (max-width: 1023px) { ... }` |
| `orientation`            | Landscape / portrait           | `@media (orientation: landscape) { ... }`                   |
| `min-resolution`         | Retina / resolusi tinggi       | `@media (min-resolution: 2dppx) { ... }`                    |
| `prefers-color-scheme`   | Dark / light mode              | `@media (prefers-color-scheme: dark) { ... }`               |
| `prefers-reduced-motion` | User sensitif animasi          | `@media (prefers-reduced-motion: reduce) { ... }`           |
| `hover`                  | Device dengan hover / touch    | `@media (hover: hover) { ... }`                             |
| `pointer`                | Presisi pointer (mouse / jari) | `@media (pointer: fine) { ... }`                            |

### Ukuran Breakpoint Umum

```css
/* Mobile: 0 - 575px — no query (base style) */
/* Small tablet: 576px+  */  @media (min-width: 576px) { ... }
/* Tablet: 768px+ */         @media (min-width: 768px) { ... }
/* Desktop kecil: 992px+ */  @media (min-width: 992px) { ... }
/* Desktop besar: 1200px+ */ @media (min-width: 1200px) { ... }
/* Layar lebar: 1400px+ */   @media (min-width: 1400px) { ... }
```

---

## Responsive Units & Functions

| Fungsi / Unit     | Penjelasan                   | Contoh                                 |
| ----------------- | ---------------------------- | -------------------------------------- |
| `clamp()`         | Responsive tanpa media query | `font-size: clamp(1.5rem, 4vw, 3rem);` |
| `min()` / `max()` | Nilai minimal / maksimal     | `width: min(100% - 2rem, 1200px);`     |
| `vw` / `vh`       | Unit viewport                | `min-height: 80vh;`                    |

---

## Responsive Layout Patterns

```css
/* Flexible Grid (tanpa media query) */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 16px;
}

/* Flexible Flexbox */
.flex-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
.flex-grid > * {
  flex: 1 1 280px;
}

/* Responsive Padding */
.container {
  padding: 16px;
}
@media (min-width: 768px) {
  .container {
    padding: 24px;
  }
}
@media (min-width: 1024px) {
  .container {
    padding: 32px;
  }
}

/* Responsive Font */
body {
  font-size: 16px;
}
@media (min-width: 768px) {
  body {
    font-size: 18px;
  }
}
@media (min-width: 1200px) {
  body {
    font-size: 20px;
  }
}
```

---

## Images & Media

| Properti          | Penjelasan       | Contoh                                   |
| ----------------- | ---------------- | ---------------------------------------- |
| `max-width: 100%` | Gambar responsif | `img { max-width: 100%; height: auto; }` |

### Responsive Video / Iframe

```css
.video-container {
  position: relative;
  width: 100%;
  padding-bottom: 56.25%; /* 16:9 */
  height: 0;
  overflow: hidden;
}
.video-container iframe,
.video-container video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
```

### Picture Element (HTML)

```html
<picture>
  <source media="(min-width: 1024px)" srcset="large.webp" />
  <source media="(min-width: 768px)" srcset="medium.webp" />
  <img src="small.webp" alt="Responsive" />
</picture>
```

---

## Hide / Show

```css
/* Mobile-first: sembunyi di mobile, tampil di desktop */
.desktop-only {
  display: none;
}
@media (min-width: 1024px) {
  .desktop-only {
    display: block;
  }
}

/* Desktop-first: tampil di mobile, sembunyi di desktop */
.mobile-only {
  display: block;
}
@media (min-width: 1024px) {
  .mobile-only {
    display: none;
  }
}
```

---

## Dark Mode

| Teknik                 | Penjelasan                              | Contoh                                                             |
| ---------------------- | --------------------------------------- | ------------------------------------------------------------------ |
| `prefers-color-scheme` | Dark mode berdasarkan preferensi sistem | `@media (prefers-color-scheme: dark) { :root { --bg: #1a1a2e; } }` |
| `[data-theme]`         | Dark mode toggle dengan class/attr      | `[data-theme="dark"] { --bg: #1a1a2e; }`                           |

```css
:root {
  --bg: white;
  --text: #333;
}
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #1a1a2e;
    --text: #e0e0e0;
  }
}
body {
  background: var(--bg);
  color: var(--text);
}
```

---

## Accessibility

```css
/* Matikan animasi untuk user yang sensitif */
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
  }
}
```

---

## Contoh Halaman Responsive Lengkap

```css
/* Base (mobile) */
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  font-family: Arial, sans-serif;
}
.container {
  width: 100%;
  padding: 0 16px;
}
.nav-links {
  display: none;
}
.hamburger {
  display: block;
}
.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

/* Tablet */
@media (min-width: 768px) {
  .container {
    padding: 0 24px;
  }
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Desktop */
@media (min-width: 1024px) {
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 32px;
  }
  .nav-links {
    display: flex;
  }
  .hamburger {
    display: none;
  }
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
```
