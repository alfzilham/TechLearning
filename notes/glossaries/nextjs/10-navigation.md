# Navigation

## Link Component

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `<Link>` | Client-side navigation | `<Link href="/about">Tentang</Link>` |
| `prefetch` | Prefetch halaman (default) | `prefetch={false}` untuk non-aktifkan |
| `replace` | Ganti history, bukan push | `<Link href="/" replace />` |
| `scroll` | Scroll ke top setelah navigasi | `scroll={false}` |

```tsx
import Link from 'next/link';

export default function Navbar() {
  return (
    <nav>
      <Link href="/" className="nav-link">Home</Link>
      <Link href="/about">Tentang</Link>
      <Link href="/products" prefetch={false}>Produk</Link>
      <Link href="/contact" replace>Kontak</Link>

      {/* Dynamic link */}
      <Link href={`/products/${product.id}`}>
        {product.nama}
      </Link>

      {/* Link dengan query params */}
      <Link href={{
        pathname: '/products',
        query: { category: 'electronics', page: 1 },
      }}>
        Elektronik
      </Link>
    </nav>
  );
}
```

---

## useRouter

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useRouter()` | Router hook untuk Client Component | `const router = useRouter()` |
| `router.push()` | Navigasi ke route | `router.push('/dashboard')` |
| `router.replace()` | Navigasi tanpa tambah history | `router.replace('/login')` |
| `router.back()` | Kembali | `router.back()` |
| `router.refresh()` | Refresh halaman tanpa reload | `router.refresh()` |
| `router.prefetch()` | Prefetch route | `router.prefetch('/about')` |

```tsx
"use client";
import { useRouter } from 'next/navigation';

export default function NavigationButtons() {
  const router = useRouter();

  return (
    <div className="space-x-4">
      <button onClick={() => router.push('/dashboard')}>
        Ke Dashboard
      </button>

      <button onClick={() => router.replace('/login')}>
        Login (ganti history)
      </button>

      <button onClick={() => router.back()}>
        Kembali
      </button>

      <button onClick={() => router.refresh()}>
        Refresh Data
      </button>

      <button onClick={() => router.prefetch('/about')}>
        Prefetch About
      </button>
    </div>
  );
}
```

---

## usePathname & useSearchParams

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `usePathname()` | Pathname saat ini | `/blog/my-post` |
| `useSearchParams()` | Query string params | `{ page: '2', q: 'react' }` |
| `useParams()` | Dynamic route params | `{ id: '123' }` |

```tsx
"use client";
import { usePathname, useSearchParams, useParams } from 'next/navigation';

// Active link detector
function NavLink({ href, children }: { href: string; children: React.ReactNode }) {
  const pathname = usePathname();
  const isActive = pathname === href || pathname.startsWith(href + '/');

  return (
    <Link href={href} className={isActive ? 'active' : ''}>
      {children}
    </Link>
  );
}

// Search params — filter produk
function ProductFilter() {
  const searchParams = useSearchParams();
  const pathname = usePathname();
  const router = useRouter();

  const category = searchParams.get('category') || 'all';
  const page = Number(searchParams.get('page') || '1');

  const setFilter = (key: string, value: string) => {
    const params = new URLSearchParams(searchParams.toString());
    params.set(key, value);
    params.set('page', '1'); // reset page
    router.push(`${pathname}?${params.toString()}`);
  };

  return (
    <div>
      <button onClick={() => setFilter('category', 'electronics')}>
        Elektronik
      </button>
      <p>Halaman: {page}</p>
    </div>
  );
}

// useParams — dynamic route
function UserPage() {
  const params = useParams<{ id: string }>();
  return <h1>User ID: {params.id}</h1>;
}
```

---

## redirect & permanentRedirect

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `redirect(path)` | Redirect (307) — Server Component | `import { redirect } from 'next/navigation'` |
| `permanentRedirect(path)` | Redirect permanen (308) | `import { permanentRedirect } from 'next/navigation'` |

```tsx
import { redirect, permanentRedirect } from 'next/navigation';

// Server Component redirect
export default async function OldPage() {
  redirect('/new-page');
}

// Conditional redirect
export default async function Profile({ params }: { params: { id: string } }) {
  const user = await getUser(params.id);

  if (!user) {
    redirect('/users');
  }

  if (user.role !== 'admin') {
    redirect('/dashboard');
  }

  return <div>{user.nama}</div>;
}

// Permanen redirect
export default function OldBlog() {
  permanentRedirect('/blog');
}
```
