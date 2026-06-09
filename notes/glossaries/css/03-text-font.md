# 03 - Text & Font

## Font Properties

| Properti           | Penjelasan                           | Contoh                              |
| ------------------ | ------------------------------------ | ----------------------------------- |
| `font-family`      | Jenis huruf                          | `font-family: Arial, sans-serif;`   |
| `font-size`        | Ukuran huruf                         | `font-size: 16px;`                  |
| `font-weight`      | Ketebalan huruf (100-900)            | `font-weight: 700;`                 |
| `font-style`       | Gaya huruf (miring)                  | `font-style: italic;`               |
| `font-variant`     | Varian font (small-caps)             | `font-variant: small-caps;`         |
| `line-height`      | Tinggi baris (jarak antar baris)     | `line-height: 1.5;`                 |
| `font` (Shorthand) | Semua properti font dalam satu baris | `font: 16px/1.5 Arial, sans-serif;` |

Contoh lengkap:

```css
body {
  font-family: Arial, sans-serif;
}
.heading {
  font-family: "Times New Roman", Georgia, serif;
}
.mono {
  font-family: "Courier New", monospace;
}

p {
  font-size: 16px;
}
h1 {
  font-size: 2rem;
}
.small {
  font-size: 0.8em;
}

.normal {
  font-weight: 400;
}
.bold {
  font-weight: 700;
}
.light {
  font-weight: 300;
}

.italic {
  font-style: italic;
}
.smallcaps {
  font-variant: small-caps;
}

body {
  font:
    16px/1.5 Arial,
    sans-serif;
}
h1 {
  font:
    bold 2rem/1.2 Georgia,
    serif;
}
```

---

## Text Properties

| Properti          | Penjelasan                           | Contoh                        |
| ----------------- | ------------------------------------ | ----------------------------- |
| `text-align`      | Perataan teks                        | `text-align: center;`         |
| `text-decoration` | Dekorasi teks (garis bawah, coret)   | `text-decoration: underline;` |
| `text-transform`  | Transformasi huruf                   | `text-transform: uppercase;`  |
| `text-indent`     | Indentasi baris pertama paragraf     | `text-indent: 2em;`           |
| `letter-spacing`  | Jarak antar huruf (tracking)         | `letter-spacing: 2px;`        |
| `word-spacing`    | Jarak antar kata                     | `word-spacing: 5px;`          |
| `white-space`     | Perilaku spasi putih dan wrapping    | `white-space: nowrap;`        |
| `word-break`      | Pemotongan kata yang terlalu panjang | `word-break: break-all;`      |
| `overflow-wrap`   | Membungkus kata panjang              | `overflow-wrap: break-word;`  |
| `text-overflow`   | Menangani teks overflow (ellipsis)   | `text-overflow: ellipsis;`    |

Contoh lengkap:

```css
.text-left {
  text-align: left;
}
.text-center {
  text-align: center;
}
.text-justify {
  text-align: justify;
}

.underline {
  text-decoration: underline;
}
.fancy {
  text-decoration: underline wavy red;
}

.upper {
  text-transform: uppercase;
}
.capitalize {
  text-transform: capitalize;
}

p {
  text-indent: 2em;
}
.spasi {
  letter-spacing: 2px;
}
.word-spasi {
  word-spacing: 5px;
}

.nowrap {
  white-space: nowrap;
}
.pre {
  white-space: pre;
}
.break {
  word-break: break-all;
}

.truncate {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

---

## Text Direction

| Properti       | Penjelasan                            | Contoh                         |
| -------------- | ------------------------------------- | ------------------------------ |
| `direction`    | Arah teks                             | `direction: rtl;`              |
| `unicode-bidi` | Bersama direction untuk override arah | `unicode-bidi: bidi-override;` |

---

## Web Fonts

| Properti                 | Penjelasan              | Contoh                                                               |
| ------------------------ | ----------------------- | -------------------------------------------------------------------- |
| `@font-face`             | Font kustom dari file   | `@font-face { font-family: "MyFont"; src: url("myfont.woff2"); }`    |
| `@import` (Google Fonts) | Import font dari Google | `@import url("https://fonts.googleapis.com/css2?family=Open+Sans");` |

Contoh lengkap:

```css
@font-face {
  font-family: "MyFont";
  src:
    url("myfont.woff2") format("woff2"),
    url("myfont.woff") format("woff");
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}

@import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;700&display=swap");

body {
  font-family: "Open Sans", sans-serif;
}
```

---

## Contoh Lengkap

```css
body {
  font-family:
    "Inter",
    -apple-system,
    sans-serif;
  font-size: 16px;
  line-height: 1.6;
  color: #333;
}

h1 {
  font:
    bold 2.5rem/1.2 Georgia,
    serif;
  letter-spacing: -0.5px;
  text-align: center;
}

p {
  text-indent: 2em;
  text-align: justify;
  word-spacing: 1px;
}

.link {
  text-decoration: none;
  color: #0066cc;
}
.link:hover {
  text-decoration: underline;
}

.card-title {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  font-weight: 600;
}
```
