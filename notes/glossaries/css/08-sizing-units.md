# 08 - Sizing & Units

## Width & Height

| Properti                   | Penjelasan      | Contoh               |
| -------------------------- | --------------- | -------------------- |
| `width`                    | Lebar elemen    | `width: 300px;`      |
| `height`                   | Tinggi elemen   | `height: 200px;`     |
| `min-width` / `min-height` | Ukuran minimal  | `min-width: 200px;`  |
| `max-width` / `max-height` | Ukuran maksimal | `max-width: 1200px;` |

```css
img {
  max-width: 100%;
  height: auto;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
}
```

---

## CSS Units

### Absolute Units

| Unit        | Penjelasan                            | Contoh             |
| ----------- | ------------------------------------- | ------------------ |
| `px`        | Pixel (1px = 1/96 inch)               | `width: 100px;`    |
| `pt`        | Point (1pt = 1/72 inch) — untuk print | `font-size: 12pt;` |
| `cm` / `mm` | Centimeter / milimeter                | `width: 5cm;`      |
| `in`        | Inch                                  | `width: 2in;`      |
| `pc`        | Pica (1pc = 12pt)                     | `font-size: 1pc;`  |

### Relative Units (Rekomendasi)

| Unit            | Penjelasan                                              | Contoh             |
| --------------- | ------------------------------------------------------- | ------------------ |
| `%`             | Persen dari parent                                      | `width: 50%;`      |
| `em`            | Relatif terhadap font-size elemen sendiri (atau parent) | `font-size: 2em;`  |
| `rem`           | Relatif terhadap font-size root (`<html>`)              | `font-size: 2rem;` |
| `vw`            | 1% dari lebar viewport                                  | `width: 100vw;`    |
| `vh`            | 1% dari tinggi viewport                                 | `height: 100vh;`   |
| `vmin` / `vmax` | 1% dari ukuran terkecil / terbesar viewport             | `width: 50vmin;`   |

```css
html {
  font-size: 16px;
}
h1 {
  font-size: 2rem;
} /* 2 × 16px = 32px */
p {
  font-size: 1rem;
} /* 1 × 16px = 16px */
.full-screen {
  height: 100vh;
}
.hero {
  min-height: 80vh;
}
.half-width {
  width: 50vw;
}
.square {
  width: 50vmin;
  height: 50vmin;
}
```

---

## Modern CSS Functions

| Fungsi    | Penjelasan                           | Contoh                             |
| --------- | ------------------------------------ | ---------------------------------- |
| `calc()`  | Kalkulasi matematika untuk nilai CSS | `width: calc(100% - 40px);`        |
| `min()`   | Ambil nilai terkecil                 | `width: min(100%, 400px);`         |
| `max()`   | Ambil nilai terbesar                 | `width: max(300px, 50%);`          |
| `clamp()` | Nilai dengan batas bawah dan atas    | `width: clamp(280px, 50%, 800px);` |

```css
.box {
  width: calc(100% - 40px);
}
.box {
  height: calc(100vh - 80px);
}
.box {
  padding: calc(1rem + 2px);
}
.box {
  width: min(100%, 400px);
}
.box {
  width: max(300px, 50%);
}
h1 {
  font-size: clamp(1.5rem, 4vw, 3rem);
}
```

---

## Sizing Patterns

```css
/* Responsive Typography */
html {
  font-size: clamp(16px, 1vw + 14px, 22px);
}

/* Fluid Container */
.container {
  width: min(100% - 2rem, 1200px);
  margin-inline: auto;
}

/* Aspect Ratio */
.video {
  aspect-ratio: 16 / 9;
}
.square {
  aspect-ratio: 1 / 1;
}
```
