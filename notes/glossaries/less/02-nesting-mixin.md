# 02 Nesting & Mixin

## Nesting

| Konsep | Penjelasan | Contoh |
|--------|------------|--------|
| Nested selectors | Menulis selector anak di dalam selector induk | `nav { ul { li { ... } } }` |
| `&` parent selector | Mereferensi selector induk | `&:hover`, `&--modifier` |
| `&` untuk modifier | Membuat class modifier berdasarkan induk | `.card { &--dark { ... } }` → `.card--dark` |
| `@media` nesting | Menempatkan media query di dalam selector | `a { @media (max-w: 600px) { ... } }` |
| Multiple `&` | Menggabungkan parent selector dengan dirinya sendiri | `& + &`, `& > &` |

```less
// Nested selectors dasar
nav {
  background: #333;
  ul {
    margin: 0;
    padding: 0;
    li {
      display: inline-block;
      a {
        color: white;
        text-decoration: none;
      }
    }
  }
}
// Output: nav ul li a { color: white; }

// Parent selector &
.button {
  color: black;

  &:hover {
    color: blue;
  }

  &--primary {
    background: #007bff;
  }

  &-icon {
    margin-right: 4px;
  }

  // Combinator dengan &
  & + & {
    margin-left: 8px;
  }

  & > & {
    border: 2px solid;
  }
}
// Output: .button:hover, .button--primary, .button-icon, .button + .button, .button > .button

// Nesting media query dalam selector
.card {
  width: 800px;

  @media (max-width: 768px) {
    width: 100%;
  }

  @media (max-width: 480px) {
    width: 100%;
    padding: 8px;
  }
}
// Output media query tetap terpisah di output CSS
```

## Mixin

| Konsep | Penjelasan | Contoh |
|--------|------------|--------|
| Mixin sebagai class | Semua class Less bisa dipakai sebagai mixin | `.a { color: red; } .b { .a; }` |
| Mixin tersembunyi | Parentheses agar class tidak muncul di output CSS | `.mixin() { color: red; }` |
| Parametric mixin | Mixin yang menerima parameter | `.mixin(@color) { color: @color; }` |
| Default arguments | Parameter dengan nilai bawaan | `.mixin(@p: 10px) { padding: @p; }` |
| `@arguments` variable | Mengakses seluruh argumen yang diberikan | `.mixin(@a, @b) { @arguments; }` |
| Multiple parameters | Mixin dengan beberapa parameter | `.mixin(@x; @y; @z) { ... }` |
| Variable args | Menangkap sisa argumen dengan `...` | `.mixin(@a, @rest...) { ... }` |

```less
// Class sebagai mixin
.bordered {
  border: 1px solid #ddd;
  border-radius: 4px;
}
.card {
  .bordered;       // menyisipkan properti dari .bordered
  padding: 16px;
}

// Mixin tersembunyi (tidak muncul di output CSS)
.text-ellipsis() {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.title {
  .text-ellipsis;
  font-size: 18px;
}

// Parametric mixin dengan default
.border-radius(@radius: 4px) {
  -webkit-border-radius: @radius;
  border-radius: @radius;
}
.button {
  .border-radius(8px);
}
.box {
  .border-radius();  // pakai default 4px
}

// @arguments variable
.box-shadow(@x: 0, @y: 2px, @blur: 4px, @color: rgba(0,0,0,.1)) {
  -webkit-box-shadow: @arguments;
  box-shadow: @arguments;
}
.card {
  .box-shadow(0, 4px, 8px, rgba(0,0,0,.2));
}

// Multiple parameters (semicolon separator)
.mixin(@color; @size: 14px; @weight: normal) {
  color: @color;
  font-size: @size;
  font-weight: @weight;
}
.text { .mixin(red, 16px, bold); }

// Variable args
.transition(@prop: all, @rest...) {
  -webkit-transition: @arguments;
  transition: @arguments;
}
.fade {
  .transition(opacity, 0.3s, ease-in-out);
}
```
