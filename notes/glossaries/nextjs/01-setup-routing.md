# Setup & Routing

## Setup

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `create-next-app` | Membuat project Next.js baru | `npx create-next-app@latest my-app` |
| App Router | Sistem routing baru (Next.js 13+) | `app/` directory |
| Pages Router | Legacy routing (masih support) | `pages/` directory |
| TypeScript | Default TypeScript support | `create-next-app --ts` |
| Tailwind CSS | Default styling option | Included in `create-next-app` |

```bash
# Create Next.js app
npx create-next-app@latest my-app --typescript --tailwind --eslint

# App structure
my-app/
├── app/
│   ├── layout.tsx      # Root layout
│   ├── page.tsx        # Home page (/)
│   └── globals.css     # Global styles
├── public/             # Static assets
├── next.config.js      # Next.js config
└── package.json
```

---

## App Router — Folder-based Routing

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `page.tsx` | File untuk membuat route | `app/about/page.tsx` → `/about` |
| `layout.tsx` | Layout bersama untuk route & child | `app/layout.tsx` |
| `route.ts` | API Route Handler | `app/api/users/route.ts` → `/api/users` |
| Dynamic route `[param]` | Route dengan parameter | `app/users/[id]/page.tsx` → `/users/1` |
| Catch-all `[...slug]` | Tangkap semua segments | `app/blog/[...slug]/page.tsx` |
| Optional catch-all `[[...slug]]` | Catch-all opsional | `app/[[...slug]]/page.tsx` |

```tsx
// app/page.tsx — route: /
export default function Home() {
  return <h1>Home Page</h1>;
}

// app/about/page.tsx — route: /about
export default function About() {
  return <h1>Tentang Kami</h1>;
}

// app/users/[id]/page.tsx — route: /users/1, /users/2
export default function UserDetail({ params }: { params: { id: string } }) {
  return <h1>User: {params.id}</h1>;
}

// app/blog/[...slug]/page.tsx — route: /blog/2024/jan/hello
export default function BlogPost({ params }: { params: { slug: string[] } }) {
  return <h1>Blog: {params.slug.join(' / ')}</h1>;
}
```

---

## File Conventions

| File | Keterangan |
|------|-----------|
| `page.tsx` | Halaman utama route |
| `layout.tsx` | Layout bersama |
| `loading.tsx` | Loading UI (Suspense) |
| `error.tsx` | Error UI |
| `not-found.tsx` | 404 UI |
| `route.ts` | API Route Handler |
| `template.tsx` | Layout yang re-mount setiap navigasi |
| `default.tsx` | Fallback untuk parallel routes |

```tsx
// app/layout.tsx — Root layout (wajib)
export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="id">
      <body>
        <header>Navbar</header>
        <main>{children}</main>
        <footer>Footer</footer>
      </body>
    </html>
  );
}

// app/users/layout.tsx — Layout khusus route /users
export default function UsersLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="users-layout">
      <aside>Sidebar Users</aside>
      <section>{children}</section>
    </div>
  );
}
```
