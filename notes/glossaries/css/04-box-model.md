# 04 - Box Model

Setiap elemen HTML adalah kotak (box).

```
┌─────────────────────────────┐
│         MARGIN              │
│  ┌───────────────────────┐  │
│  │       BORDER          │  │
│  │  ┌─────────────────┐  │  │
│  │  │    PADDING      │  │  │
│  │  │  ┌───────────┐  │  │  │
│  │  │  │  CONTENT  │  │  │  │
│  │  │  └───────────┘  │  │  │
│  │  └─────────────────┘  │  │
│  └───────────────────────┘  │
└─────────────────────────────┘
```

## Content

| Properti | Penjelasan    | Contoh           |
| -------- | ------------- | ---------------- |
| `width`  | Lebar konten  | `width: 300px;`  |
| `height` | Tinggi konten | `height: 200px;` |

---

## Padding

| Properti           | Penjelasan            | Contoh                          |
| ------------------ | --------------------- | ------------------------------- |
| `padding`          | Semua sisi            | `padding: 20px;`                |
| `padding: a b`     | Atas-bawah kiri-kanan | `padding: 10px 20px;`           |
| `padding: a b c`   | Atas kiri-kanan bawah | `padding: 10px 20px 15px;`      |
| `padding: a b c d` | Atas kanan bawah kiri | `padding: 10px 15px 20px 25px;` |
| `padding-top`      | Padding atas saja     | `padding-top: 10px;`            |
| `padding-right`    | Padding kanan saja    | `padding-right: 15px;`          |
| `padding-bottom`   | Padding bawah saja    | `padding-bottom: 20px;`         |
| `padding-left`     | Padding kiri saja     | `padding-left: 25px;`           |

---

## Border

| Properti                       | Penjelasan                                       | Contoh                            |
| ------------------------------ | ------------------------------------------------ | --------------------------------- |
| `border-width`                 | Ketebalan border                                 | `border-width: 2px;`              |
| `border-style`                 | Gaya border (solid, dashed, dotted, dll)         | `border-style: solid;`            |
| `border-color`                 | Warna border                                     | `border-color: red;`              |
| `border` (Shorthand)           | Semua properti border dalam satu baris           | `border: 2px solid #333;`         |
| `border-top/right/bottom/left` | Per sisi border                                  | `border-bottom: 3px dashed blue;` |
| `border-radius`                | Sudut melengkung                                 | `border-radius: 8px;`             |
| `border-collapse`              | Untuk tabel — menggabungkan border               | `border-collapse: collapse;`      |
| `outline`                      | Garis di luar border (tidak mempengaruhi ukuran) | `outline: 2px solid blue;`        |

Contoh lengkap:

```css
.box {
  border: 2px solid #333;
}
.bottom {
  border-bottom: 3px dashed blue;
}
.left {
  border-left: 4px solid green;
}
.rounded {
  border-radius: 8px;
}
.circle {
  border-radius: 50%;
}
.pill {
  border-radius: 999px;
}

input:focus {
  outline: 2px solid blue;
  outline-offset: 2px;
}
```

---

## Margin

| Properti                       | Penjelasan                                        | Contoh                                                        |
| ------------------------------ | ------------------------------------------------- | ------------------------------------------------------------- |
| `margin`                       | Jarak di luar border ke elemen lain               | `margin: 20px;`                                               |
| `margin: 0 auto`               | Tengah horizontal                                 | `margin: 0 auto;`                                             |
| `margin-top/right/bottom/left` | Per sisi margin                                   | `margin-top: 10px;`                                           |
| Margin negatif                 | Menarik elemen ke arah tertentu                   | `margin-left: -20px;`                                         |
| Margin collapse                | Margin vertikal bertumpuk, hanya terbesar berlaku | `h1 { margin-bottom: 30px; } p { margin-top: 20px; } //=30px` |

---

## Box Sizing

| Properti                  | Penjelasan                             | Contoh                                                     |
| ------------------------- | -------------------------------------- | ---------------------------------------------------------- |
| `box-sizing: content-box` | Default: width/height hanya CONTENT    | `width: 200px; padding: 20px; border: 2px; // total=244px` |
| `box-sizing: border-box`  | Width/height termasuk PADDING + BORDER | `width: 200px; padding: 20px; border: 2px; // total=200px` |

Reset umum:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

---

## Display & Overflow

| Properti                    | Penjelasan                         | Contoh                   |
| --------------------------- | ---------------------------------- | ------------------------ |
| `display: block`            | Lebar penuh, mulai dari baris baru | `display: block;`        |
| `display: inline`           | Hanya selebar konten               | `display: inline;`       |
| `display: inline-block`     | Inline tapi bisa diberi ukuran     | `display: inline-block;` |
| `overflow`                  | Menangani konten yang meluap       | `overflow: hidden;`      |
| `overflow-x` / `overflow-y` | Per sumbu overflow                 | `overflow-x: auto;`      |

---

## Contoh Lengkap

```css
.card {
  width: 300px;
  box-sizing: border-box;
  padding: 24px;
  border: 1px solid #e0e0e0;
  border-radius: 12px;
  margin: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}
/* Total lebar card = 300px (border-box) */
```
