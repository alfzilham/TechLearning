# 07 - Grid

## Grid Container

| Properti                    | Penjelasan                    | Contoh                                             |
| --------------------------- | ----------------------------- | -------------------------------------------------- |
| `display: grid`             | Mengaktifkan CSS Grid         | `display: grid;`                                   |
| `grid-template-columns`     | Jumlah dan lebar kolom        | `grid-template-columns: 1fr 2fr 1fr;`              |
| `grid-template-rows`        | Tinggi baris                  | `grid-template-rows: auto 1fr auto;`               |
| `grid-template-areas`       | Layout dengan nama area       | `grid-template-areas: "header header header";`     |
| `grid-template` (Shorthand) | Gabungan columns, rows, areas | `grid-template: "header header" 80px / 1fr 250px;` |

Contoh lengkap:

```css
.grid {
  grid-template-columns: 200px 200px 200px;
}
.grid {
  grid-template-columns: 1fr 2fr 1fr;
}
.grid {
  grid-template-columns: repeat(3, 1fr);
}
.grid {
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}
.grid {
  grid-template-rows: 100px 200px 100px;
}
```

### `grid-template-areas` Layout:

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 200px;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header  header  header"
    "nav     main    aside"
    "footer  footer  footer";
  min-height: 100vh;
}

.header {
  grid-area: header;
}
.nav {
  grid-area: nav;
}
.main {
  grid-area: main;
}
.aside {
  grid-area: aside;
}
.footer {
  grid-area: footer;
}
```

---

## Gap

| Properti     | Penjelasan          | Contoh              |
| ------------ | ------------------- | ------------------- |
| `gap`        | Jarak baris & kolom | `gap: 16px;`        |
| `row-gap`    | Khusus antar baris  | `row-gap: 20px;`    |
| `column-gap` | Khusus antar kolom  | `column-gap: 12px;` |

---

## Grid Items Placement

| Properti      | Penjelasan                                                                  | Contoh                |
| ------------- | --------------------------------------------------------------------------- | --------------------- |
| `grid-column` | Posisi item berdasarkan garis kolom                                         | `grid-column: 1 / 3;` |
| `grid-row`    | Posisi item berdasarkan garis baris                                         | `grid-row: 1 / 3;`    |
| `grid-area`   | Nama area atau shorthand posisi (row-start / col-start / row-end / col-end) | `grid-area: header;`  |

```css
.item {
  grid-column: 1 / 3;
} /* garis 1 sampai 3 */
.item {
  grid-column: 1 / -1;
} /* awal sampai akhir */
.item {
  grid-column: 1 / span 2;
} /* mulai 1, ambil 2 kolom */
.item {
  grid-row: 1 / span 2;
}
.item {
  grid-area: 1 / 1 / 3 / 3;
} /* row-start / col-start / row-end / col-end */
```

---

## Alignment

| Properti                  | Penjelasan                                       | Contoh                     |
| ------------------------- | ------------------------------------------------ | -------------------------- |
| `justify-items`           | Perataan item horizontal di dalam cell           | `justify-items: center;`   |
| `align-items`             | Perataan item vertikal di dalam cell             | `align-items: center;`     |
| `place-items` (Shorthand) | Gabungan align-items dan justify-items           | `place-items: center;`     |
| `justify-content`         | Perataan grid dalam container (jika lebih kecil) | `justify-content: center;` |
| `align-content`           | Perataan vertikal grid dalam container           | `align-content: center;`   |
| `justify-self`            | Override justify-items per item                  | `justify-self: end;`       |
| `align-self`              | Override align-items per item                    | `align-self: center;`      |

---

## Implicit Grid

| Properti            | Penjelasan                                      | Contoh                                    |
| ------------------- | ----------------------------------------------- | ----------------------------------------- |
| `grid-auto-rows`    | Ukuran baris yang tidak didefinisikan eksplisit | `grid-auto-rows: 200px;`                  |
| `grid-auto-columns` | Ukuran kolom yang tidak didefinisikan eksplisit | `grid-auto-columns: minmax(100px, auto);` |
| `grid-auto-flow`    | Cara grid menempatkan item ekstra               | `grid-auto-flow: dense;`                  |

---

## Minmax & Auto

| Fungsi      | Penjelasan                                          | Contoh                                  |
| ----------- | --------------------------------------------------- | --------------------------------------- |
| `minmax()`  | Ukuran minimal dan maksimal                         | `minmax(150px, 1fr)`                    |
| `auto-fill` | Buat kolom sebanyak mungkin (termasuk kosong)       | `repeat(auto-fill, minmax(200px, 1fr))` |
| `auto-fit`  | Buat kolom sebanyak mungkin (kolom kosong collapse) | `repeat(auto-fit, minmax(200px, 1fr))`  |

---

## Common Patterns

```css
/* Card Grid Responsive */
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
}

/* Full Layout */
.layout {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: auto 1fr auto;
  grid-template-areas: "header header" "sidebar main" "footer footer";
  min-height: 100vh;
}

/* Centering Content */
.center {
  display: grid;
  place-items: center;
  min-height: 200px;
}

/* Masonry-like */
.masonry {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-flow: dense;
}
.wide {
  grid-column: span 2;
}
.tall {
  grid-row: span 2;
}
```
