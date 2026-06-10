# Server & Client Components

## Server Components (Default)

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Server Component | Semua komponen di App Router adalah Server Component secara default | `export default function Page() { ... }` |
| Keuntungan | Lebih kecil bundle, akses langsung DB, fetch efisien | Langsung `await db.findMany()` |
| Tidak bisa | useState, useEffect, event handlers, browser API | Tidak bisa interaktivitas |
| Async | Server Component bisa `async` | `export default async function Page()` |

```tsx
// Server Component — default, tidak perlu "use client"
async function ProductList() {
  // Langsung fetch di komponen
  const products = await fetch('https://api.example.com/products').then(r => r.json());

  return (
    <ul>
      {products.map(p => (
        <li key={p.id}>
          <h2>{p.nama}</h2>
          <p>Rp{p.harga}</p>
        </li>
      ))}
    </ul>
  );
}

// Bisa juga langsung akses database
import { db } from '@/lib/db';

async function UsersPage() {
  const users = await db.user.findMany();

  return (
    <div>
      {users.map(u => <p key={u.id}>{u.nama}</p>)}
    </div>
  );
}

export default UsersPage;
```

---

## Client Components

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `"use client"` | Directive untuk Client Component | `"use client"; export default function Comp()` |
| Interaktivitas | Bisa pakai hooks, events, browser API | useState, useEffect, onClick |
| Bundle | Termasuk di JavaScript bundle client | — |

```tsx
"use client";
import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(c => c + 1)}>Tambah</button>
    </div>
  );
}
```

---

## Kapan Pakai yang Mana

| Server Component | Client Component |
|-----------------|------------------|
| Fetch data dari API/DB | State (`useState`, `useReducer`) |
| Konten statis | Effects (`useEffect`) |
| SEO penting | Event handlers (`onClick`) |
| Akses backend langsung | Browser API (`localStorage`) |
| Konten tanpa interaktivitas | Form kompleks, real-time UI |

---

## Interleaving Pattern

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Server + Client | Server Component sebagai parent, Client Component sebagai child | Server fetch data → Client render interaktif |

```tsx
// Server Component (parent) — fetch data
import ProductCard from './ProductCard';

export default async function ProductsPage() {
  const products = await fetch('https://api.example.com/products').then(r => r.json());

  return (
    <div>
      {products.map(p => (
        // Client Component (child) — render interaktif
        <ProductCard key={p.id} product={p} />
      ))}
    </div>
  );
}
```

```tsx
// ProductCard.tsx — Client Component
"use client";
import { useState } from 'react';

export default function ProductCard({ product }: { product: { id: number; nama: string; harga: number } }) {
  const [added, setAdded] = useState(false);

  return (
    <div className="card">
      <h3>{product.nama}</h3>
      <p>Rp{product.harga}</p>
      <button onClick={() => setAdded(true)}>
        {added ? '✓ Di Keranjang' : '+ Keranjang'}
      </button>
    </div>
  );
}
```

---

## Passing Data dari Server ke Client

```tsx
// Server Component — kirim data sebagai props
import ClientComp from './ClientComp';

export default async function Page() {
  const data = await fetchData();

  return <ClientComp data={data} />;
}

// Client Component — terima props
"use client";
export default function ClientComp({ data }: { data: DataType }) {
  // data sudah tersedia tanpa fetch client
  return <div>{data.map(...)}</div>;
}
```
