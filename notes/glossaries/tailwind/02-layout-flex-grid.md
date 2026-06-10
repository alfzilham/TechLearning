# Layout: Flex & Grid

## Flexbox

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| `display: flex` | `flex` | `flex` |
| `flex-direction: row/col` | `flex-row`, `flex-col` | `flex flex-col` |
| `flex-wrap` | `flex-wrap`, `flex-nowrap` | `flex-wrap` |
| `justify-content` | `justify-start`, `center`, `between`, `end`, `evenly`, `around` | `justify-between` |
| `align-items` | `items-start`, `center`, `end`, `stretch`, `baseline` | `items-center` |
| `align-self` | `self-start`, `center`, `end`, `stretch` | `self-center` |
| `flex: 1` | `flex-1` | `flex-1` |
| `gap` | `gap-{size}`, `gap-x-`, `gap-y-` | `gap-4` |

```html
<!-- Navbar -->
<nav class="flex items-center justify-between px-6 py-4 bg-white shadow">
  <div class="flex items-center gap-8">
    <span class="text-xl font-bold">Logo</span>
    <div class="flex gap-6">
      <a href="#" class="hover:text-blue-600">Home</a>
      <a href="#" class="hover:text-blue-600">About</a>
      <a href="#" class="hover:text-blue-600">Contact</a>
    </div>
  </div>
  <button class="px-4 py-2 bg-blue-600 text-white rounded-lg">Login</button>
</nav>

<!-- Card grid dengan flex wrap -->
<div class="flex flex-wrap gap-4 p-6">
  <div class="flex-1 min-w-[280px] bg-white p-4 rounded-lg shadow">Card 1</div>
  <div class="flex-1 min-w-[280px] bg-white p-4 rounded-lg shadow">Card 2</div>
  <div class="flex-1 min-w-[280px] bg-white p-4 rounded-lg shadow">Card 3</div>
</div>

<!-- Column layout -->
<div class="flex flex-col items-center justify-center min-h-screen">
  <h1 class="text-4xl font-bold">Centered Content</h1>
  <p class="text-gray-600 mt-2">Vertically and horizontally centered</p>
</div>
```

---

## Grid

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| `display: grid` | `grid` | `grid` |
| `grid-template-columns` | `grid-cols-1` s/d `grid-cols-12` | `grid-cols-3` |
| `grid-template-rows` | `grid-rows-*` | `grid-rows-3` |
| `gap` | `gap-*` | `gap-6` |
| `column-span` | `col-span-*` | `col-span-2` |
| `row-span` | `row-span-*` | `row-span-2` |
| `column-start/end` | `col-start-*`, `col-end-*`, `col-span-full` | `col-span-full` |
| `auto-fit/fill` | `grid-cols-[repeat(auto-fit,minmax(200px,1fr))]` | Custom |

```html
<!-- Basic grid 3 kolom -->
<div class="grid grid-cols-3 gap-6 p-6">
  <div class="bg-white p-4 rounded-lg shadow">Item 1</div>
  <div class="bg-white p-4 rounded-lg shadow">Item 2</div>
  <div class="bg-white p-4 rounded-lg shadow">Item 3</div>
</div>

<!-- Grid dengan span -->
<div class="grid grid-cols-4 gap-4 p-6">
  <div class="col-span-2 bg-blue-100 p-4 rounded">Span 2 kolom</div>
  <div class="bg-green-100 p-4 rounded">Item</div>
  <div class="bg-green-100 p-4 rounded">Item</div>
  <div class="col-span-3 bg-yellow-100 p-4 rounded">Span 3 kolom</div>
  <div class="bg-green-100 p-4 rounded">Item</div>
</div>

<!-- Responsive grid (auto-fit) -->
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
  <div class="bg-white rounded-lg shadow p-4">Card</div>
  <div class="bg-white rounded-lg shadow p-4">Card</div>
  <div class="bg-white rounded-lg shadow p-4">Card</div>
  <div class="bg-white rounded-lg shadow p-4">Card</div>
</div>

<!-- Aside + Content layout -->
<div class="grid grid-cols-[250px_1fr] min-h-screen">
  <aside class="bg-gray-100 p-6">Sidebar</aside>
  <main class="p-6">Main Content</main>
</div>
```

---

## Container

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Max-width container | `container` | `container mx-auto` |
| Centering | `mx-auto` | `container mx-auto px-4` |

```html
<div class="container mx-auto px-4">
  <!-- Konten melebar sampai max-width, lalu centered -->
</div>
```

---

## Common Layout Patterns

```html
<!-- Card Grid Responsive -->
<section class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
  <article class="bg-white rounded-2xl shadow-lg overflow-hidden">
    <img src="img.jpg" alt="" class="w-full h-48 object-cover" />
    <div class="p-6">
      <h3 class="text-xl font-semibold">Card Title</h3>
      <p class="text-gray-600 mt-2">Card description here...</p>
    </div>
  </article>
</section>

<!-- Holy Grail Layout -->
<div class="grid grid-rows-[auto_1fr_auto] min-h-screen">
  <header class="bg-white shadow p-4">Header</header>
  <div class="grid grid-cols-[200px_1fr_200px]">
    <nav class="bg-gray-100 p-4">Sidebar</nav>
    <main class="p-6">Content</main>
    <aside class="bg-gray-100 p-4">Widgets</aside>
  </div>
  <footer class="bg-gray-800 text-white p-4">Footer</footer>
</div>
```
