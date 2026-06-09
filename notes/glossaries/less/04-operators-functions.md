# 04 Operators & Functions

## Operators

| Konsep | Penjelasan | Contoh |
|--------|------------|--------|
| Aritmatika angka | Operasi `+`, `-`, `*`, `/` pada angka dan dimensi | `@w: 100px + 50px;` |
| Aritmatika warna | Operasi aritmatika pada nilai hex/rgba | `@color: #333 + #111;` |
| Parenthesized | Mengelompokkan ekspresi dengan tanda kurung | `@w: (100px + 50px) * 2;` |
| Unit otomatis | Hasil operasi menggunakan unit operand pertama | `10px * 2 = 20px` |

```less
// Aritmatika angka
@base: 100px;
@padding: @base / 10;
@width: @base + (@padding * 2);

.container {
  width: @width;               // 120px
  padding: @padding;           // 10px
  margin: (@base - 20px) / 2;  // 40px
}

// Operasi dengan unit berbeda
@a: 10px + 5;     // 15px
@b: 20px - 5px;   // 15px
@c: 10px * 3;     // 30px
@d: 30px / 2;     // 15px

// Color arithmetic
@base-color: #334455;
@lighter: @base-color + #111111;  // #445566
@darker: @base-color - #111111;   // #223344

// Parenthesized expressions
@area: (10px + 20px) * (2 + 1);  // 90px
@calc: (100% - 50px) / 2;        // (100% - 50px) / 2 -- untuk CSS calc

// Menghasilkan CSS calc()
.element {
  width: calc(100% - 40px);  // string biasa, bukan operasi Less
}
```

## Color Functions

| Konsep | Penjelasan | Contoh |
|--------|------------|--------|
| `darken()` | Menggelapkan warna dengan persentase | `darken(@color, 10%)` |
| `lighten()` | Menerangkan warna dengan persentase | `lighten(@color, 10%)` |
| `saturate()` | Meningkatkan saturasi | `saturate(@color, 20%)` |
| `desaturate()` | Menurunkan saturasi | `desaturate(@color, 20%)` |
| `fadein()` | Menambah opacity (mengurangi transparansi) | `fadein(@color, 10%)` |
| `fadeout()` | Mengurangi opacity (menambah transparansi) | `fadeout(@color, 10%)` |
| `fade()` | Mengatur opacity absolut | `fade(@color, 50%)` |
| `spin()` | Memutar hue color wheel | `spin(@color, 180deg)` |
| `mix()` | Mencampur dua warna | `mix(@c1, @c2, 50%)` |
| `tint()` | Mencampur warna dengan putih | `tint(@color, 30%)` |
| `shade()` | Mencampur warna dengan hitam | `shade(@color, 30%)` |
| `greyscale()` | Menghilangkan saturasi (100% desaturate) | `greyscale(@color)` |
| `contrast()` | Memilih warna kontras (hitam/putih) untuk teks | `contrast(@bg)` |

```less
@primary: #007bff;
@bg: #f5f5f5;
@text: #333;

// Manipulasi warna dasar
.button {
  background: @primary;
  border-color: darken(@primary, 10%);
  color: lighten(@primary, 60%);

  &:hover {
    background: darken(@primary, 5%);
  }
}

// Saturasi & opacity
.alert {
  background: saturate(@primary, 30%);
  &.muted {
    background: desaturate(@primary, 50%);
  }
  &.transparent {
    background: fadeout(@primary, 30%);  // 70% opacity
  }
}

// Absolute opacity
.overlay {
  background: fade(#000, 50%);           // rgba(0,0,0,.5)
}

// Spin — menghasilkan palet dari satu warna
@base: #3498db;

.card-primary  { background: @base; }
.card-secondary { background: spin(@base, 60deg); }
.card-accent    { background: spin(@base, 180deg); }
.card-complement { background: spin(@base, 210deg); }

// Mix — mencampur dua warna
@red: #ff0000;
@blue: #0000ff;
@purple: mix(@red, @blue, 50%);  // #800080

// Tint & Shade
.card {
  background: @primary;
  color: tint(@primary, 80%);    // campur dengan putih
  border: 1px solid shade(@primary, 20%);  // campur dengan hitam
}

// Greyscale
.palette {
  color: @primary;
  &.grey {
    color: greyscale(@primary);
  }
}

// Contrast untuk aksesibilitas teks
.card {
  background: @primary;
  color: contrast(@primary);  // output: white, karena bg biru gelap
}
.card-light {
  background: @bg;
  color: contrast(@bg);       // output: black, karena bg terang
}
```

## Math Functions

| Konsep | Penjelasan | Contoh |
|--------|------------|--------|
| `ceil()` | Pembulatan ke atas | `ceil(4.2)` → `5` |
| `floor()` | Pembulatan ke bawah | `floor(4.8)` → `4` |
| `round()` | Pembulatan terdekat | `round(4.5)` → `5` |
| `percentage()` | Konversi ke persentase | `percentage(0.25)` → `25%` |
| `abs()` | Nilai absolut | `abs(-10px)` → `10px` |
| `min()` | Nilai terkecil | `min(10px, 20px)` → `10px` |
| `max()` | Nilai terbesar | `max(10px, 20px)` → `20px` |
| `sqrt()` | Akar kuadrat | `sqrt(16)` → `4` |
| `pow()` | Pangkat | `pow(2, 3)` → `8` |
| `mod()` | Sisa bagi (modulus) | `mod(10, 3)` → `1` |

```less
// Pembulatan
.box {
  width: ceil(100.4px);   // 101px
  height: floor(100.8px);  // 100px
  padding: round(10.5px);  // 11px
}

// Persentase
.container {
  width: percentage(0.75);     // 75%
  @ratio: 3 / 4;
  height: percentage(@ratio);  // 75%
}

// Nilai absolut
.element {
  margin: abs(-20px);  // 20px
}

// Min / Max
.sidebar {
  width: min(300px, 50%);   // 300px (tergantung konteks)
}
.content {
  width: max(600px, 80%);
}

// Sqrt, Pow, Mod
@columns: 12;
.item {
  // Contoh penggunaan kombinasi
  width: percentage(1 / @columns);  // 8.33333333%

  // sqrt
  @area: 100px;
  @side: sqrt(100px * 100px);  // 100px

  // pow
  @scale: pow(1.5, 2);  // 2.25

  // mod — grid alternatif
  // mod(5, 2) = 1, mod(6, 2) = 0
}
```
