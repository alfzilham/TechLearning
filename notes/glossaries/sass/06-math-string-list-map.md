# 06 Math, String, List & Map Modules

## Math (`sass:math`)

| Fungsi                | Penjelasan             | Contoh                     |
| --------------------- | ---------------------- | -------------------------- |
| `math.ceil($n)`       | Bulatkan ke atas       | `ceil(1.1)` → `2`          |
| `math.floor($n)`      | Bulatkan ke bawah      | `floor(1.9)` → `1`         |
| `math.round($n)`      | Bulatkan terdekat      | `round(1.5)` → `2`         |
| `math.abs($n)`        | Nilai absolut          | `abs(-10)` → `10`          |
| `math.min($a, $b...)` | Nilai terkecil         | `min(1, 3, 2)` → `1`       |
| `math.max($a, $b...)` | Nilai terbesar         | `max(1, 3, 2)` → `3`       |
| `math.random()`       | Random 0–1             | `random()` → `0.472`       |
| `math.random($n)`     | Random 1–$n            | `random(100)` → `42`       |
| `math.percentage($n)` | Ubah desimal ke persen | `percentage(0.75)` → `75%` |
| `math.div($a, $b)`    | Pembagian (ganti `/`)  | `div(16, 4)` → `4`         |
| `math.unit($n)`       | Dapatkan satuan        | `unit(16px)` → `"px"`      |

## String (`sass:string`)

| Fungsi                               | Penjelasan                 | Contoh                                   |
| ------------------------------------ | -------------------------- | ---------------------------------------- |
| `string.unquote($s)`                 | Lepas tanda kutip          | `unquote("hello")` → `hello`             |
| `string.quote($s)`                   | Tambah tanda kutip         | `quote(hello)` → `"hello"`               |
| `string.to-upper-case($s)`           | Huruf besar semua          | `to-upper-case("sass")` → `"SASS"`       |
| `string.to-lower-case($s)`           | Huruf kecil semua          | `to-lower-case("SASS")` → `"sass"`       |
| `string.length($s)`                  | Panjang string             | `length("hello")` → `5`                  |
| `string.str-index($s, $sub)`         | Posisi substring (1-based) | `str-index("hello", "el")` → `2`         |
| `string.str-insert($s, $insert, $i)` | Sisipkan di posisi         | `str-insert("hllo", "e", 2)` → `"hello"` |
| `string.str-slice($s, $start, $end)` | Potong string              | `str-slice("hello", 2, 4)` → `"ell"`     |

## List (`sass:list`)

| Fungsi                     | Penjelasan                 | Contoh                            |
| -------------------------- | -------------------------- | --------------------------------- |
| `list.nth($list, $n)`      | Ambil item ke-n (1-based)  | `nth(10px 20px 30px, 2)` → `20px` |
| `list.join($a, $b)`        | Gabung 2 list              | `join(1 2, 3 4)` → `1 2 3 4`      |
| `list.append($list, $val)` | Tambah item ke list        | `append(1 2, 3)` → `1 2 3`        |
| `list.index($list, $val)`  | Cari posisi value          | `index(1 2 3, 2)` → `2`           |
| `list.length($list)`       | Hitung jumlah item         | `length(1 2 3)` → `3`             |
| `list.separator($list)`    | Cek separator (space/koma) | `separator(1, 2)` → `comma`       |
| `list.is-bracketed($list)` | Cek bracketed `[ ]`        | `is-bracketed([1 2])` → `true`    |

## Map (`sass:map`)

| Fungsi                    | Penjelasan                   | Contoh                               |
| ------------------------- | ---------------------------- | ------------------------------------ |
| `map.get($map, $key)`     | Ambil value dari key         | `get((a: 1, b: 2), a)` → `1`         |
| `map.merge($a, $b)`       | Gabung 2 map                 | `merge((a:1), (b:2))` → `(a:1, b:2)` |
| `map.keys($map)`          | Dapatkan semua keys (list)   | `keys((a:1, b:2))` → `(a, b)`        |
| `map.values($map)`        | Dapatkan semua values (list) | `values((a:1, b:2))` → `(1, 2)`      |
| `map.has-key($map, $key)` | Cek apakah key ada           | `has-key((a:1), a)` → `true`         |
| `map.remove($map, $key)`  | Hapus key dari map           | `remove((a:1, b:2), a)` → `(b:2)`    |

```scss
@use 'sass:math';
@use 'sass:string';
@use 'sass:list';
@use 'sass:map';

// =============================================
// MATH
// =============================================

// Responsive font-size clamp
@function responsive-font($min, $max) {
  $diff: $max - $min;
  return clamp(#{$min}, calc(#{$min} + #{$diff} * (100vw - 320px) / 880), #{$max});
}

h1 { font-size: responsive-font(24px, 48px); }

// Grid column width
@function col-width($cols, $total: 12, $gap: 30px) {
  $gap-total: math.div(($total - 1) * $gap, $total);
  @return calc(math.percentage(math.div($cols, $total)) - #{$gap-total});
}

.col-4 { width: col-width(4); }

// Random color utility
@function random-color() {
  $r: math.floor(math.random(255));
  $g: math.floor(math.random(255));
  $b: math.floor(math.random(255));
  @return rgb($r, $g, $b);
}

// =============================================
// STRING
// =============================================

// Utility class generator
$prefix: 'btn';

@each $mod in ('primary', 'secondary', 'danger') {
  $class: string.to-lower-case(string.unquote("#{$prefix}-#{$mod}"));
  .#{$class} { }
}

// URL slug
@function slugify($str) {
  $str: string.to-lower-case($str);
  @return string.unquote($str);
}

// =============================================
// LIST
// =============================================

$spacing: 4px 8px 12px 16px 24px;

@for $i from 1 through list.length($spacing) {
  .p-#{$i} {
    padding: list.nth($spacing, $i);
  }
}

$fonts: 'Inter', 'Roboto', sans-serif;

// list.join
$all-fonts: list.join(('Arial'), $fonts);     // ('Arial', 'Inter', 'Roboto', sans-serif)

// list.append
$extended: list.append($spacing, 32px);        // (4px 8px 12px 16px 24px 32px)

// list.index
$pos: list.index($fonts, 'Roboto');            // 2

// =============================================
// MAP
// =============================================

$breakpoints: (
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px
);

// map.get
$md-width: map.get($breakpoints, md);         // 768px

// map.has-key
@mixin respond($bp) {
  @if map.has-key($breakpoints, $bp) {
    @media (min-width: map.get($breakpoints, $bp)) {
      @content;
    }
  }
}

// map.merge — extend config
$spacing-config: (
  tight: 0.25rem,
  base: 1rem,
  loose: 2rem
);

$extended-config: map.merge($spacing-config, (
  xloose: 4rem,
  xxloose: 6rem
));

// map.keys + map.values — generate utility classes
$theme-colors: (
  primary: #3498db,
  success: #2ecc71,
  danger: #e74c3c
);

@each $name in map.keys($theme-colors) {
  $color: map.get($theme-colors, $name);
  .text-#{$name} { color: $color; }
}

// map.remove
$reduced-colors: map.remove($theme-colors, 'danger');
// (primary: #3498db, success: #2ecc71)
```
