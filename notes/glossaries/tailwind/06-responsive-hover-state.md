# Responsive & State Variants

## Breakpoints

| Prefix | Min-width | Target |
|--------|-----------|--------|
| `sm:` | 640px | Mobile landscape |
| `md:` | 768px | Tablet |
| `lg:` | 1024px | Desktop |
| `xl:` | 1280px | Large desktop |
| `2xl:` | 1536px | Extra large |

```html
<!-- Responsive grid -->
<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
  <div class="bg-white p-4 rounded shadow">Card</div>
  <div class="bg-white p-4 rounded shadow">Card</div>
  <div class="bg-white p-4 rounded shadow">Card</div>
  <div class="bg-white p-4 rounded shadow">Card</div>
</div>

<!-- Responsive text -->
<h1 class="text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-bold">
  Responsive Heading
</h1>

<!-- Responsive padding -->
<div class="p-4 sm:p-6 md:p-8 lg:p-12">
  Responsive padding
</div>

<!-- Hide/show based on screen -->
<img class="hidden md:block" src="desktop-image.jpg" alt="" />
<img class="block md:hidden" src="mobile-image.jpg" alt="" />
```

---

## Hover & Focus

| State | Prefix | Keterangan |
|-------|--------|-----------|
| Hover | `hover:` | Mouse di atas elemen |
| Focus | `focus:` | Elemen mendapat fokus |
| Focus visible | `focus-visible:` | Keyboard focus saja |
| Active | `active:` | Sedang diklik |
| Visited | `visited:` | Link sudah dikunjungi |
| Disabled | `disabled:` | Elemen nonaktif |

```html
<!-- Hover effect -->
<button class="bg-blue-500 hover:bg-blue-700 text-white px-4 py-2 rounded transition">
  Hover me
</button>

<!-- Focus ring -->
<input
  class="border border-gray-300 focus:border-blue-500 focus:ring-2 focus:ring-blue-200 rounded px-4 py-2 outline-none"
  placeholder="Focus on me"
/>

<!-- Active press effect -->
<button class="bg-green-500 hover:bg-green-600 active:scale-95 transition text-white px-6 py-3 rounded-lg">
  Click me
</button>

<!-- Disabled state -->
<button class="bg-gray-300 text-gray-500 cursor-not-allowed px-4 py-2 rounded" disabled>
  Disabled
</button>

<!-- Link visited -->
<a href="#" class="text-blue-600 visited:text-purple-600 underline">Link</a>
```

---

## Group & Peer

| Konsep | Prefix | Keterangan |
|--------|--------|-----------|
| Group hover | `group`, `group-hover:` | Style child saat parent di-hover |
| Group focus | `group-focus:` | Style child saat parent di-focus |
| Peer | `peer`, `peer-*:` | Style sibling saat elemen di-* |

```html
<!-- Group hover — card reveal button -->
<div class="group relative bg-white p-6 rounded-xl shadow hover:shadow-lg transition cursor-pointer">
  <h3 class="text-xl font-semibold">Card Title</h3>
  <p class="text-gray-600 mt-2">Card description</p>
  <button class="mt-4 opacity-0 group-hover:opacity-100 transition bg-blue-600 text-white px-4 py-2 rounded">
    Hidden until hover
  </button>
</div>

<!-- Peer — show/hide based on sibling state -->
<div class="space-y-2">
  <input type="checkbox" id="agree" class="peer" />
  <label for="agree" class="ml-2">Setuju dengan syarat</label>
  <p class="peer-checked:text-green-600 text-sm text-gray-500">
    Terima kasih! ✓
  </p>
</div>

<!-- Peer invalid — show error message -->
<div class="space-y-1">
  <input type="email" required class="peer border rounded p-2" placeholder="Email" />
  <p class="hidden peer-invalid:block text-red-500 text-sm">Email tidak valid</p>
</div>
```

---

## Dark Mode

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Dark mode | `dark:` | `dark:bg-gray-900 dark:text-white` |

```html
<!-- Dark mode card — otomatis berdasarkan system preference atau class -->
<div class="bg-white dark:bg-gray-800 text-gray-900 dark:text-white p-6 rounded-xl shadow">
  <h3 class="text-xl font-semibold">Dark mode ready</h3>
  <p class="text-gray-600 dark:text-gray-400 mt-2">This card adapts to dark mode.</p>
</div>

<!-- Dark mode button variants -->
<button class="bg-blue-500 dark:bg-blue-600 hover:bg-blue-700 dark:hover:bg-blue-500 text-white px-4 py-2 rounded">
  Button
</button>
```

```js
// tailwind.config.js — enable dark mode class-based
module.exports = {
  darkMode: 'class', // or 'media' (default, based on system)
};
```

---

## Motion Variants

| Konsep | Prefix | Keterangan |
|--------|--------|-----------|
| Reduced motion | `motion-safe:` | Hanya jika user tidak prefer reduced motion |
| | `motion-reduce:` | Hanya jika user prefer reduced motion |

```html
<!-- Animasi hanya untuk user yang tidak prefer reduced motion -->
<div class="motion-safe:animate-bounce motion-reduce:animate-none">
  Animated element
</div>
```

---

## ARIA & Data Attributes

| Konsep | Prefix | Contoh |
|--------|--------|--------|
| ARIA state | `aria-*:` | `aria-expanded:` `aria-checked:` `aria-selected:` |
| Data attribute | `data-*:` | `data-active:` `data-open:` |

```html
<!-- ARIA expanded -->
<button aria-expanded="false" class="aria-expanded:bg-blue-100">
  Toggle
</button>

<!-- Data attribute -->
<div data-active="true" class="data-[active=true]:bg-green-100">
  Active item
</div>
```

---

## Open/Closed Details

```html
<details class="open:bg-blue-50 open:ring-2 open:ring-blue-500 rounded-lg p-4 transition">
  <summary class="font-semibold cursor-pointer">Click to expand</summary>
  <p class="mt-2 text-gray-600">Konten yang muncul saat dibuka.</p>
</details>
```
