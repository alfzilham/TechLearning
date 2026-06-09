# 02 - Colors & Background

## Color Properties

| Properti        | Penjelasan                       | Contoh                            |
| --------------- | -------------------------------- | --------------------------------- |
| `color`         | Warna teks                       | `color: red;`                     |
| `color: #hex`   | Warna dengan hex 6 digit         | `color: #ff0000;`                 |
| `color: #hex8`  | Hex 8 digit (dengan alpha)       | `color: #ff000080;`               |
| `color: rgb()`  | RGB (0-255)                      | `color: rgb(255, 0, 0);`          |
| `color: rgba()` | RGB + Alpha (transparansi)       | `color: rgba(255, 0, 0, 0.5);`    |
| `color: hsl()`  | HSL (Hue, Saturation, Lightness) | `color: hsl(0, 100%, 50%);`       |
| `color: hsla()` | HSL + Alpha                      | `color: hsla(0, 100%, 50%, 0.5);` |

---

## Background Properties

| Properti                 | Penjelasan                                 | Contoh                                                      |
| ------------------------ | ------------------------------------------ | ----------------------------------------------------------- |
| `background-color`       | Warna latar belakang                       | `background-color: lightblue;`                              |
| `background-image`       | Gambar latar belakang                      | `background-image: url("bg.jpg");`                          |
| `background-repeat`      | Mengatur pengulangan gambar                | `background-repeat: no-repeat;`                             |
| `background-size`        | Ukuran gambar latar                        | `background-size: cover;`                                   |
| `background-position`    | Posisi gambar latar                        | `background-position: center;`                              |
| `background-attachment`  | Perilaku scroll gambar latar               | `background-attachment: fixed;`                             |
| `background` (Shorthand) | Semua properti background dalam satu baris | `background: #f0f0f0 url("bg.jpg") no-repeat center/cover;` |

---

## Gradients

| Fungsi              | Penjelasan                           | Contoh                                                       |
| ------------------- | ------------------------------------ | ------------------------------------------------------------ |
| `linear-gradient()` | Gradien linear ke segala arah        | `background: linear-gradient(red, blue);`                    |
| `radial-gradient()` | Gradien melingkar                    | `background: radial-gradient(circle, red, blue);`            |
| `conic-gradient()`  | Gradien melingkar penuh (roda warna) | `background: conic-gradient(red, yellow, green, blue, red);` |

Contoh lengkap:

```css
.grad1 {
  background: linear-gradient(red, blue);
}
.grad2 {
  background: linear-gradient(to right, red, yellow);
}
.grad3 {
  background: linear-gradient(to bottom right, red, blue);
}
.grad4 {
  background: linear-gradient(45deg, red, yellow, green);
}
.grad5 {
  background: linear-gradient(to right, red 0%, yellow 50%, green 100%);
}

.circle {
  background: radial-gradient(circle, red, blue);
}
.ellipse {
  background: radial-gradient(ellipse, yellow, orange, red);
}
.at-center {
  background: radial-gradient(circle at center, white, #333);
}
```

---

## Shadow

| Properti      | Penjelasan                  | Contoh                                      |
| ------------- | --------------------------- | ------------------------------------------- |
| `box-shadow`  | Bayangan di belakang elemen | `box-shadow: 2px 2px 4px rgba(0,0,0,0.2);`  |
| `text-shadow` | Bayangan pada teks          | `text-shadow: 1px 1px 2px rgba(0,0,0,0.3);` |

Contoh lengkap:

```css
.shadow-sm {
  box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}
.shadow-md {
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}
.shadow-lg {
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
}
.inset {
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
}
.multi {
  box-shadow:
    0 2px 4px rgba(0, 0, 0, 0.1),
    0 8px 16px rgba(0, 0, 0, 0.1);
}
.hard {
  box-shadow: 4px 4px 0px #333;
}

.light {
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
}
.neon {
  text-shadow:
    0 0 5px #0ff,
    0 0 10px #0ff,
    0 0 20px #0ff;
}
.outline {
  text-shadow:
    -1px -1px 0 #000,
    1px -1px 0 #000,
    -1px 1px 0 #000,
    1px 1px 0 #000;
}
```

---

## Opacity

| Properti  | Penjelasan                                       | Contoh          |
| --------- | ------------------------------------------------ | --------------- |
| `opacity` | Tingkat transparansi (0 = transparan, 1 = solid) | `opacity: 0.5;` |

Perbedaan `opacity` vs `rgba`:

```css
/* opacity: seluruh elemen jadi transparan (termasuk anaknya) */
.card {
  opacity: 0.5;
}

/* rgba: hanya background yang transparan */
.card {
  background: rgba(0, 0, 0, 0.5);
}
```

---

## Contoh Lengkap

```css
.card {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.4);
  border-radius: 12px;
  padding: 24px;
}

.hero {
  background:
    linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url("bg.jpg") center/cover no-repeat fixed;
  color: white;
  min-height: 400px;
}
```
