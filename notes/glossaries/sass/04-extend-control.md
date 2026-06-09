# 04 Extend & Control Flow

## Extend

| Konsep            | Penjelasan                                                     | Contoh                                           |
| ----------------- | -------------------------------------------------------------- | ------------------------------------------------ |
| `@extend`         | Warisi selector dari class lain                                | `.btn-danger { @extend .btn; background: red; }` |
| `%placeholder`    | Silent class — hanya di-compile jika di-`@extend`              | `%btn-shared { padding: 8px 16px; }`             |
| Placeholder usage | Gunakan placeholder untuk menghindari class ekstra di HTML     | `.btn { @extend %btn-shared; }`                  |
| Extend chains     | `@extend` dari hasil `@extend` lain — hati-hati bloat          | `.a { } .b { @extend .a; } .c { @extend .b; }`   |
| Module scope      | `@extend` hanya bekerja dalam module yang sama (loaded module) | Harus `@use` file yang memiliki class target     |
| Kapan hindari     | Jika selector chain jadi panjang atau CSS membengkak           | Hindari `@extend` di dalam `@media` — tidak work |

```scss
// %placeholder (silent class) — recommended
%btn-base {
  display: inline-block;
  padding: 0.5rem 1rem;
  border: none;
  font-size: 1rem;
  cursor: pointer;
}

.btn-primary {
  @extend %btn-base;
  background: #3498db;
  color: #fff;
}

.btn-secondary {
  @extend %btn-base;
  background: #95a5a6;
  color: #fff;
}

// @extend dari regular class
.error {
  border: 1px solid red;
  color: red;
}

.error--serious {
  @extend .error;
  border-width: 3px;
}

// Extend dengan placeholder — lebih aman dari extend chain
%tf-card {
  border-radius: 8px;
  padding: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.card-product {
  @extend %tf-card;
}

.card-profile {
  @extend %tf-card;
}

// @extend TIDAK bekerja di @media — gunakan mixin
// ❌ SALAH:
// @media (min-width: 768px) {
//   .card { @extend %tf-card; }  // error
// }

// ✅ BENAR: gunakan mixin
@mixin card-styles {
  border-radius: 8px;
  padding: 1rem;
}

@media (min-width: 768px) {
  .card {
    @include card-styles;
  }
}
```

## Control Flow

| Konsep                     | Penjelasan                      | Contoh                                     |
| -------------------------- | ------------------------------- | ------------------------------------------ |
| `@if`                      | Conditional dasar               | `@if $dark == true { background: #000; }`  |
| `@else if`                 | Kondisi kedua                   | `@else if $theme == 'light' { ... }`       |
| `@else`                    | Fallback                        | `@else { background: #fff; }`              |
| `@for ... through`         | Loop termasuk nilai akhir       | `@for $i from 1 through 5` → 1,2,3,4,5     |
| `@for ... to`              | Loop tidak termasuk nilai akhir | `@for $i from 1 to 5` → 1,2,3,4            |
| `@each $item in $list`     | Iterasi list                    | `@each $color in $colors { ... }`          |
| `@each $key, $val in $map` | Iterasi map                     | `@each $name, $px in $breakpoints { ... }` |
| `@while`                   | Loop selama kondisi true        | `@while $i > 0 { $i: $i - 1; }`            |

```scss
// @if / @else
$theme: "dark";

.card {
  @if $theme == "dark" {
    background: #1a1a2e;
    color: #eee;
  } @else if $theme == "light" {
    background: #fff;
    color: #333;
  } @else {
    background: #f5f5f5;
    color: #666;
  }
}

// @for — utility classes
@for $i from 1 through 4 {
  .p-#{$i} {
    padding: #{$i * 0.25}rem;
  }
}
// Output: .p-1 { padding: 0.25rem; } ... .p-4 { padding: 1rem; }

@for $i from 0 to 5 {
  .mt-#{$i} {
    margin-top: #{$i * 4}px;
  }
}
// Output: .mt-0, .mt-1 ... .mt-4 (TIDAK ada .mt-5)

// @each with list
$colors: ("primary" #3498db, "success" #2ecc71, "danger" #e74c3c);

@each $name, $hex in $colors {
  .btn-#{$name} {
    background: $hex;
    color: #fff;

    &:hover {
      background: darken($hex, 10%);
    }
  }
}

// @each dengan multiple assignment
$sizes: 8px 12px 16px 24px;
$labels: xs sm md lg;

@each $size, $label in zip($sizes, $labels) {
  .fs-#{$label} {
    font-size: $size;
  }
}

// @while — grid columns
$columns: 12;
$i: 1;

@while $i <= $columns {
  .col-#{$i} {
    width: percentage($i / $columns);
  }
  $i: $i + 1;
}
```
