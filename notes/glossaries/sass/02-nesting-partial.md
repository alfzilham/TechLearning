# 02 Nesting & Partial

## Nesting

| Konsep              | Penjelasan                            | Contoh                                               |
| ------------------- | ------------------------------------- | ---------------------------------------------------- |
| Nested selector     | Tulis selector di dalam selector lain | `.parent { .child { } }`                             |
| `&` parent selector | Referensi ke parent selector          | `&:hover`, `&.active`, `&::before`                   |
| BEM modifier        | Gunakan `&--` untuk modifier BEM      | `.block { &--modifier { } }` jadi `.block--modifier` |
| BEM element         | Gunakan `&__` untuk element BEM       | `.block { &__element { } }` jadi `.block__element`   |
| Nesting &           | Chain multiple `&`                    | `&:hover & { }`                                      |
| Nesting properties  | Group properti dengan namespace sama  | `font: { size: 16px; weight: bold; }`                |
| `@at-root`          | Break out dari nesting ke root        | `.parent { @at-root .child { } }` jadi `.child`      |

```scss
// Nested selectors
.nav {
  list-style: none;

  li {
    display: inline-block;

    a {
      text-decoration: none;
      color: #333;

      &:hover {
        color: #007bff;
      }
    }
  }
}

// BEM with nesting
.card {
  background: #fff;

  &__title {
    font-size: 1.25rem;
  }

  &__body {
    padding: 1rem;
  }

  &--featured {
    border: 2px solid gold;
  }

  &--featured &__title {
    color: gold;
  }
}

// Nesting properties
.btn {
  font: {
    family: "Inter", sans-serif;
    size: 1rem;
    weight: 600;
  }

  border: 1px solid {
    color: #ddd;
    radius: 4px;
  }
}

// @at-root
.list {
  .item {
    color: #333;
  }

  @at-root .no-list {
    color: #666;
  }
}
// Output: .list .item, .no-list { }
```

## Partial

| Konsep          | Penjelasan                                             | Contoh                                       |
| --------------- | ------------------------------------------------------ | -------------------------------------------- |
| Partial file    | File SCSS diawali `_` — tidak di-compile sendiri       | `_variables.scss`                            |
| Load partial    | Gunakan `@use` tanpa path underscore                   | `@use 'variables';`                          |
| Namespace       | `@use` otomatis buat namespace dari nama file          | `variables.$color`                           |
| `@use ... as`   | Aliaskan namespace                                     | `@use 'variables' as v;` → `v.$color`        |
| `@use ... as *` | Load tanpa namespace (hati-hati konflik)               | `@use 'variables' as *;` → langsung `$color` |
| `@forward`      | Re-export partial agar bisa di-load lewat 1 file       | `@forward 'variables';`                      |
| `@import`       | **Deprecated** — tidak punya namespace, global pollusi | `@import 'variables';` (jangan dipakai)      |

```scss
// _variables.scss (partial)
$color-primary: #3498db;
$spacing: 1rem;

// _mixins.scss
@use "variables" as v;

@mixin spaced {
  margin-bottom: v.$spacing;
}

// _index.scss (barrel file)
@forward "variables";
@forward "mixins";

// main.scss
@use "index" as *;

.button {
  background: $color-primary;
  @include spaced;
}

// Dengan namespace
@use "variables" as var;

.header {
  color: var.$color-primary;
}

// @import — deprecated
// @import 'variables';   // ← JANGAN DIPAKAI
// Alasan: global pollusi, tidak ada namespace,
// sulit dilacak dependency-nya, akan dihapus dari Sass
```
