# 03 Extend & Merge

## Extend

| Konsep | Penjelasan | Contoh |
|--------|------------|--------|
| `&:extend(.class)` | Mewarisi semua properti selector lain tanpa duplikasi | `.b { &:extend(.a); }` |
| `&:extend(.class all)` | Juga memperluas ke instance nested dari selector target | `.b { &:extend(.a all); }` |
| Extend multiple | Memperluas beberapa selector sekaligus | `&:extend(.a); &:extend(.b);` atau `&:extend(.a, .b)` |
| Extend nested | Memperluas selector di dalam nested rule | `.inner { &:extend(.outer .desc); }` |
| Extend vs mixin | Extend menggabungkan selector (DRY CSS), mixin menduplikasi properti | Lihat perbandingan di bawah |

### Extend vs Mixin

| Aspek | Extend | Mixin |
|-------|--------|-------|
| Output CSS | Selector digabung (comma) — lebih ringkas | Properti disalin ke setiap selector |
| Ukuran file | Lebih kecil | Lebih besar (duplikasi) |
| Spesifisitas | Mewarisi spesifisitas selector target | Spesifisitas sesuai posisi pemanggilan |
| Parameter | Tidak bisa | Bisa parametric |
| Kondisional | Tidak bisa | Bisa dengan guards |

```less
// EXTEND basic
.a {
  color: red;
  padding: 10px;
}
.b {
  &:extend(.a);
  border: 1px solid;
}
// Output:
// .a, .b { color: red; padding: 10px; }
// .b { border: 1px solid; }

// EXTEND all — juga memperluas instance di dalam pseudo-class
.a {
  color: red;
  &:hover {
    color: blue;
  }
}
.b {
  &:extend(.a all);
}
// Output:
// .a, .b { color: red; }
// .a:hover, .b:hover { color: blue; }

// Tanpa 'all':
.c {
  &:extend(.a);
}
// Output:
// .a, .c { color: red; }
// .a:hover { color: blue; }   // tidak mengextend :hover

// EXTEND multiple
.error {
  color: red;
}
.serious {
  font-weight: bold;
}
.danger {
  &:extend(.error);
  &:extend(.serious);
  background: #fcc;
}
// Atau: &:extend(.error, .serious);

// EXTEND nested selector
.outer {
  .desc {
    color: green;
  }
}
.inner {
  &:extend(.outer .desc);
}
// Output: .outer .desc, .inner { color: green; }

// Perbandingan dengan Mixin
// Mixin — duplikasi properti
.bordered-mixin {
  border: 1px solid #ddd;
}
.card-a { .bordered-mixin; }
.card-b { .bordered-mixin; }
// Output: .card-a { border: 1px solid #ddd; }
//         .card-b { border: 1px solid #ddd; }

// Extend — selector grouping
.bordered-extend {
  border: 1px solid #ddd;
}
.card-x { &:extend(.bordered-extend); }
.card-y { &:extend(.bordered-extend); }
// Output: .bordered-extend, .card-x, .card-y { border: 1px solid #ddd; }
```

## Merge

| Konsep | Penjelasan | Contoh |
|--------|------------|--------|
| Comma merge `+` | Menggabungkan nilai dengan koma | `.a+() { background: url(a.png); }` |
| Space merge `+_` | Menggabungkan nilai dengan spasi | `.a+_() { transform: scale(1); }` |

```less
// Comma merge (+)
.mixin-bg() {
  background+:
    url(bg1.png) no-repeat top left;
}
.card {
  .mixin-bg();
  background+:
    url(bg2.png) center center;
}
// Output: .card {
//   background: url(bg1.png) no-repeat top left,
//               url(bg2.png) center center;
// }

// Space merge (+_)
.mixin-shadow() {
  box-shadow+_: 0 2px 4px rgba(0,0,0,.1);
}
.card {
  .mixin-shadow();
  box-shadow+_: 0 0 0 1px #eee;
}
// Output: .card {
//   box-shadow: 0 2px 4px rgba(0,0,0,.1) 0 0 0 1px #eee;
// }

// Merge dengan transform
.mixin-scale() {
  transform+_: scale(1.5);
}
.element {
  .mixin-scale();
  transform+_: rotate(45deg);
}
// Output: .element {
//   transform: scale(1.5) rotate(45deg);
// }

// Merge dengan background (comma)
.mixin-gradient() {
  background+:
    linear-gradient(red, orange);
}
.banner {
  .mixin-gradient();
  background+:
    url(pattern.png) repeat;
}
// Output: .banner {
//   background: linear-gradient(red, orange),
//               url(pattern.png) repeat;
// }
```
