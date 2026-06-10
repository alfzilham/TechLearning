# Data Fetching

## Server-side Fetching

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `fetch()` di Server Component | Fetch langsung, tanpa useEffect | `const data = await fetch(url)` |
| `cache: 'force-cache'` | Cache default (static) | `fetch(url, { cache: 'force-cache' })` |
| `cache: 'no-store'` | Selalu fresh (dynamic) | `fetch(url, { cache: 'no-store' })` |
| `next: { revalidate: 60 }` | ISR — revalidate setiap 60 detik | `fetch(url, { next: { revalidate: 60 } })` |
| `next: { tags: ['products'] }` | Tag untuk revalidateTag | `fetch(url, { next: { tags: ['products'] } })` |

```tsx
// Static — cache selamanya (default)
async function StaticPage() {
  const data = await fetch('https://api.example.com/posts');
  const posts = await data.json();

  return <div>{posts.map(...)}</div>;
}

// Dynamic — selalu fresh
async function DynamicPage() {
  const data = await fetch('https://api.example.com/stock', {
    cache: 'no-store',
  });
  const stock = await data.json();
  return <div>Harga: {stock.price}</div>;
}

// ISR — revalidate setiap 60 detik
async function BlogPage() {
  const data = await fetch('https://api.example.com/blog', {
    next: { revalidate: 60 },
  });
  const posts = await data.json();
  return <div>{posts.map(...)}</div>;
}
```

---

## Parallel Fetching

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `Promise.all()` | Fetch multiple data paralel | `const [a, b] = await Promise.all([f1(), f2()])` |

```tsx
// Parallel — lebih cepat dari sequential
export default async function Dashboard() {
  const [user, orders, products] = await Promise.all([
    fetch('/api/user').then(r => r.json()),
    fetch('/api/orders').then(r => r.json()),
    fetch('/api/products').then(r => r.json()),
  ]);

  return (
    <div>
      <h1>Welcome {user.nama}</h1>
      <p>Orders: {orders.length}</p>
      <p>Products: {products.length}</p>
    </div>
  );
}
```

---

## generateMetadata

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `generateMetadata` | Dynamic SEO metadata berdasarkan data | `export async function generateMetadata({ params })` |

```tsx
import type { Metadata } from 'next';

// Static metadata
export const metadata: Metadata = {
  title: 'About Us',
  description: 'Tentang perusahaan kami',
};

// Dynamic metadata
export async function generateMetadata({ params }: { params: { id: string } }): Promise<Metadata> {
  const product = await fetch(`https://api.example.com/products/${params.id}`).then(r => r.json());

  return {
    title: product.nama,
    description: product.deskripsi,
    openGraph: {
      images: [product.image],
    },
  };
}

export default async function ProductPage({ params }: { params: { id: string } }) {
  const product = await fetch(`https://api.example.com/products/${params.id}`).then(r => r.json());

  return (
    <div>
      <h1>{product.nama}</h1>
      <p>{product.deskripsi}</p>
    </div>
  );
}
```

---

## Client-side Fetching

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useEffect` + fetch | Client-side fetching tradisional | `useEffect(() => { fetch() }, [])` |
| TanStack Query | Library untuk client fetching | `useQuery({ queryKey, queryFn })` |
| SWR | Lightweight fetching library | `useSWR('/api/user')` |

```tsx
"use client";
import { useState, useEffect } from 'react';

export default function ClientProducts() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch('/api/products')
      .then(r => r.json())
      .then(data => { setProducts(data); setLoading(false); });
  }, []);

  if (loading) return <p>Loading...</p>;
  return <div>{products.map(...)}</div>;
}
```
