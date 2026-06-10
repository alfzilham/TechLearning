# Config, Customization & Animation

## Konfigurasi tailwind.config.js

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ['./src/**/*.{js,ts,jsx,tsx}'],

  // Dark mode: 'media' (system) atau 'class' (toggle manual)
  darkMode: 'class',

  theme: {
    // Ekstend — tambah tanpa override default
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          100: '#dbeafe',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
        },
        custom: '#abcdef',
      },

      fontFamily: {
        sans: ['Inter', 'sans-serif'],
        mono: ['Fira Code', 'monospace'],
      },

      fontSize: {
        'xxs': '0.65rem',
      },

      spacing: {
        '18': '4.5rem',
        '88': '22rem',
      },

      borderRadius: {
        '4xl': '2rem',
      },

      animation: {
        'fade-in': 'fadeIn 0.5s ease-in-out',
        'slide-up': 'slideUp 0.3s ease-out',
      },

      keyframes: {
        fadeIn: {
          '0%': { opacity: '0' },
          '100%': { opacity: '1' },
        },
        slideUp: {
          '0%': { transform: 'translateY(20px)', opacity: '0' },
          '100%': { transform: 'translateY(0)', opacity: '1' },
        },
      },
    },
  },

  plugins: [
    require('@tailwindcss/forms'),
    require('@tailwindcss/typography'),
    require('@tailwindcss/aspect-ratio'),
  ],
};
```

---

## @apply & @layer

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `@apply` | Menggabungkan utility classes ke CSS custom | `@apply px-4 py-2 bg-blue-500 text-white rounded` |
| `@layer` | Atur urutan prioritas CSS | `@layer base { }`, `@layer components { }`, `@layer utilities { }` |

```css
/* Menggabungkan utility ke custom class */
@layer components {
  .btn {
    @apply inline-flex items-center justify-center px-4 py-2 rounded-lg font-medium transition duration-200;
  }

  .btn-primary {
    @apply btn bg-blue-600 text-white hover:bg-blue-700;
  }

  .btn-secondary {
    @apply btn bg-gray-200 text-gray-800 hover:bg-gray-300;
  }

  .btn-danger {
    @apply btn bg-red-500 text-white hover:bg-red-600;
  }

  .btn-sm {
    @apply px-3 py-1 text-sm;
  }

  .btn-lg {
    @apply px-6 py-3 text-lg;
  }

  .card {
    @apply bg-white rounded-xl shadow-md p-6;
  }
}

@layer base {
  h1 {
    @apply text-4xl font-bold;
  }
  h2 {
    @apply text-2xl font-semibold;
  }
  a {
    @apply text-blue-600 hover:text-blue-800;
  }
}
```

---

## Custom Utilities dengan Plugin

```js
// tailwind.config.js
const plugin = require('tailwindcss/plugin');

module.exports = {
  plugins: [
    plugin(function({ addUtilities, addComponents, addBase, theme }) {
      addUtilities({
        '.text-shadow': {
          textShadow: '2px 2px 4px rgba(0,0,0,0.3)',
        },
        '.scrollbar-hide': {
          '-ms-overflow-style': 'none',
          'scrollbar-width': 'none',
          '&::-webkit-scrollbar': { display: 'none' },
        },
      });
    }),
  ],
};
```

---

## Animasi

| Konsep | Kelas | Contoh |
|--------|-------|--------|
| Transition | `transition` | `transition` = `transition: all 150ms` |
| Duration | `duration-{ms}` | `duration-300` |
| Timing | `ease-linear`, `ease-in`, `ease-out`, `ease-in-out` | `ease-out` |
| Delay | `delay-{ms}` | `delay-200` |
| Transform | `scale-{n}`, `rotate-{deg}`, `translate-{x/y}-{n}` | `hover:scale-105` |
| Origin | `origin-*` | `origin-center` |
| Built-in anim | `animate-spin`, `animate-ping`, `animate-pulse`, `animate-bounce` | `animate-spin` |

```html
<!-- Transition dasar -->
<button class="bg-blue-500 hover:bg-blue-700 transition duration-300 ease-in-out text-white px-4 py-2 rounded">
  Hover me
</button>

<!-- Scale on hover -->
<img class="hover:scale-110 transition duration-300 cursor-pointer" src="photo.jpg" alt="" />

<!-- Rotate -->
<div class="hover:rotate-180 transition duration-500">Rotate 180°</div>

<!-- Translate -->
<div class="hover:translate-y-[-4px] transition">Lift on hover</div>

<!-- Loading spinner -->
<div class="animate-spin h-8 w-8 border-4 border-blue-500 border-t-transparent rounded-full"></div>

<!-- Pulse animation -->
<div class="animate-pulse bg-gray-200 h-12 w-full rounded"></div>

<!-- Ping (notification badge) -->
<div class="relative">
  <button>Notifications</button>
  <span class="absolute top-0 right-0 animate-ping h-3 w-3 bg-red-500 rounded-full"></span>
</div>

<!-- Bounce -->
<div class="animate-bounce">↓ Scroll down</div>
```

---

## Custom Animation Example

```css
/* globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer utilities {
  .animate-fade-in {
    animation: fadeIn 0.5s ease-out;
  }

  .animate-slide-up {
    animation: slideUp 0.3s ease-out;
  }

  .animate-scale-in {
    animation: scaleIn 0.2s ease-out;
  }
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes slideUp {
  from { transform: translateY(20px); opacity: 0; }
  to { transform: translateY(0); opacity: 1; }
}

@keyframes scaleIn {
  from { transform: scale(0.95); opacity: 0; }
  to { transform: scale(1); opacity: 1; }
}
```

---

## safelist

```js
// tailwind.config.js — cegah purge untuk dynamic classes
module.exports = {
  safelist: [
    'bg-red-500',
    'bg-green-500',
    'bg-blue-500',
    'text-center',
    'text-lg',
    'font-bold',
    { pattern: /^bg-/ }, // semua bg-
    { pattern: /^text-(red|green|blue)-(500|600)$/ },
  ],
};
```

---

## Contoh Lengkap

```html
<div class="min-h-screen bg-gray-50 dark:bg-gray-900 p-8 transition-colors duration-500">
  <!-- Card dengan animasi -->
  <div class="max-w-md mx-auto bg-white dark:bg-gray-800 rounded-2xl shadow-lg p-6 animate-fade-in">

    <!-- Avatar dengan pulse -->
    <div class="relative inline-flex">
      <img class="w-16 h-16 rounded-full" src="avatar.jpg" alt="" />
      <span class="absolute bottom-0 right-0 h-4 w-4 bg-green-500 rounded-full ring-2 ring-white"></span>
    </div>

    <!-- Text -->
    <h2 class="mt-4 text-xl font-bold text-gray-900 dark:text-white">John Doe</h2>
    <p class="text-gray-500 dark:text-gray-400">Full Stack Developer</p>

    <!-- Button dengan hover & transition -->
    <button class="mt-6 w-full bg-blue-600 hover:bg-blue-700 active:scale-95 transition-all duration-200 text-white font-semibold py-3 px-6 rounded-xl">
      Follow
    </button>

    <!-- Loading skeleton -->
    <div class="mt-6 space-y-3 animate-pulse">
      <div class="h-4 bg-gray-200 dark:bg-gray-700 rounded w-3/4"></div>
      <div class="h-4 bg-gray-200 dark:bg-gray-700 rounded w-1/2"></div>
    </div>

  </div>
</div>
```
