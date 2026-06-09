# 01 Setup & Variable

## Setup

| Konsep              | Penjelasan                                      | Contoh                                          |
| ------------------- | ----------------------------------------------- | ----------------------------------------------- |
| Basic compile       | Compile SCSS ke CSS sekali                      | `sass input.scss output.css`                    |
| Watch mode          | Pantau perubahan & compile otomatis             | `sass --watch input.scss:output.css`            |
| Watch folder        | Pantau seluruh folder                           | `sass --watch scss/:css/`                       |
| Compressed          | Minified output untuk production                | `sass --style compressed input.scss output.css` |
| Expanded            | Readable output untuk development               | `sass --style expanded input.scss output.css`   |
| package.json script | Simpan command di `"scripts"`                   | `"sass": "sass --watch scss/:css/"`             |
| node-sass           | LibSass-based — deprecated, pindah ke dart-sass | `npm i node-sass` (tidak disarankan)            |
| dart-sass           | Official implementation — recommended           | `npm i sass` (otomatis dart-sass)               |

```scss
// package.json
{
  "scripts": {
    "sass": "sass --watch scss/:css/",
    "sass:build": "sass --style compressed scss/:css/"
  }
}
```

## Variable

| Konsep            | Penjelasan                                           | Contoh                                              |
| ----------------- | ---------------------------------------------------- | --------------------------------------------------- |
| Declare           | Definisi variable dengan `$`                         | `$color-primary: #3498db;`                          |
| Naming convention | Gunakan dasbor untuk readability                     | `$font-size-lg`, `$spacing-unit`                    |
| Global scope      | Variable di luar block — bisa diakses di mana saja   | `$color: red;` di root file                         |
| Local scope       | Variable di dalam `{ }` — hanya berlaku di block itu | `@mixin foo { $local: 10px; }`                      |
| `!default`        | Set default, tidak override jika sudah ada nilai     | `$color: blue !default;` — pattern library override |
| `!global`         | Paksa variable local menjadi global                  | `$var: 10px !global;`                               |
| String            | Tipe data teks                                       | `"Helvetica"`, `'Arial'`, `sans-serif`              |
| Number            | Tipe data angka (bisa dengan/satuan)                 | `16px`, `1.5`, `100%`, `2em`                        |
| Color             | Tipe data warna                                      | `#fff`, `red`, `rgba(0,0,0,.5)`, `hsl(0,100%,50%)`  |
| List              | Kumpulan nilai dipisah spasi/koma                    | `10px 20px 30px`, `'Roboto', sans-serif`            |
| Map               | Key-value pairs                                      | `$breakpoints: (sm: 576px, md: 768px);`             |
| Interpolasi       | Gunakan variable dalam selector/property             | `#{$prefix}-wrapper`                                |

```scss
// Variable declarations
$color-primary: #3498db;
$color-secondary: #2ecc71;
$font-stack: "Inter", sans-serif;
$spacing-unit: 8px;
$breakpoints: (
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px,
);

// !default pattern (untuk library / reusable module)
$border-radius: 4px !default;
$enable-shadows: true !default;

// Scoping
$global-var: 16px;

.container {
  $local-var: 10px; // local scope
  font-size: $local-var;
}

// Interpolation
$prefix: "app";
.#{$prefix}-header {
}

// Data types
$string: "Hello";
$number: 24px;
$color: #333;
$list: 10px 20px 30px;
$map: (
  header: 60px,
  footer: 40px,
);
```
