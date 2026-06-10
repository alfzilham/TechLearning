# Spacing & Sizing

## Margin

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| All sides | `m-{size}` | `m-4` = margin 16px |
| Horizontal | `mx-{size}` | `mx-auto` = center horizontal |
| Vertical | `my-{size}` | `my-4` |
| Top | `mt-{size}` | `mt-8` |
| Right | `mr-{size}` | `mr-2` |
| Bottom | `mb-{size}` | `mb-4` |
| Left | `ml-{size}` | `ml-4` |
| Negative | `-m-{size}`, `-mt-*`, dll | `-mt-4` |

```html
<!-- Margin scale -->
<div class="m-0"> 0px</div>
<div class="m-1"> 4px</div>
<div class="m-2"> 8px</div>
<div class="m-4"> 16px</div>
<div class="m-6"> 24px</div>
<div class="m-8"> 32px</div>
<div class="m-10">40px</div>

<!-- Center horizontally -->
<div class="w-96 mx-auto">Centered container</div>

<!-- Margin antar anak (gap alternatif untuk flex) -->
<div class="space-y-4">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>
```

---

## Padding

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| All sides | `p-{size}` | `p-6` |
| Horizontal | `px-{size}` | `px-6` |
| Vertical | `py-{size}` | `py-3` |
| Per sisi | `pt-*`, `pr-*`, `pb-*`, `pl-*` | `pl-8` |

```html
<!-- Card dengan padding -->
<div class="p-8 bg-white rounded-2xl shadow">
  <h2 class="text-2xl font-bold">Judul</h2>
  <p class="text-gray-600 mt-2">Konten dengan padding konsisten</p>
</div>

<!-- Button dengan padding horizontal -->
<button class="px-6 py-3 bg-blue-600 text-white rounded-lg">Button</button>
```

---

## Space Between

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Spacing antar item vertikal | `space-y-{size}` | `space-y-4` |
| Spacing antar item horizontal | `space-x-{size}` | `space-x-4` |
| Reverse | `space-x-reverse`, `space-y-reverse` | Untuk RTL |

```html
<div class="flex flex-col space-y-4">
  <div>Item 1 — jarak 16px</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>

<div class="flex space-x-4">
  <button>Button 1</button>
  <button>Button 2</button>
  <button>Button 3</button>
</div>
```

---

## Width

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Fixed width | `w-{size}` | `w-96` = 384px |
| Percentage | `w-1/2`, `w-1/3`, `w-2/3`, `w-3/4`, `w-full` | `w-1/2` = 50% |
| Viewport | `w-screen` | `w-screen` = 100vw |
| Min | `min-w-{size}`, `min-w-0`, `min-w-full` | `min-w-[280px]` |
| Max | `max-w-{size}`, `max-w-lg`, `max-w-5xl` | `max-w-4xl mx-auto` |
| Auto | `w-auto` | Sesuai konten |
| Arbitrary | `w-[500px]`, `w-[calc(100%-2rem)]` | Custom value |

```html
<!-- Lebar prosentase -->
<div class="w-1/2 bg-blue-100">50%</div>
<div class="w-1/3 bg-green-100">33%</div>

<!-- Max-width container -->
<div class="max-w-4xl mx-auto px-4">
  <p>Responsive container — maksimal 896px</p>
</div>

<!-- Min width untuk flex items -->
<div class="flex">
  <div class="min-w-[250px]">Sidebar minimal 250px</div>
  <div class="flex-1">Content</div>
</div>

<!-- Arbitrary value -->
<img class="w-[200px] h-[200px] object-cover" src="photo.jpg" alt="" />
```

---

## Height

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Fixed height | `h-{size}` | `h-64` = 256px |
| Full | `h-full` | 100% parent |
| Screen | `h-screen` | 100vh |
| Min | `min-h-*` | `min-h-screen` |
| Max | `max-h-*` | `max-h-96` |

```html
<!-- Full screen sections -->
<section class="min-h-screen bg-gradient-to-b from-blue-500 to-purple-600">
  Hero section — min-height 100vh
</section>

<!-- Equal height cards -->
<div class="grid grid-cols-3 gap-4">
  <div class="h-full bg-white p-4">Full height card</div>
</div>
```

---

## Size (Tailwind v3.4+)

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Width & Height | `size-{size}` | `size-8` = 32x32px |

```html
<img class="size-12 rounded-full" src="avatar.jpg" alt="" />
<!-- Sama dengan: w-12 h-12 -->
```
