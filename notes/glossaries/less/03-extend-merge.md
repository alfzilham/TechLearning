# Extend & Merge

## Extend

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `&:extend(.class)` | Mewarisi style dari selector lain | `&:extend(.btn)` |
| `&:extend(.class all)` | Extend termasuk nested instances | `&:extend(.btn all)` |
| Extend vs Mixin | Extend = grouping selector, Mixin = copy style | — |

```less
// Tanpa extend — duplikasi
.btn {
  padding: 10px 20px;
  border-radius: 4px;
  font-size: 14px;
}

.btn-primary {
  padding: 10px 20px;
  border-radius: 4px;
  font-size: 14px;
  background: blue;
  color: white;
}
/* Output — duplikasi properti */

// Dengan extend — lebih efisien
.btn {
  padding: 10px 20px;
  border-radius: 4px;
  font-size: 14px;
}

.btn-primary {
  &:extend(.btn);
  background: blue;
  color: white;
}

.btn-danger {
  &:extend(.btn);
  background: red;
  color: white;
}

/* OUTPUT CSS:
.btn,
.btn-primary,
.btn-danger {
  padding: 10px 20px;
  border-radius: 4px;
  font-size: 14px;
}

.btn-primary { background: blue; color: white; }
.btn-danger { background: red; color: white; }
*/
```

### `&:extend(.class all)`
Juga mewarisi style dari nested instances.
```less
.btn {
  padding: 10px;

  .icon {
    margin-right: 8px;
  }
}

.btn-large {
  &:extend(.btn all);
  // Juga mewarisi .btn .icon
  padding: 20px;
}
```

### Extend pada selector yang lebih kompleks
```less
// Bisa extend selector dengan multiple class
a.important {
  font-weight: bold;
  color: red;
}

.btn {
  &:extend(a.important);
  // Sama dengan: .btn { font-weight: bold; color: red; }
}

// Bisa extend dengan pseudo-class
:hover {
  text-decoration: underline;
}

.link {
  &:extend(:hover);
}
```

### Extend vs Mixin
```less
// Mixin — copy style (CSS lebih besar)
.button-base() {
  padding: 8px 16px;
  border-radius: 4px;
}

.btn-primary {
  .button-base();
  background: blue;
}

.btn-secondary {
  .button-base();
  background: gray;
}
/* Output — duplikasi padding/border */

// Extend — grouping (CSS lebih kecil)
.button-base {
  padding: 8px 16px;
  border-radius: 4px;
}

.btn-primary {
  &:extend(.button-base);
  background: blue;
}

.btn-secondary {
  &:extend(.button-base);
  background: gray;
}
/* Output — padding/border di-group */
```

---

## Merge

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Comma merge `+` | Menggabungkan nilai dengan koma | `.mixin()+ { }` |
| Space merge `+_` | Menggabungkan nilai dengan spasi | `.mixin()+_ { }` |

### Comma Merge `+`
Untuk properti yang menerima multiple values dengan koma.
```less
// Tanpa merge
.mixin-shadow() {
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.card {
  .mixin-shadow();
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
}
// Output — OVERRIDE! shadow pertama hilang

// Dengan merge +
.mixin-shadow() {
  box-shadow+: 0 2px 4px rgba(0,0,0,0.1);
}

.card {
  .mixin-shadow();
  box-shadow+: 0 4px 8px rgba(0,0,0,0.2);
}
// Output: box-shadow: 0 2px 4px ..., 0 4px 8px ...;
```

### Space Merge `+_`
Untuk properti yang menggabungkan dengan spasi.
```less
.mixin-transition() {
  transition+: transform 0.3s;
}

.card {
  .mixin-transition();
  transition+: opacity 0.2s;
}
// Output: transition: transform 0.3s, opacity 0.2s;
// (comma, karena transition juga pakai koma)

// Space merge untuk properti seperti background, transform
.mixin-bg() {
  background+_: url("pattern.png") no-repeat;
}

.hero {
  .mixin-bg();
  background+_: linear-gradient(to right, blue, purple);
}
// Output: background: url("pattern.png") no-repeat linear-gradient(...);
```
