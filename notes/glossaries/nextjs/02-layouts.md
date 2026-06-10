# Layouts

## Root Layout

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Root layout | Layout paling atas — wajib ada | `app/layout.tsx` |
| `<html>` & `<body>` | Hanya di root layout | Semua layout child tidak perlu HTML tag |
| `{children}` | Konten halaman atau layout child | `<main>{children}</main>` |

```tsx
// app/layout.tsx — Root layout
import type { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'My App',
  description: 'My Next.js application',
};

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="id">
      <body>
        <nav>{/* Navbar — ada di semua halaman */}</nav>
        <main>{children}</main>
        <footer>{/* Footer — ada di semua halaman */}</footer>
      </body>
    </html>
  );
}
```

---

## Nested Layouts

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Nested layout | Layout khusus untuk segmen route | `app/dashboard/layout.tsx` |
| Layout stacking | Child layout di-render di dalam parent layout | Root → Dashboard → Settings |
| Persist | Layout tetap mount saat navigasi antar child | Sidebar tidak re-render |

```tsx
// app/dashboard/layout.tsx
export default function DashboardLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="dashboard-layout">
      <aside>{/* Sidebar — tetap saat navigasi */}</aside>
      <section>{children}</section>
    </div>
  );
}

// app/dashboard/settings/layout.tsx — bisa nested lagi
export default function SettingsLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="settings-layout">
      <nav>{/* Tab settings */}</nav>
      {children}
    </div>
  );
}
```

---

## Template vs Layout

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `layout.tsx` | Persist (tidak re-mount saat navigasi) | Sidebar, navbar |
| `template.tsx` | Re-mount setiap navigasi | Analytics tracking, form state reset |

```tsx
// app/dashboard/template.tsx — selalu re-mount
export default function Template({ children }: { children: React.ReactNode }) {
  useEffect(() => {
    console.log('Page viewed');
    // Analytics page view
  }, []);

  return <div className="template">{children}</div>;
}
```

---

## Route Groups `()`

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `(group)` | Mengelompokkan route tanpa mempengaruhi URL | `(marketing)` dan `(dashboard)` |
| Organize | Memisahkan layout berbeda dalam satu level | `/`, `/about` pakai layout A, `/dashboard` pakai layout B |

```tsx
// Struktur folder:
app/
├── (marketing)/
│   ├── layout.tsx        // Layout khusus marketing
│   ├── page.tsx          // /
│   └── about/
│       └── page.tsx      // /about
├── (dashboard)/
│   ├── layout.tsx        // Layout khusus dashboard
│   └── dashboard/
│       └── page.tsx      // /dashboard

// app/(marketing)/layout.tsx
export default function MarketingLayout({ children }: { children: React.ReactNode }) {
  return (
    <div>
      <header>Marketing Header</header>
      {children}
    </div>
  );
}
```

---

## Parallel Routes `@folder`

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `@slot` | Render multiple halaman dalam satu layout | `@feed` dan `@sidebar` |
| `default.tsx` | Fallback jika slot tidak punya halaman untuk route | `app/@sidebar/default.tsx` |

```tsx
// app/layout.tsx — parallel routes
export default function Layout({
  children,
  feed,
  sidebar,
}: {
  children: React.ReactNode;
  feed: React.ReactNode;
  sidebar: React.ReactNode;
}) {
  return (
    <div className="flex">
      <main>{children}</main>
      <aside>{sidebar}</aside>
      <section>{feed}</section>
    </div>
  );
}

// Struktur:
app/
├── layout.tsx
├── page.tsx
├── @sidebar/
│   ├── default.tsx        // Fallback sidebar
│   └── settings/
│       └── page.tsx
└── @feed/
    └── page.tsx
```
