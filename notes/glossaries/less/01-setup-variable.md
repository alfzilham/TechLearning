# Setup & Variable

## Setup

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `npm install -g less` | Install Less compiler global | `npm i -g less` |
| `lessc` | Compile .less ke .css | `lessc style.less style.css` |
| `--watch` | Otomatis compile saat file berubah | `lessc --watch style.less style.css` |
| `--clean-css` | Minify output CSS | `lessc --clean-css style.less style.min.css` |
| `--source-map` | Generate source map | `lessc --source-map style.less style.css` |
| `less.render()` | Compile via Node.js API | `less.render(".a { color: red }", callback)` |

```less
// Terminal
npm install -g less
lessc src/style.less dist/style.css
lessc --watch src/style.less dist/style.css
lessc --clean-css src/style.less dist/style.min.css

// package.json
{
  "scripts": {
    "compile": "lessc src/style.less dist/style.css",
    "watch": "lessc --watch src/style.less dist/style.css",
    "build": "lessc --clean-css src/style.less dist/style.min.css"
  }
}

// Node.js API
const less = require('less');
less.render('.class { color: red; }', (err, output) => {
  console.log(output.css);
});
```

---

## Variable

### `@variable`
Variabel untuk menyimpan nilai (warna, ukuran, font, dll).
```less
@primary-color: #3498db;
@font-size: 16px;
@spacing: 20px;

.header {
  color: @primary-color;
  font-size: @font-size;
  padding: @spacing;
}
```

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `@nama` | Mendeklarasikan variable | `@warna: red;` |
| `@{nama}` | Interpolation — pakai variable di selector/properti | `.@{name} { }` |
| Lazy loading | Variable diproses dari akhir (tidak masalah urutan) | `@a: 1; @a: 2;` → hasil 2 |
| Variable scoping | Variable lokal di dalam block | `.box { @color: red; }` |

### Interpolation `@{var}`
Variable bisa dipakai di selector, properti, URL, import.
```less
@prefix: col;
@url: "../images/";
@side: left;

.@{prefix}-4 { width: 33%; }          // .col-4
.@{prefix}-6 { width: 50%; }          // .col-6

background-url: "@{url}bg.jpg";       // "../images/bg.jpg"
border-@{side}: 1px solid #ccc;       // border-left
```

### Lazy Loading
Variable di Less tidak harus didefinisikan sebelum dipakai (beda dengan Sass).
```less
// Lazy loading — urutan deklarasi tidak masalah
.section {
  color: @theme; // @theme belum didefinisikan di sini
}

@theme: blue;    // Tapi nanti akan dipakai

// Hasil: .section { color: blue; }
```

### Variable Scoping
```less
@color: blue; // global

.box {
  @color: red; // lokal — override global di scope ini
  color: @color; // red
}

.other {
  color: @color; // blue (global)
}
```

### Variable List (Multiple values)
```less
@sizes: 10px 20px 30px;
@colors: red, green, blue;

.box {
  padding: @sizes;      // padding: 10px 20px 30px
  color: extract(@colors, 1); // red
}
```
