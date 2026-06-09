# 06 - Flexbox

## Flex Container

| Properti                | Penjelasan                                | Contoh                 |
| ----------------------- | ----------------------------------------- | ---------------------- |
| `display: flex`         | Mengaktifkan Flexbox pada container       | `display: flex;`       |
| `flex-direction`        | Arah utama flex items                     | `flex-direction: row;` |
| `flex-wrap`             | Membungkus item jika melebihi container   | `flex-wrap: wrap;`     |
| `flex-flow` (Shorthand) | Gabungan `flex-direction` dan `flex-wrap` | `flex-flow: row wrap;` |

```css
.container {
  display: flex;
}
.row {
  flex-direction: row;
}
.column {
  flex-direction: column;
}
.column-reverse {
  flex-direction: column-reverse;
}
.nowrap {
  flex-wrap: nowrap;
}
.wrap {
  flex-wrap: wrap;
}
```

---

## Alignment (Main Axis)

| Properti                         | Penjelasan                 | Contoh                            |
| -------------------------------- | -------------------------- | --------------------------------- |
| `justify-content: flex-start`    | Ke kiri (default)          | `justify-content: flex-start;`    |
| `justify-content: flex-end`      | Ke kanan                   | `justify-content: flex-end;`      |
| `justify-content: center`        | Tengah                     | `justify-content: center;`        |
| `justify-content: space-between` | Rata kiri-kanan            | `justify-content: space-between;` |
| `justify-content: space-around`  | Rata dengan setengah jarak | `justify-content: space-around;`  |
| `justify-content: space-evenly`  | Jarak sama rata            | `justify-content: space-evenly;`  |

---

## Alignment (Cross Axis)

| Properti                  | Penjelasan                                       | Contoh                     |
| ------------------------- | ------------------------------------------------ | -------------------------- |
| `align-items: stretch`    | Tinggi penuh (default)                           | `align-items: stretch;`    |
| `align-items: flex-start` | Ke atas                                          | `align-items: flex-start;` |
| `align-items: flex-end`   | Ke bawah                                         | `align-items: flex-end;`   |
| `align-items: center`     | Tengah vertikal                                  | `align-items: center;`     |
| `align-content`           | Perataan multiple baris (jika `flex-wrap: wrap`) | `align-content: center;`   |

---

## Flex Items

| Properti           | Penjelasan                                    | Contoh                    |
| ------------------ | --------------------------------------------- | ------------------------- |
| `flex-grow`        | Seberapa banyak item bisa membesar (proporsi) | `flex-grow: 1;`           |
| `flex-shrink`      | Seberapa banyak item bisa mengecil            | `flex-shrink: 0;`         |
| `flex-basis`       | Ukuran dasar sebelum grow/shrink              | `flex-basis: 200px;`      |
| `flex` (Shorthand) | Gabungan grow, shrink, basis                  | `flex: 1;`                |
| `align-self`       | Override `align-items` untuk item tertentu    | `align-self: flex-start;` |
| `order`            | Urutan item (default 0, kecil = duluan)       | `order: 1;`               |

```css
.item1 {
  flex-grow: 1;
}
.item2 {
  flex-grow: 2;
}
.no-shrink {
  flex-shrink: 0;
}
.fixed {
  flex-basis: 200px;
}
.item {
  flex: 1;
} /* flex: 1 1 0% */
.item {
  flex: 0 0 auto;
} /* tidak membesar/mengecil */
.item {
  flex: 1 1 200px;
} /* grow 1, shrink 1, basis 200px */

.top {
  align-self: flex-start;
}
.bottom {
  align-self: flex-end;
}
.item1 {
  order: 2;
}
.item2 {
  order: 1;
} /* muncul duluan */
```

---

## Gap

| Properti     | Penjelasan                                   | Contoh              |
| ------------ | -------------------------------------------- | ------------------- |
| `gap`        | Jarak antar flex items horizontal & vertikal | `gap: 16px;`        |
| `row-gap`    | Khusus jarak vertikal                        | `row-gap: 20px;`    |
| `column-gap` | Khusus jarak horizontal                      | `column-gap: 12px;` |

---

## Common Patterns

```css
/* Tengah Sempurna */
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Navbar */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 16px 24px;
}
.nav-links {
  display: flex;
  gap: 16px;
  list-style: none;
}

/* Card Grid */
.grid {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
.card {
  flex: 1 1 300px;
}

/* Sticky Footer */
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
.content {
  flex: 1;
}

/* Holy Grail Layout */
.container {
  display: flex;
  flex-wrap: wrap;
}
.header {
  flex: 0 0 100%;
}
.nav {
  flex: 0 0 200px;
}
.main {
  flex: 1;
}
.sidebar {
  flex: 0 0 200px;
}
.footer {
  flex: 0 0 100%;
}
```
