# Operators & Functions

## Operators

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `+` | Penjumlahan | `10px + 5px` → `15px` |
| `-` | Pengurangan | `20px - 8px` → `12px` |
| `*` | Perkalian | `10px * 3` → `30px` |
| `/` | Pembagian | `30px / 2` → `15px` |
| `%` | Modulus | `10 % 3` → `1` |
| `()` | Parentheses untuk prioritas | `(10px + 5px) * 2` → `30px` |
| Color ops | Operasi pada warna | `#333 + #111` → `#444` |

```less
// Arithmetic
@base: 16px;
@spacing: 10px;

.box {
  width: 100% - 40px;           // calc(100% - 40px)
  padding: @spacing * 2;        // padding: 20px
  font-size: @base + 4px;       // font-size: 20px
  margin: (@spacing * 3) - 5px; // margin: 25px
}

// Color arithmetic
@primary: #336699;
@darker: @primary - #111111;    // #225588
@lighter: @primary + #333333;   // #6699cc

.text {
  color: @primary;
  background: @lighter;
}
```

---

## Color Functions

| Fungsi | Penjelasan | Contoh |
|--------|-----------|--------|
| `darken(@color, 10%)` | Gelapkan warna | `darken(red, 10%)` |
| `lighten(@color, 10%)` | Terangkan warna | `lighten(blue, 10%)` |
| `saturate(@color, 20%)` | Tambah saturasi | `saturate(gray, 50%)` |
| `desaturate(@color, 20%)` | Kurangi saturasi | `desaturate(red, 20%)` |
| `fadein(@color, 10%)` | Tambah opacity (kurang transparan) | `fadein(rgba(0,0,0,0.5), 10%)` |
| `fadeout(@color, 10%)` | Kurangi opacity (lebih transparan) | `fadeout(rgba(0,0,0,0.5), 10%)` |
| `fade(@color, 50%)` | Set opacity | `fade(red, 50%)` |
| `spin(@color, 10deg)` | Putar hue | `spin(red, 180deg)` → cyan |
| `mix(@a, @b, 50%)` | Campur 2 warna | `mix(red, blue)` → purple |
| `tint(@color, 50%)` | Campur dengan putih | `tint(red, 50%)` → pink |
| `shade(@color, 50%)` | Campur dengan hitam | `shade(red, 50%)` → dark red |
| `greyscale(@color)` | Buat grayscale (100% desaturate) | `greyscale(red)` → gray |
| `contrast(@color)` | Pilih hitam/putih kontras | `contrast(white)` → black |

```less
@primary: #3498db;
@success: #2ecc71;
@danger: #e74c3c;

.btn {
  &-primary {
    background: @primary;
    &:hover { background: darken(@primary, 10%); }
    &:active { background: darken(@primary, 15%); }
  }

  &-success {
    background: @success;
    &:hover { background: darken(@success, 10%); }
  }

  &-danger {
    background: @danger;
    &:hover { background: darken(@danger, 10%); }
  }

  &-outline {
    background: transparent;
    border: 2px solid @primary;
    color: @primary;
    &:hover {
      background: @primary;
      color: fade(@primary, 0%); // jadi putih
    }
  }
}

// System warna
@bg: #f5f5f5;
@text: contrast(@bg); // hitam (#000) — kontras otomatis

body {
  background: @bg;
  color: @text;
}

// Mix
.alert {
  &-info { background: mix(blue, white, 20%); color: darken(blue, 20%); }
  &-warn { background: mix(orange, white, 20%); color: darken(orange, 20%); }
}
```

---

## Math Functions

| Fungsi | Penjelasan | Contoh |
|--------|-----------|--------|
| `ceil(3.14)` | Bulatkan ke atas | `ceil(3.14)` → `4` |
| `floor(3.14)` | Bulatkan ke bawah | `floor(3.14)` → `3` |
| `round(3.14)` | Bulatkan terdekat | `round(3.14)` → `3` |
| `percentage(0.15)` | Ubah ke persen | `percentage(0.15)` → `15%` |
| `abs(-10px)` | Nilai absolut | `abs(-10px)` → `10px` |
| `min(a, b, c)` | Nilai terkecil | `min(10px, 20px, 5px)` → `5px` |
| `max(a, b, c)` | Nilai terbesar | `max(10px, 20px, 5px)` → `20px` |
| `sqrt(25)` | Akar kuadrat | `sqrt(25)` → `5` |
| `pow(2, 3)` | Pangkat | `pow(2, 3)` → `8` |
| `mod(10, 3)` | Sisa bagi | `mod(10, 3)` → `1` |

```less
@columns: 12;
@gutter: 16px;
@container: 1200px;

.col {
  width: (100% / @columns); // 8.333%
}

// min/max untuk responsive
.sidebar {
  width: min(300px, 25%);   // minimal dari 300px atau 25%
}
.content {
  width: max(600px, 75%);
}

// ceil/floor untuk grid
.span-5 {
  width: percentage(ceil(5 / @columns * 100) / 100);
  // percentage(ceil(0.4167)) = percentage(1) = 100%
  // Oops — pakai floor:
}
.span-5 {
  width: percentage(floor(5 / @columns * 100) / 100);
  // percentage(0.41) = 41%
}
```
