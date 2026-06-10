# Nesting & Mixin

## Nesting

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Nested selector | Menulis selector di dalam selector | `.parent { .child { } }` |
| `&` parent | Referensi ke selector induk | `&:hover`, `&--active` |
| `&.class` | Parent dengan class | `.card { &.active { } }` → `.card.active` |
| `@media` nesting | Media query di dalam selector | `.box { @media (max-width: 768px) { } }` |
| Nested properties | Properti dengan namespace | `font: { size: weight: }` (Less TIDAK support) |

```less
// Nesting biasa
.navbar {
  background: #333;
  padding: 16px;

  .nav-link {
    color: white;
    text-decoration: none;

    &:hover {
      color: #3498db;
    }

    &--active {
      font-weight: bold;
    }
  }

  .nav-list {
    display: flex;
    gap: 16px;
  }
}

// Output CSS:
// .navbar { background: #333; padding: 16px; }
// .navbar .nav-link { color: white; text-decoration: none; }
// .navbar .nav-link:hover { color: #3498db; }
// .navbar .nav-link--active { font-weight: bold; }
// .navbar .nav-list { display: flex; gap: 16px; }
```

### `&` — Parent Selector Examples
```less
.btn {
  padding: 8px 16px;

  // & sebagai prefix
  &-primary { background: blue; }    // .btn-primary
  &-danger { background: red; }      // .btn-danger

  // & sebagai pseudo-class
  &:hover { opacity: 0.8; }           // .btn:hover
  &:focus { outline: 2px solid; }    // .btn:focus

  // & di tengah selector
  .dark-theme & { background: black; } // .dark-theme .btn
}
```

### Nesting dengan `@media`
```less
.card {
  width: 100%;
  padding: 16px;

  @media (min-width: 768px) {
    width: 50%;
    padding: 24px;
  }

  @media (min-width: 1024px) {
    width: 33.33%;
  }
}

// Output:
// .card { width: 100%; padding: 16px; }
// @media (min-width: 768px) { .card { width: 50%; padding: 24px; } }
// @media (min-width: 1024px) { .card { width: 33.33%; } }
```

---

## Mixin

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Mixin as class | Class bisa dipakai sebagai mixin | `.a();` atau `.a;` |
| Hidden mixin | Mixin dengan `()` tidak muncul di CSS | `.mixin() { }` |
| Parametric | Mixin dengan parameter | `.mixin(@color) { }` |
| Default param | Parameter dengan nilai default | `.mixin(@color: red) { }` |
| `@arguments` | Semua parameter dalam satu variable | `border: @arguments;` |
| Variable args `...` | Menampung sisa argumen | `.mixin(@a, @rest...) { }` |

```less
// Mixin as class (biasa — muncul di CSS)
.bordered {
  border: 1px solid #ccc;
  border-radius: 4px;
}

.card {
  .bordered; // atau .bordered();
  padding: 16px;
}
// Output: .bordered { ... } dan .card { border... padding... }

// Hidden mixin (tidak muncul di CSS)
.border-radius(@radius) {
  -webkit-border-radius: @radius;
  -moz-border-radius: @radius;
  border-radius: @radius;
}

.card {
  .border-radius(8px);
}
// Output: .card { -webkit-border-radius: 8px; ... }

// Mixin dengan default parameter
.mixin(@color: red, @size: 14px) {
  color: @color;
  font-size: @size;
}

.box {
  .mixin(blue);          // color: blue, size: 14px
  .mixin(green, 18px);   // color: green, size: 18px
}

// @arguments — semua parameter
.shadow(@x: 0, @y: 2px, @blur: 4px, @color: rgba(0,0,0,0.2)) {
  box-shadow: @arguments;
}

.card { .shadow(); }
// Output: box-shadow: 0 2px 4px rgba(0,0,0,0.2)

// Variable args
.mixin(@color, @rest...) {
  color: @color;
  box-shadow: @rest;
}

.box { .mixin(red, 0 2px 4px rgba(0,0,0,0.2)); }
```

### Pattern Matching
Mixin bisa dipilih berdasarkan nilai parameter.
```less
// Mixin hanya jalan jika @color = red
.mixin(red) {
  color: red;
  font-weight: bold;
}

.mixin(blue) {
  color: blue;
  font-style: italic;
}

// Mixin default (apapun selain red/blue)
.mixin(@color) {
  color: @color;
}

.alert-danger { .mixin(red); }   // color: red; font-weight: bold
.alert-info { .mixin(blue); }    // color: blue; font-style: italic
.alert-warning { .mixin(green); } // color: green
```
