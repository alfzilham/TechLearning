# Dasar & Instalasi

## Setup

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `npm install -D tailwindcss` | Install Tailwind sebagai dev dependency | `npm i -D tailwindcss @tailwindcss/postcss postcss` |
| `npx tailwindcss init` | Generate `tailwind.config.js` | `npx tailwindcss init -p` (with PostCSS) |
| `@tailwind` directives | Import utility layers | `@tailwind base; @tailwind components; @tailwind utilities` |
| `content` config | Path file yang di-scan Tailwind | `content: ['./src/**/*.{js,ts,jsx,tsx}']` |

```bash
# Install
npm install -D tailwindcss @tailwindcss/postcss postcss
npx tailwindcss init -p
```

```js
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
    './app/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

```css
/* globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

---

## Integrasi dengan Framework

| Framework | Setup |
|-----------|-------|
| Next.js | Built-in support, langsung pakai className |
| Vite + React | `npm i -D tailwindcss @tailwindcss/vite` + plugin di vite.config |
| Create React App | `npm i -D tailwindcss postcss autoprefixer` + postcss.config.js |

```tsx
// Next.js — sudah include Tailwind by default
export default function Home() {
  return <h1 className="text-3xl font-bold underline">Hello</h1>;
}

// Vite — tambah plugin
// vite.config.ts
import tailwindcss from '@tailwindcss/vite';
export default defineConfig({ plugins: [react(), tailwindcss()] });
```

---

## Utility Classes Dasar

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Utility-first | Bangun UI dari utility classes kecil | `flex justify-center items-center p-4` |
| No custom CSS | Minimal CSS manual | Hanya utility di HTML/JSX |
| Consistent scale | Spacing, color, font pakai skala tetap | `p-4`, `text-lg`, `m-2` |

```html
<!-- Utility-first approach -->
<div class="flex items-center justify-between bg-white p-6 rounded-xl shadow-lg">
  <div class="flex items-center gap-4">
    <img class="w-12 h-12 rounded-full" src="avatar.jpg" alt="" />
    <div>
      <h2 class="text-xl font-semibold text-gray-800">John Doe</h2>
      <p class="text-sm text-gray-500">Developer</p>
    </div>
  </div>
  <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition">
    Follow
  </button>
</div>
```
