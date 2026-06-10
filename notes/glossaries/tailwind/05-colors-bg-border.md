# Colors, Background & Border

## Color Palette

| Shade | 50 | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 | 950 |
|-------|:--:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **slate** | #f8fafc | #f1f5f9 | #e2e8f0 | #cbd5e1 | #94a3b8 | #64748b | #475569 | #334155 | #1e293b | #0f172a | #020617 |
| **gray** | #f9fafb | #f3f4f6 | #e5e7eb | #d1d5db | #9ca3af | #6b7280 | #4b5563 | #374151 | #1f2937 | #111827 | #030712 |
| **zinc** | #fafafa | #f4f4f5 | #e4e4e7 | #d4d4d8 | #a1a1aa | #71717a | #52525b | #3f3f46 | #27272a | #18181b | #09090b |
| **neutral** | #fafafa | #f5f5f5 | #e5e5e5 | #d4d4d4 | #a3a3a3 | #737373 | #525252 | #404040 | #262626 | #171717 | #0a0a0a |
| **red** | #fef2f2 | #fee2e2 | #fecaca | #fca5a5 | #f87171 | #ef4444 | #dc2626 | #b91c1c | #991b1b | #7f1d1d | #450a0a |
| **orange** | #fff7ed | #ffedd5 | #fed7aa | #fdba74 | #fb923c | #f97316 | #ea580c | #c2410c | #9a3412 | #7c2d12 | #431407 |
| **amber** | #fffbeb | #fef3c7 | #fde68a | #fcd34d | #fbbf24 | #f59e0b | #d97706 | #b45309 | #92400e | #78350f | #451a03 |
| **yellow** | #fefce8 | #fef9c3 | #fef08a | #fde047 | #facc15 | #eab308 | #ca8a04 | #a16207 | #854d0e | #713f12 | #422006 |
| **green** | #f0fdf4 | #dcfce7 | #bbf7d0 | #86efac | #4ade80 | #22c55e | #16a34a | #15803d | #166534 | #14532d | #052e16 |
| **emerald** | #ecfdf5 | #d1fae5 | #a7f3d0 | #6ee7b7 | #34d399 | #10b981 | #059669 | #047857 | #065f46 | #064e3b | #022c22 |
| **teal** | #f0fdfa | #ccfbf1 | #99f6e4 | #5eead4 | #2dd4bf | #14b8a6 | #0d9488 | #0f766e | #115e59 | #134e4a | #042f2e |
| **cyan** | #ecfeff | #cffafe | #a5f3fc | #67e8f9 | #22d3ee | #06b6d4 | #0891b2 | #0e7490 | #155e75 | #164e63 | #083344 |
| **sky** | #f0f9ff | #e0f2fe | #bae6fd | #7dd3fc | #38bdf8 | #0ea5e9 | #0284c7 | #0369a1 | #075985 | #0c4a6e | #082f49 |
| **blue** | #eff6ff | #dbeafe | #bfdbfe | #93c5fd | #60a5fa | #3b82f6 | #2563eb | #1d4ed8 | #1e40af | #1e3a8a | #172554 |
| **indigo** | #eef2ff | #e0e7ff | #c7d2fe | #a5b4fc | #818cf8 | #6366f1 | #4f46e5 | #4338ca | #3730a3 | #312e81 | #1e1b4b |
| **purple** | #faf5ff | #f3e8ff | #e9d5ff | #d8b4fe | #c084fc | #a855f7 | #9333ea | #7e22ce | #6b21a8 | #581c87 | #3b0764 |
| **pink** | #fdf2f8 | #fce7f3 | #fbcfe8 | #f9a8d4 | #f472b6 | #ec4899 | #db2777 | #be185d | #9d174d | #831843 | #500724 |

---

## Background

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Background color | `bg-{color}-{shade}` | `bg-blue-500` |
| Transparent | `bg-transparent` | — |
| Opacity | `/opacity` | `bg-blue-500/50` (50% opacity) |

```html
<div class="bg-blue-500 text-white p-4">Blue background</div>
<div class="bg-blue-500/20 p-4">Blue with 20% opacity</div>
<div class="bg-gradient-to-r from-blue-500 to-purple-600 p-8 text-white">
  Gradient background
</div>
```

---

## Gradients

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Direction | `bg-gradient-to-{t/r/b/l/tr/tl/br/bl}` | `bg-gradient-to-r` |
| Start color | `from-{color}` | `from-blue-500` |
| Mid color (opsional) | `via-{color}` | `via-purple-500` |
| End color | `to-{color}` | `to-pink-500` |

```html
<div class="bg-gradient-to-r from-cyan-500 to-blue-500">Blue gradient</div>
<div class="bg-gradient-to-br from-green-400 via-blue-500 to-purple-600">Multi gradient</div>
<button class="bg-gradient-to-r from-purple-500 to-pink-500 text-white px-6 py-3 rounded-lg">
  Gradient Button
</button>
```

---

## Border

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Width | `border`, `border-0`, `border-2`, `border-4`, `border-8` | `border` = 1px |
| Color | `border-{color}-{shade}` | `border-gray-300` |
| Side | `border-t`, `border-r`, `border-b`, `border-l` | `border-b-2` |
| Radius | `rounded`, `rounded-{sm/md/lg/xl/2xl/3xl/full}` | `rounded-lg` |
| Per corner | `rounded-t-*`, `rounded-b-*`, `rounded-l-*`, `rounded-r-*` | `rounded-t-xl` |

```html
<div class="border border-gray-300 rounded-lg p-4">Card with border</div>
<div class="border-2 border-blue-500 rounded-xl p-4">Blue border</div>
<div class="border-b-2 border-gray-200 pb-2">Bottom border only</div>
<img class="rounded-full w-16 h-16" src="avatar.jpg" alt="" />
<button class="rounded-full px-6 py-2 bg-blue-600 text-white">Pill button</button>
<div class="rounded-t-xl border p-4">Top corners rounded</div>
```

---

## Ring & Divide

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Ring (outline) | `ring`, `ring-{n}`, `ring-{color}` | `ring-2 ring-blue-500` |
| Ring offset | `ring-offset-{n}` | `ring-offset-2` |
| Divide (antar anak) | `divide-{x/y}-{n}`, `divide-{color}` | `divide-y-2 divide-gray-200` |

```html
<!-- Focus ring -->
<input
  class="ring-2 ring-blue-500 rounded-lg px-4 py-2 focus:outline-none focus:ring-4"
  placeholder="Input with ring"
/>

<!-- Divider antar item -->
<ul class="divide-y divide-gray-200">
  <li class="py-3">Item 1</li>
  <li class="py-3">Item 2</li>
  <li class="py-3">Item 3</li>
</ul>
```

---

## Shadow

| Kelas | Nilai |
|-------|-------|
| `shadow-sm` | `0 1px 2px 0 rgba(0,0,0,0.05)` |
| `shadow` | `0 1px 3px 0 rgba(0,0,0,0.1)` |
| `shadow-md` | `0 4px 6px -1px rgba(0,0,0,0.1)` |
| `shadow-lg` | `0 10px 15px -3px rgba(0,0,0,0.1)` |
| `shadow-xl` | `0 20px 25px -5px rgba(0,0,0,0.1)` |
| `shadow-2xl` | `0 25px 50px -12px rgba(0,0,0,0.25)` |
| `shadow-inner` | `inset 0 2px 4px 0 rgba(0,0,0,0.05)` |
| `shadow-none` | `none` |
| Warna shadow | `shadow-blue-500/50` |

```html
<div class="shadow-sm">Small shadow</div>
<div class="shadow-md">Medium shadow</div>
<div class="shadow-lg">Large shadow</div>
<div class="shadow-xl shadow-blue-500/30">Blue colored shadow</div>
```

---

## Opacity

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Opacity | `opacity-{0-100}` | `opacity-50` = 50% |

```html
<button class="opacity-60 hover:opacity-100 transition">Hover to full opacity</button>
<div class="bg-black/50">50% black overlay (Tailwind v3.3+)</div>
```
