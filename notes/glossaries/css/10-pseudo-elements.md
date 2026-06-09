# 10 - Pseudo-elements

Pseudo-elements adalah "elemen virtual" yang bisa ditambahkan ke halaman via CSS. Ditulis dengan `::`.

## `::before` dan `::after`

| Selector   | Penjelasan                                                | Contoh                                |
| ---------- | --------------------------------------------------------- | ------------------------------------- |
| `::before` | Menambahkan konten sebelum elemen (WAJIB punya `content`) | `.element::before { content: "→ "; }` |
| `::after`  | Menambahkan konten sesudah elemen (WAJIB punya `content`) | `.element::after { content: " ←"; }`  |

### `content` Property

| Nilai        | Penjelasan                            | Contoh                                  |
| ------------ | ------------------------------------- | --------------------------------------- |
| `"teks"`     | Teks string                           | `content: " ↗";`                        |
| `""`         | String kosong (untuk dekorasi visual) | `content: ""; display: block;`          |
| `attr(x)`    | Ambil nilai atribut dari elemen       | `content: " (" attr(href) ")";`         |
| `counter(x)` | Counter CSS                           | `content: "Chapter " counter(chapter);` |

---

## Common Uses

```css
/* Icon / Emoji */
.email::before {
  content: "📧 ";
  margin-right: 4px;
}
.pdf-link::after {
  content: "📄";
  margin-left: 4px;
}
.verified::after {
  content: "✓";
  color: green;
}

/* Clearfix */
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

/* Quote Decoration */
blockquote::before {
  content: '"';
  font-size: 3em;
  color: #ccc;
}

/* File type indicator */
a[href$=".pdf"]::after {
  content: " (PDF)";
}
a[href$=".doc"]::after {
  content: " (Word)";
}
a[href$=".zip"]::after {
  content: " (ZIP)";
}
```

### Tooltip with `::after`

```css
[data-tooltip] {
  position: relative;
}
[data-tooltip]::after {
  content: attr(data-tooltip);
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  background: #333;
  color: white;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 12px;
  white-space: nowrap;
  opacity: 0;
  transition: opacity 0.2s;
}
[data-tooltip]:hover::after {
  opacity: 1;
}
```

### Custom Checkbox

```css
input[type="checkbox"] {
  appearance: none;
  width: 20px;
  height: 20px;
  border: 2px solid #ccc;
  border-radius: 4px;
}
input[type="checkbox"]:checked {
  background: blue;
  border-color: blue;
}
input[type="checkbox"]:checked::after {
  content: "✓";
  display: block;
  color: white;
  text-align: center;
  line-height: 18px;
}
```

---

## `::first-letter`

| Selector         | Penjelasan                                     | Contoh                                             |
| ---------------- | ---------------------------------------------- | -------------------------------------------------- |
| `::first-letter` | Style huruf pertama dalam teks (efek drop cap) | `p::first-letter { font-size: 3em; float: left; }` |

Properti yang bisa digunakan: `color`, `font`, `background`, `margin`, `padding`, `border`, `float`, `line-height`, `text-decoration`, `text-transform`, `letter-spacing`, `word-spacing`.

```css
p::first-letter {
  font-size: 3em;
  font-weight: bold;
  color: red;
  float: left;
  margin-right: 8px;
}
```

---

## `::first-line`

| Selector       | Penjelasan               | Contoh                                              |
| -------------- | ------------------------ | --------------------------------------------------- |
| `::first-line` | Style baris pertama teks | `p::first-line { font-weight: bold; color: #333; }` |

Properti yang bisa digunakan: `color`, `font`, `background`, `line-height`, `letter-spacing`, `word-spacing`, `text-decoration`, `text-transform`.

---

## `::selection`

| Selector      | Penjelasan                            | Contoh                                               |
| ------------- | ------------------------------------- | ---------------------------------------------------- |
| `::selection` | Style saat user memilih/menandai teks | `::selection { background: #0066ff; color: white; }` |

---

## `::placeholder`

| Selector        | Penjelasan                        | Contoh                                                    |
| --------------- | --------------------------------- | --------------------------------------------------------- |
| `::placeholder` | Style teks placeholder pada input | `input::placeholder { color: #999; font-style: italic; }` |

```css
input::placeholder {
  color: #999;
  font-style: italic;
  font-size: 0.9em;
}
/* Vendor prefix */
input::-webkit-input-placeholder {
  color: #999;
}
```

---

## `::marker`

| Selector   | Penjelasan                                      | Contoh                                          |
| ---------- | ----------------------------------------------- | ----------------------------------------------- |
| `::marker` | Style bullet/angka pada `<li>` atau `<summary>` | `li::marker { color: red; font-weight: bold; }` |

```css
ul li::marker {
  content: "▶ ";
  font-size: 0.8em;
}
ol li::marker {
  color: blue;
  font-weight: bold;
}
details summary::marker {
  color: orange;
}
```

---

## `::backdrop`

| Selector     | Penjelasan                             | Contoh                                                                          |
| ------------ | -------------------------------------- | ------------------------------------------------------------------------------- |
| `::backdrop` | Latar belakang modal/dialog fullscreen | `dialog::backdrop { background: rgba(0,0,0,0.5); backdrop-filter: blur(4px); }` |

---

## Contoh Lengkap

```css
/* Custom ordered list dengan style */
ol {
  list-style: none;
  counter-reset: item;
}
ol li {
  counter-increment: item;
  margin-bottom: 8px;
}
ol li::before {
  content: counter(item) ".";
  color: #0066ff;
  font-weight: bold;
  margin-right: 8px;
}

/* Quote block */
blockquote {
  position: relative;
  padding: 16px 24px;
  background: #f9f9f9;
  border-left: 4px solid #ccc;
}
blockquote::before {
  content: open-quote;
  font-size: 4em;
  position: absolute;
  top: -10px;
  left: 8px;
  color: #ddd;
}

/* Image hover overlay */
.img-wrapper {
  position: relative;
}
.img-wrapper::after {
  content: "🔍 Lihat";
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s;
}
.img-wrapper:hover::after {
  opacity: 1;
}
```
