# 01 Setup & Variable

## Setup

| Konsep | Penjelasan | Contoh |
|--------|------------|--------|
| Instalasi global | Install Less compiler via npm secara global | `npm install -g less` |
| Kompilasi file | Mengubah `.less` menjadi `.css` dengan CLI | `lessc input.less output.css` |
| Watch mode | Otomatis kompilasi setiap perubahan file | `lessc --watch input.less output.css` |
| Minify | Mengompresi output CSS dengan plugin clean-css | `lessc --clean-css input.less output.css` |
| Node.js API | Kompilasi programatik via `less.render()` | `less.render(code, { paths }, callback)` |
| Package script | Menyimpan perintah Less di `package.json` | `"build:css": "lessc src/style.less dist/style.css"` |

```less
// CLI
npm install -g less
lessc style.less style.css
lessc --watch style.less style.css
lessc --clean-css style.less style.min.css

// Node.js usage
const less = require('less');
less.render('.class { width: 1 + 1 }', {
  paths: ['.', './src'],
  filename: 'style.less'
}, (err, output) => {
  console.log(output.css);
});

// package.json
// "scripts": {
//   "build:css": "lessc src/style.less dist/style.css",
//   "watch:css": "lessc --watch src/style.less dist/style.css",
//   "min:css": "lessc --clean-css src/style.less dist/style.min.css"
// }
```

## Variable

| Konsep | Penjelasan | Contoh |
|--------|------------|--------|
| Deklarasi variable | Mendefinisikan nilai reusable dengan `@` | `@primary: #007bff;` |
| Value interpolation | Menyisipkan variable ke selector/properti/URL | `@{selector} { @{prop}: value; }` |
| Lazy loading | Variable tidak perlu dideklarasikan sebelum digunakan | `@var: 10px;` setelah penggunaan tetap diproses |
| Last definition wins | Nilai variable adalah deklarasi terakhir dalam scope | `@var: 1; @var: 2;` → hasilnya `2` |
| Variable dalam string | Interpolasi dalam string path/URL | `background: url("@{base-url}/img.png");` |

```less
// Variable dasar
@primary: #007bff;
@padding: 16px;
@font-stack: 'Helvetica', sans-serif;

body {
  color: @primary;
  padding: @padding;
  font-family: @font-stack;
}

// Interpolation di selector
@prefix: app;
.@{prefix}-header { background: @primary; }
.@{prefix}-footer { color: @primary; }

// Interpolation di properti
@side: margin-top;
.@{side} { @{side}: 10px; }

// Interpolation di URL
@base-url: "../assets";
.logo { background: url("@{base-url}/logo.png"); }

// Lazy loading
@size: 20px;
.box { width: @size; }
@size: 30px;
// Hasil: .box { width: 30px; } — last definition wins

// Variable scoping
@color: red;
.wrapper {
  @color: blue;
  .inner { color: @color; } // blue
}
.outer { color: @color; }   // red
```
