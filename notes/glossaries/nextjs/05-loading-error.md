# Loading, Error & Not Found

## Loading UI

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `loading.tsx` | Menampilkan loading saat route load | `app/dashboard/loading.tsx` |
| Instant loading | Langsung tampil (tunggu data) | Component stateless |
| Suspense | Streaming per bagian | `<Suspense>` di layout/page |

```tsx
// app/dashboard/loading.tsx — loading untuk /dashboard & child-nya
export default function Loading() {
  return (
    <div className="flex items-center justify-center h-64">
      <div className="animate-spin h-8 w-8 border-4 border-blue-500 rounded-full border-t-transparent" />
      <p className="ml-3">Memuat data...</p>
    </div>
  );
}

// Skeleton loading
export default function Loading() {
  return (
    <div className="space-y-4 p-4">
      <div className="h-8 bg-gray-200 rounded animate-pulse w-1/3" />
      {[1,2,3].map(i => (
        <div key={i} className="h-16 bg-gray-100 rounded animate-pulse" />
      ))}
    </div>
  );
}
```

---

## Streaming dengan Suspense

```tsx
import { Suspense } from 'react';

async function SlowComponent() {
  await new Promise(r => setTimeout(r, 2000));
  return <p>Loaded after 2s</p>;
}

async function FastComponent() {
  return <p>Loaded instantly</p>;
}

export default function Page() {
  return (
    <div>
      <FastComponent />
      <Suspense fallback={<p>Loading slow component...</p>}>
        <SlowComponent />
      </Suspense>
    </div>
  );
}
```

---

## Error UI

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `error.tsx` | Error boundary untuk route | `app/dashboard/error.tsx` |
| `error` object | Berisi `message` dan `digest` | `"use client"` — harus Client Component |
| `reset()` | Function untuk coba lagi | `reset()` → re-render konten |

```tsx
"use client"; // error.tsx HARUS Client Component

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  return (
    <div className="error-container">
      <h2>Terjadi kesalahan!</h2>
      <p className="text-gray-600">{error.message}</p>
      <button
        onClick={() => reset()}
        className="btn btn-primary mt-4"
      >
        Coba Lagi
      </button>
    </div>
  );
}
```

---

## Not Found UI

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `not-found.tsx` | Halaman 404 untuk route | `app/not-found.tsx` |
| `notFound()` | Trigger 404 dari komponen | `import { notFound } from 'next/navigation'` |

```tsx
// app/not-found.tsx — Global 404
export default function NotFound() {
  return (
    <div className="text-center py-20">
      <h1 className="text-6xl font-bold">404</h1>
      <h2 className="text-2xl mt-4">Halaman tidak ditemukan</h2>
      <p className="mt-2">Halaman yang kamu cari tidak ada.</p>
      <a href="/" className="btn btn-primary mt-6">Kembali ke Home</a>
    </div>
  );
}
```

```tsx
// Trigger 404 dari komponen
import { notFound } from 'next/navigation';

export default async function UserPage({ params }: { params: { id: string } }) {
  const res = await fetch(`/api/users/${params.id}`);

  if (!res.ok) {
    notFound(); // → menampilkan not-found.tsx
  }

  const user = await res.json();
  return <div>{user.nama}</div>;
}
```

---

## Kombinasi Lengkap

```tsx
// Struktur folder:
app/
├── dashboard/
│   ├── page.tsx
│   ├── loading.tsx      // Loading skeleton
│   ├── error.tsx        // Error boundary
│   ├── not-found.tsx    // 404 khusus dashboard
│   └── settings/
│       ├── page.tsx
│       └── loading.tsx  // Loading khusus settings
```

Dengan struktur ini:
- **loading.tsx** tampil sementara data di-fetch
- **error.tsx** tampil jika ada error di komponen
- **not-found.tsx** tampil jika `notFound()` dipanggil
- Masing-masing route bisa punya loading/error/not-found sendiri
