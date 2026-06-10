# Advanced Patterns

## Route Groups `()`

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `(group)` | Group route tanpa pengaruh URL | `(marketing)`, `(dashboard)` |
| Layout isolation | Layout berbeda per group | `(marketing)/layout.tsx` |

```tsx
// Struktur:
app/
├── (marketing)/
│   ├── layout.tsx      // Layout marketing
│   ├── page.tsx        // /
│   └── pricing/
│       └── page.tsx    // /pricing
├── (dashboard)/
│   ├── layout.tsx      // Layout dashboard
│   └── dashboard/
│       ├── page.tsx    // /dashboard
│       └── settings/
│           └── page.tsx // /dashboard/settings
```

---

## Intercepting Routes `(.)`

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `(.)` | Intercept sibling route | Modal di atas halaman list |
| `(..)` | Intercept parent route | `(..)photo` |
| `(...)` | Intercept root route | `(...)photo` |

```tsx
// Struktur — Feed dengan modal foto:
app/
├── feed/
│   ├── page.tsx              // /feed — list foto
│   └── (..)photo/
│       └── [id]/
│           └── page.tsx      // Intercept: modal dari feed
├── photo/
│   └── [id]/
│       └── page.tsx          // /photo/123 — halaman penuh

// app/feed/layout.tsx
export default function FeedLayout({ children, modal }: {
  children: React.ReactNode;
  modal: React.ReactNode;
}) {
  return (
    <div>
      {children}
      {modal} {/* Modal foto */}
    </div>
  );
}
```

```tsx
// app/feed/page.tsx
import Link from 'next/link';

export default function Feed() {
  return (
    <div>
      {photos.map(photo => (
        <Link key={photo.id} href={`/photo/${photo.id}`}>
          <img src={photo.thumbnail} alt="" />
        </Link>
      ))}
    </div>
  );
}
```

---

## Parallel Routes `@folder`

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `@slot` | Multiple pages in one layout | `@feed`, `@sidebar` |
| `default.tsx` | Fallback jika slot tidak punya halaman | `app/@sidebar/default.tsx` |

```tsx
// app/layout.tsx
export default function Layout({
  children,
  team,
  analytics,
}: {
  children: React.ReactNode;
  team: React.ReactNode;
  analytics: React.ReactNode;
}) {
  return (
    <div className="grid grid-cols-3 gap-4">
      <main className="col-span-2">{children}</main>
      <aside className="space-y-4">
        {team}
        {analytics}
      </aside>
    </div>
  );
}

// app/@team/page.tsx — /team
export default function TeamPage() {
  return <div>Team Dashboard</div>;
}

// app/@analytics/page.tsx — /analytics
export default function AnalyticsPage() {
  return <div>Analytics Dashboard</div>;
}
```

---

## PWA (Progressive Web App)

```tsx
// app/manifest.ts
import type { MetadataRoute } from 'next';

export default function manifest(): MetadataRoute.Manifest {
  return {
    name: 'My App',
    short_name: 'MyApp',
    description: 'My PWA application',
    start_url: '/',
    display: 'standalone',
    background_color: '#ffffff',
    theme_color: '#000000',
    icons: [
      { src: '/icon-192.png', sizes: '192x192', type: 'image/png' },
      { src: '/icon-512.png', sizes: '512x512', type: 'image/png' },
    ],
  };
}
```

```tsx
// app/layout.tsx — add manifest
export const metadata: Metadata = {
  manifest: '/manifest.json',
  appleWebApp: {
    capable: true,
    statusBarStyle: 'default',
    title: 'My App',
  },
};
```

---

## Turbopack

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `--turbo` | Fast dev server dengan Turbopack | `next dev --turbo` |
| HMR | Hot Module Replacement lebih cepat | Edit code → instant update |
| Stable | Production masih Webpack | `next build` tetap Webpack |

```bash
# Dev dengan Turbopack
next dev --turbo

# package.json
{
  "scripts": {
    "dev": "next dev --turbo",
    "build": "next build"
  }
}
```

---

## Partial Prerendering (PPR)

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| PPR | Kombinasi static + dynamic dalam satu halaman | `experimental: { ppr: true }` |
| Static shell | Bagian statis di-pre-render | Navbar, footer |
| Dynamic holes | Bagian dinamis streaming | User data, real-time content |

```js
// next.config.js
module.exports = {
  experimental: {
    ppr: true,
  },
};
```

```tsx
export default function Page() {
  return (
    <div>
      {/* Static — pre-rendered */}
      <header>This is static</header>

      {/* Dynamic — streaming */}
      <Suspense fallback={<Loading />}>
        <DynamicContent />
      </Suspense>

      {/* Static lagi */}
      <footer>Static footer</footer>
    </div>
  );
}
```
