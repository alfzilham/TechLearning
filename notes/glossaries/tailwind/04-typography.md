# Typography

## Font Size

| Kelas | Ukuran | CSS |
|-------|--------|-----|
| `text-xs` | 12px | `font-size: 0.75rem` |
| `text-sm` | 14px | `font-size: 0.875rem` |
| `text-base` | 16px | `font-size: 1rem` (default) |
| `text-lg` | 18px | `font-size: 1.125rem` |
| `text-xl` | 20px | `font-size: 1.25rem` |
| `text-2xl` | 24px | `font-size: 1.5rem` |
| `text-3xl` | 30px | `font-size: 1.875rem` |
| `text-4xl` | 36px | `font-size: 2.25rem` |
| `text-5xl` | 48px | `font-size: 3rem` |
| `text-6xl` | 60px | `font-size: 3.75rem` |
| `text-7xl` | 72px | `font-size: 4.5rem` |
| `text-8xl` | 96px | `font-size: 6rem` |
| `text-9xl` | 128px | `font-size: 8rem` |
| `text-[32px]` | Arbitrary | Custom value |

```html
<h1 class="text-4xl font-bold">Heading</h1>
<h2 class="text-2xl font-semibold">Subheading</h2>
<p class="text-base">Body text</p>
<p class="text-sm text-gray-500">Small/caption text</p>
```

---

## Font Weight

| Kelas | CSS |
|-------|-----|
| `font-thin` | 100 |
| `font-extralight` | 200 |
| `font-light` | 300 |
| `font-normal` | 400 |
| `font-medium` | 500 |
| `font-semibold` | 600 |
| `font-bold` | 700 |
| `font-extrabold` | 800 |
| `font-black` | 900 |

---

## Text Alignment & Transform

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Align left | `text-left` | default untuk LTR |
| Align center | `text-center` | heading |
| Align right | `text-right` | — |
| Justify | `text-justify` | paragraf |
| Uppercase | `uppercase` | NAV LINK |
| Lowercase | `lowercase` | teks |
| Capitalize | `capitalize` | Setiap Kata |
| Normal case | `normal-case` | reset |
| Line clamp | `line-clamp-1` s/d `line-clamp-6` | batasi baris |

```html
<h1 class="text-center text-3xl font-bold">Judul di Tengah</h1>

<p class="text-justify text-gray-700 leading-relaxed">
  Paragraf dengan rata kanan-kiri (justify) dan line-height yang nyaman dibaca.
</p>

<nav class="uppercase text-sm font-semibold tracking-wider">
  Menu Navigasi
</nav>

<div class="line-clamp-3">
  <p>Teks panjang yang dipotong setelah 3 baris dengan ellipsis...</p>
</div>
```

---

## Line Height & Letter Spacing

| Konsep | Kelas | Nilai |
|--------|-------|-------|
| Leading (line-height) | `leading-none` | 1 |
| | `leading-tight` | 1.25 |
| | `leading-normal` | 1.5 |
| | `leading-relaxed` | 1.625 |
| | `leading-loose` | 2 |
| Tracking (letter-spacing) | `tracking-tighter` | -0.05em |
| | `tracking-tight` | -0.025em |
| | `tracking-normal` | 0 |
| | `tracking-wide` | 0.025em |
| | `tracking-wider` | 0.05em |
| | `tracking-widest` | 0.1em |

```html
<article class="prose prose-lg max-w-none">
  <p class="leading-relaxed text-gray-700">
    Teks dengan line-height nyaman untuk bacaan panjang.
  </p>
  <p class="tracking-wide uppercase text-sm font-semibold text-gray-500">
    SPACING LEBAR
  </p>
</article>
```

---

## Text Decoration & Color

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Color | `text-{color}-{shade}` | `text-blue-600`, `text-gray-900` |
| Decoration | `underline`, `line-through`, `no-underline` | `underline` |
| Decoration color | `decoration-{color}` | `decoration-blue-500` |
| Decoration style | `decoration-solid`, `dashed`, `dotted`, `wavy` | `underline decoration-wavy` |
| Underline offset | `underline-offset-{n}` | `underline-offset-4` |

```html
<p class="text-gray-900">Primary text color</p>
<p class="text-gray-500">Secondary/muted text</p>
<a href="#" class="underline decoration-blue-500 decoration-2 underline-offset-4 hover:no-underline">
  Link dengan underline kustom
</a>
```

---

## Utility Typography Patterns

```html
<!-- Article styling -->
<article class="max-w-3xl mx-auto px-4 py-12">
  <h1 class="text-4xl font-bold tracking-tight text-gray-900">
    Judul Artikel Blog
  </h1>
  <p class="mt-2 text-lg text-gray-500">
    Published on <time>Jan 15, 2024</time>
  </p>

  <div class="mt-8 space-y-6 text-lg leading-relaxed text-gray-700">
    <p>Paragraf pertama dengan <strong>bold text</strong> dan <em>italic</em>.</p>
    <p>Paragraf kedua dengan <a href="#" class="text-blue-600 underline">link styling</a>.</p>
  </div>
</article>

<!-- Hero text -->
<section class="text-center py-20">
  <h1 class="text-5xl sm:text-6xl lg:text-7xl font-extrabold tracking-tight">
    Build <span class="text-blue-600">Amazing</span> Products
  </h1>
  <p class="mt-6 text-xl text-gray-500 max-w-2xl mx-auto">
    Deskripsi hero yang menjelaskan value proposition dalam 1-2 kalimat.
  </p>
</section>

<!-- Truncate single line -->
<p class="truncate w-64 bg-gray-100 p-2">
  Teks yang sangat panjang ini akan dipotong menjadi satu baris dengan ellipsis di ujungnya...
</p>
```
