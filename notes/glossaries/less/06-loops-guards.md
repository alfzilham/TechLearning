# Loops & Guards

## Guards — Conditional Mixin

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `when` | Kondisi untuk menjalankan mixin | `.mixin(@a) when (@a > 10) { }` |
| `>, <, >=, =<` | Perbandingan | `when (@width >= 768px)` |
| `=` | Sama dengan | `when (@type = "dark")` |
| `,` (koma) | Logical OR | `when (@a > 10), (@b < 5)` |
| `and` | Logical AND | `when (@a > 10) and (@b < 5)` |
| `not` | Negasi | `when not (@a = 10)` |
| `true` | Nilai truthy | `when (@boolean)` |

```less
// Basic guard
.font-size(@size) when (@size >= 18px) {
  font-size: @size;
  line-height: 1.5;
}

.font-size(@size) when (@size < 18px) {
  font-size: @size;
  line-height: 1.6;
}

.heading { .font-size(24px); }  // line-height: 1.5
.paragraf { .font-size(14px); } // line-height: 1.6

// Guard dengan multiple conditions (OR via koma)
.text-color(@bg) when (lightness(@bg) >= 50%) {
  color: #333;
}

.text-color(@bg) when (lightness(@bg) < 50%) {
  color: #fff;
}

.info { .text-color(#e0e0e0); }  // color: #333
.dark { .text-color(#222); }     // color: #fff

// Guard dengan AND
.padding(@size) when (@size > 0) and (@size < 100) {
  padding: @size * 1px;
}

// Guard dengan true/false
.show(@show) when (@show = true) {
  display: block;
}

.show(@show) when (@show = false) {
  display: none;
}
```

---

## Type-check Functions (untuk Guard)

| Fungsi | Cek apakah nilai berupa... | Contoh |
|--------|---------------------------|--------|
| `iscolor(@val)` | Warna | `iscolor(#fff)` → true |
| `isnumber(@val)` | Angka | `isnumber(16px)` → true |
| `isstring(@val)` | String | `isstring("text")` → true |
| `isurl(@val)` | URL | `isurl(url(...))` → true |
| `ispixel(@val)` | Pixel | `ispixel(16px)` → true |
| `ispercentage(@val)` | Persen | `ispercentage(50%)` → true |
| `isem(@val)` | Em | `isem(2em)` → true |
| `isunit(@val, "px")` | Unit tertentu | `isunit(16px, "px")` → true |

```less
// Type-check untuk validasi
.convert(@value) when (ispixel(@value)) {
  width: @value;
}

.convert(@value) when (ispercentage(@value)) {
  width: @value;
}

.convert(@value) when (isem(@value)) {
  width: @value * 16px;
}

.box { .convert(50%); }  // width: 50%
.card { .convert(20em); } // width: 320px
```

---

## Loops (Recursive Mixin Pattern)

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Recursive mixin | Mixin panggil dirinya sendiri dengan guard | `.loop(@n) when (@n > 0)` |
| Pattern matching | Mixin berbeda berdasarkan nilai parameter | `.loop(@n) when (@n = 0)` untuk stop |

Less **TIDAK** punya `@for` / `@each` seperti Sass. Loop di Less menggunakan **recursive mixin + guard**.

### Basic Loop — Grid Columns
```less
// Stop condition — @n = 0 (tidak jalan)
.generate-columns(@n, @i: 1) when (@i = @n) {
  .col-@{i} {
    width: (@i * 100% / @n);
  }
}

// Recurse — panggil lagi dengan @i + 1
.generate-columns(@n, @i: 1) when (@i < @n) {
  .col-@{i} {
    width: (@i * 100% / @n);
  }
  .generate-columns(@n, (@i + 1));
}

// Generate 4 kolom
.generate-columns(4);

/* Output:
.col-1 { width: 25%; }
.col-2 { width: 50%; }
.col-3 { width: 75%; }
.col-4 { width: 100%; }
*/
```

### Loop — Generate Spacing Utilities
```less
.generate-spacing(@n, @i: 0) when (@i <= @n) {
  .mt-@{i} { margin-top: (@i * 4px); }
  .mb-@{i} { margin-bottom: (@i * 4px); }
  .pt-@{i} { padding-top: (@i * 4px); }
  .pb-@{i} { padding-bottom: (@i * 4px); }

  .generate-spacing(@n, (@i + 1));
}

.generate-spacing(5);

/* Output:
.mt-0 { margin-top: 0px; } .mb-0 { margin-bottom: 0px; } ...
.mt-1 { margin-top: 4px; } ...
.mt-5 { margin-top: 20px; } ...
*/
```

### Loop — Generate Color Variants
```less
// Daftar warna
@colors:
  primary  #3498db,
  success  #2ecc71,
  danger   #e74c3c,
  warning  #f39c12;

.generate-buttons(@list) when (length(@list) > 0) {
  @item: extract(@list, 1);
  @name: extract(@item, 1);
  @color: extract(@item, 2);

  .btn-@{name} {
    background: @color;
    color: white;
    &:hover {
      background: darken(@color, 10%);
    }
  }

  .generate-buttons(extract-loop-rest(@list));
}

// Helper: ambil sisa list setelah index 1
.extract-loop-rest(@list) when (length(@list) > 1) {
  @rest: extract(@list, 2);
}
// Masalah: extract hanya ambil 1 item — perlu pendekatan berbeda

// Pendekatan praktis — generate satu-satu
.generate-button(@name, @color) {
  .btn-@{name} {
    background: @color;
    color: white;
    &:hover { background: darken(@color, 10%); }
  }
}

.generate-button(primary, #3498db);
.generate-button(success, #2ecc71);
.generate-button(danger, #e74c3c);
```

### Loop — Responsive Breakpoints
```less
@breakpoints:
  sm 576px,
  md 768px,
  lg 992px,
  xl 1200px;

.make-responsive(@list, @i: 1) when (@i <= length(@list)) {
  @item: extract(@list, @i);
  @name: extract(@item, 1);
  @width: extract(@item, 2);

  .d-@{name}-none { display: none; }
  .d-@{name}-block { display: block; }
  .d-@{name}-flex { display: flex; }

  @media (min-width: @width) {
    .d-@{name}-none { display: none !important; }
    .d-@{name}-block { display: block !important; }
    .d-@{name}-flex { display: flex !important; }
  }

  .make-responsive(@list, (@i + 1));
}

// Panggil
.make-responsive(@breakpoints);
```

### Pattern Matching + Loop
Combined guard dan recursive untuk menghasilkan CSS yang bervariasi.
```less
// Mixin dengan multiple guard patterns
.spacing(@n, @type) when (@type = margin) and (@n > 0) {
  .m-@{n} { margin: (@n * 4px); }
  .mx-@{n} { margin-left: (@n * 4px); margin-right: (@n * 4px); }
  .my-@{n} { margin-top: (@n * 4px); margin-bottom: (@n * 4px); }
  .spacing(@n - 1, @type);
}

.spacing(@n, @type) when (@type = padding) and (@n > 0) {
  .p-@{n} { padding: (@n * 4px); }
  .px-@{n} { padding-left: (@n * 4px); padding-right: (@n * 4px); }
  .py-@{n} { padding-top: (@n * 4px); padding-bottom: (@n * 4px); }
  .spacing(@n - 1, @type);
}

// Stop condition
.spacing(@n, @type) when (@n = 0) {
  .m-0 { margin: 0; }
  .p-0 { padding: 0; }
}

// Generate spacing utilities 0-4
.spacing(4, margin);
.spacing(4, padding);
```
