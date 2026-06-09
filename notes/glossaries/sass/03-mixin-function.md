# 03 Mixin & Function

## Mixin

| Konsep        | Penjelasan                               | Contoh                                                         |
| ------------- | ---------------------------------------- | -------------------------------------------------------------- |
| `@mixin`      | Definisikan kumpulan deklarasi reusable  | `@mixin center { display: flex; ... }`                         |
| `@include`    | Gunakan mixin di selector                | `.box { @include center; }`                                    |
| Argument      | Mixin dengan parameter                   | `@mixin size($w, $h) { width: $w; height: $h; }`               |
| Default arg   | Parameter dengan nilai default           | `@mixin gap($g: 1rem) { gap: $g; }`                            |
| `@content`    | Content block — kirim CSS ke dalam mixin | `@mixin mobile { @media ... { @content } }`                    |
| Vendor prefix | Mixin untuk prefix CSS otomatis          | `@mixin flex { display: -webkit-flex; display: flex; }`        |
| Responsive    | Mixin untuk breakpoint                   | `@mixin respond($bp) { @media (min-width: $bp) { @content } }` |

```scss
// Basic mixin
@mixin center {
  display: flex;
  align-items: center;
  justify-content: center;
}

.container {
  @include center;
}

// Mixin with arguments & defaults
@mixin size($width, $height: $width) {
  width: $width;
  height: $height;
}

.avatar {
  @include size(48px);
}

.hero {
  @include size(100%, 500px);
}

// @content block — responsive mixin
$breakpoints: (
  sm: 576px,
  md: 768px,
  lg: 992px,
);

@mixin respond($bp) {
  @if map-has-key($breakpoints, $bp) {
    @media (min-width: map-get($breakpoints, $bp)) {
      @content;
    }
  }
}

.card {
  display: grid;
  grid-template-columns: 1fr;

  @include respond(md) {
    grid-template-columns: 1fr 1fr;
  }

  @include respond(lg) {
    grid-template-columns: 1fr 1fr 1fr;
  }
}

// Vendor prefix mixin
@mixin border-radius($r) {
  -webkit-border-radius: $r;
  -moz-border-radius: $r;
  border-radius: $r;
}

.btn {
  @include border-radius(8px);
}
```

## Function

| Konsep          | Penjelasan                     | Contoh                                     |
| --------------- | ------------------------------ | ------------------------------------------ |
| `@function`     | Definisikan function kustom    | `@function double($n) { @return $n * 2; }` |
| `@return`       | Kembalikan nilai dari function | `@return $value;`                          |
| Built-in module | Gunakan module bawaan Sass     | `@use 'sass:math';`                        |
| `sass:math`     | Fungsi matematika              | `math.div(10, 3)`                          |
| `sass:color`    | Fungsi manipulasi warna        | `color.lighten(#333, 20%)`                 |
| `sass:string`   | Fungsi manipulasi string       | `string.to-upper-case('hello')`            |
| `sass:map`      | Fungsi manipulasi map          | `map.get($map, $key)`                      |
| `sass:list`     | Fungsi manipulasi list         | `list.nth($list, 1)`                       |
| `sass:meta`     | Fungsi introspection           | `meta.type-of($var)`                       |

```scss
@use "sass:math";
@use "sass:color";

// Custom function
@function rem($px, $base: 16px) {
  @return math.div($px, $base) * 1rem;
}

@function fluid-size($min, $max, $min-vw: 320px, $max-vw: 1200px) {
  @return clamp(
    #{$min},
    calc(
      #{$min} + (#{$max} - #{$min}) *
        ((100vw - #{$min-vw}) / (#{$max-vw} - #{$min-vw}))
    ),
    #{$max}
  );
}

@function tint($color, $amount) {
  @return color.mix(white, $color, $amount);
}

@function shade($color, $amount) {
  @return color.mix(black, $color, $amount);
}

// Usage
body {
  font-size: rem(16);
  line-height: fluid-size(1.4, 1.6);
}

.card {
  background: tint(#3498db, 30%);
  border-color: shade(#3498db, 20%);
}

// Multiply atau bagi tanpa sass:math
// Di Dart Sass 2+, / cuma untuk CSS division — gunakan math.div()
@function aspect-ratio($w, $h) {
  @return math.div($h, $w) * 100%;
}

.video {
  padding-bottom: aspect-ratio(16, 9);
}
```
