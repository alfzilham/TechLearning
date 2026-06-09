# 05 Color Modules

Gunakan `@use 'sass:color';` untuk semua fungsi manipulasi warna.

| Fungsi                                  | Penjelasan                         | Contoh                                           |
| --------------------------------------- | ---------------------------------- | ------------------------------------------------ |
| `color.adjust-hue($color, $deg)`        | Putar hue color wheel sejauh n°    | `adjust-hue(#3498db, 180deg)` → complementary    |
| `color.saturate($color, $amt)`          | Tingkatkan saturasi                | `saturate(#ccc, 30%)`                            |
| `color.desaturate($color, $amt)`        | Kurangi saturasi — mendekati gray  | `desaturate(#e74c3c, 20%)`                       |
| `color.lighten($color, $amt)`           | Terangkan warna                    | `lighten(#333, 30%)` → `#8c8c8c`                 |
| `color.darken($color, $amt)`            | Gelapkan warna                     | `darken(#3498db, 20%)`                           |
| `color.opacify()` / `fade-in()`         | Tambah opacity (kurang transparan) | `opacify(rgba(0,0,0,.3), .5)` → `.8`             |
| `color.transparentize()` / `fade-out()` | Kurangi opacity (lebih transparan) | `transparentize(#333, .5)` → `rgba(51,51,51,.5)` |
| `color.mix($c1, $c2, $weight)`          | Campur 2 warna, weight% untuk c1   | `mix(#fff, #000, 50%)` → `#808080`               |
| `color.complement($color)`              | Warna complementary (hue + 180°)   | `complement(#3498db)` → `#db7734`                |
| `color.grayscale($color)`               | Buat grayscale (desaturate 100%)   | `grayscale(#e74c3c)` → `#808080`                 |
| `color.invert($color)`                  | Balik warna (255 - each channel)   | `invert(#fff)` → `#000`                          |

```scss
@use "sass:color";

// Color palette generator
$brand: #3498db;

$palette: (
  "base": $brand,
  "light": color.lighten($brand, 25%),
  "dark": color.darken($brand, 20%),
  "complement": color.complement($brand),
  "desaturated": color.desaturate($brand, 40%),
  "grayscale": color.grayscale($brand),
  "invert": color.invert($brand),
);

// Button theme generator
@mixin btn-theme($bg, $darken-amt: 10%) {
  background: $bg;
  color: if(color.lightness($bg) > 50%, #333, #fff);

  &:hover {
    background: color.darken($bg, $darken-amt);
  }

  &:active {
    background: color.darken($bg, $darken-amt + 5%);
  }
}

.btn-primary {
  @include btn-theme($brand);
}

// UI element tinting
$surface: #f8f9fa;
$border-default: color.darken($surface, 15%);

.card {
  background: $surface;
  border: 1px solid $border-default;
  box-shadow: 0 2px 8px color.transparentize(#000, 0.85);
}

// Mix untuk gradient
$gradient-start: #667eea;
$gradient-end: #764ba2;

.hero {
  background: linear-gradient(
    135deg,
    $gradient-start,
    color.mix($gradient-start, $gradient-end, 50%),
    $gradient-end
  );
}

// State colors
$success: #27ae60;

.success-badge {
  background: color.lighten($success, 40%);
  color: color.darken($success, 10%);
  border: 1px solid $success;
}

// Opacity utilities
.overlay {
  background: color.transparentize(#000, 0.5); // rgba(0,0,0,.5)
}

.fade-in {
  background: color.opacify(rgba(0, 0, 0, 0.3), 0.4); // rgba(0,0,0,.7)
}
```
