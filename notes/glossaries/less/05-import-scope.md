# Import & Scope

## Import

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `@import "file"` | Import file Less lain | `@import "variables"` |
| `@import (reference)` | Import untuk mixin/extend saja (tidak output) | `@import (reference) "bootstrap"` |
| `@import (inline)` | Copy file as-is (tidak diproses) | `@import (inline) "legacy.css"` |
| `@import (less)` | Paksa treat sebagai Less meski ext .css | `@import (less) "style.css"` |
| `@import (css)` | Paksa treat sebagai CSS (keluar `@import` CSS) | `@import (css) "style.less"` |
| `@import (multiple)` | Izinkan import file yang sama berkali-kali | `@import (multiple) "theme"` |
| `@import (optional)` | Tidak error jika file tidak ditemukan | `@import (optional) "ads.css"` |

```less
// Import biasa — file di-inline ke output
@import "variables";       // variables.less
@import "mixins/mixins";   // mixins/mixins.less
@import "https://fonts.googleapis.com/css?family=Open+Sans"; // URL

// Import (reference) — hanya mixin/extend, tidak nambah CSS
@import (reference) "bootstrap/grid";
.row {
  .make-row(); // mixin dari bootstrap, output di sini
}

// Import (inline) — copy mentah tanpa diproses
@import (inline) "legacy-styles.css";

// Import (css) — tetap jadi @import CSS, tidak di-inline
@import (css) "print.less";
// Output: @import "print.less";

// Import (less) — paksa treat sebagai Less
@import (less) "bootstrap.css";
// Bootstrap CSS akan diproses sebagai Less

// Import optional — diam saja jika file tidak ada
@import (optional) "ads.css"; // file tidak ada → tidak error
```

---

## Scope

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Global scope | Variable di luar block | `@color: red;` |
| Local scope | Variable di dalam block | `.box { @color: blue; }` |
| Lazy loading | Semua variable diproses dari call terakhir | `@a: 1; @a: 2;` → `2` |
| Variable hoisting | Variable "naik" ke atas scope | — |

```less
// Global vs Local scope
@global-color: navy;

.card {
  @card-color: #333; // local
  color: @card-color; // #333
}

// .other { color: @card-color; } // ERROR! tidak dikenal

// Scope juga berlaku untuk nested rules
.container {
  @padding-large: 30px;
  padding: @padding-large;

  .inner {
    @padding-small: 10px;
    padding: @padding-small;
    // padding: @padding-large; // bisa — scope parent
  }

  // padding: @padding-small; // ERROR — scope berbeda
}
```

### Lazy Loading (less vs sass)
```less
// Less: LAZY LOADING — deklarasi terakhir menang
@size: 20px;

.box {
  width: @size; // 30px (lazy — pakai nilai terakhir)
}

@size: 30px;

// Output: .box { width: 30px; }

// Dibanding dengan Sass:
// $size: 20px;
// .box { width: $size; } // 20px (Sass pake nilai saat itu)
// $size: 30px;
```

### Import & Scope
Variable dari file yang di-import tersedia di scope file utama.
```less
// variables.less
@primary: #3498db;
@secondary: #2ecc71;
$base-font: 16px;

// style.less
@import "variables";

.header {
  color: @primary;          // dari variables.less
  font-size: @base-font;    // dari variables.less
}
```

### Mixin dengan Guard (Pattern)
```less
// mixin dengan kondisi scope
.text-color(@bg) when (lightness(@bg) >= 50%) {
  color: #333; // background terang → teks gelap
}

.text-color(@bg) when (lightness(@bg) < 50%) {
  color: white; // background gelap → teks terang
}

.card-light {
  background: #f0f0f0;
  .text-color(#f0f0f0); // color: #333
}

.card-dark {
  background: #333;
  .text-color(#333); // color: white
}
```
