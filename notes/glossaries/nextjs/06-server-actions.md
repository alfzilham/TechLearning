# Server Actions

## Dasar Server Actions

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `"use server"` | Directive untuk server action | Di file (export) atau inline di komponen |
| Server mutation | Operasi write langsung di server | Form submit, delete, update |
| `revalidatePath()` | Revalidate cache setelah mutasi | `revalidatePath('/products')` |
| `revalidateTag()` | Revalidate cache berdasarkan tag | `revalidateTag('products')` |
| `redirect()` | Redirect setelah action | `redirect('/products')` |

```tsx
// File action — "use server" di file terpisah
// app/actions.ts
"use server";

import { revalidatePath } from 'next/cache';
import { redirect } from 'next/navigation';

export async function createProduct(formData: FormData) {
  const nama = formData.get('nama');
  const harga = formData.get('harga');

  // Validasi
  if (!nama || !harga) {
    throw new Error('Data tidak lengkap');
  }

  // Simpan ke database
  await db.product.create({
    data: { nama, harga: Number(harga) },
  });

  // Revalidate cache
  revalidatePath('/products');

  // Redirect
  redirect('/products');
}
```

---

## Server Action di Form

```tsx
// app/products/new/page.tsx
import { createProduct } from '@/app/actions';

export default function NewProductPage() {
  return (
    <form action={createProduct}>
      <label>Nama Produk</label>
      <input type="text" name="nama" required />

      <label>Harga</label>
      <input type="number" name="harga" required />

      <button type="submit">Simpan</button>
    </form>
  );
}
```

---

## Inline Server Action

```tsx
"use client";
import { useState } from 'react';

export default function LikeButton({ postId }: { postId: number }) {
  const [likes, setLikes] = useState(0);

  // Inline server action
  async function handleLike() {
    const res = await fetch('/api/like', {
      method: 'POST',
      body: JSON.stringify({ postId }),
    });
    const data = await res.json();
    setLikes(data.total);
  }

  return <button onClick={handleLike}>❤️ {likes}</button>;
}
```

---

## useActionState

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useActionState(action, initial)` | Handle form state + error | `const [state, formAction] = useActionState(create, null)` |
| `pending` | Loading state selama action berjalan | `const { pending } = useFormStatus()` |

```tsx
// app/actions.ts
"use server";

export async function updateProfile(prevState: any, formData: FormData) {
  const nama = formData.get('nama') as string;

  if (nama.length < 3) {
    return { error: 'Nama minimal 3 karakter' };
  }

  await db.user.update({ data: { nama } });
  return { success: true };
}

// app/profile/page.tsx
"use client";
import { useActionState } from 'react';
import { updateProfile } from '@/app/actions';

export default function ProfilePage() {
  const [state, formAction, pending] = useActionState(updateProfile, null);

  return (
    <form action={formAction}>
      <input type="text" name="nama" disabled={pending} />
      {state?.error && <p className="error">{state.error}</p>}
      {state?.success && <p className="success">Berhasil disimpan!</p>}
      <button type="submit" disabled={pending}>
        {pending ? 'Menyimpan...' : 'Simpan'}
      </button>
    </form>
  );
}
```

---

## Mutasi dengan Argument Tambahan

```tsx
"use server";

export async function deleteProduct(id: number) {
  // Jangan lupa validasi authorization!
  await db.product.delete({ where: { id } });
  revalidatePath('/products');
}
```

```tsx
// Komponen
import { deleteProduct } from '@/app/actions';

export default function ProductCard({ product }: { product: { id: number; nama: string } }) {
  const deleteWithId = deleteProduct.bind(null, product.id);

  return (
    <div>
      <h3>{product.nama}</h3>
      <form action={deleteWithId}>
        <button type="submit" className="btn-danger">Hapus</button>
      </form>
    </div>
  );
}
```

---

## Best Practices

| Praktik | Penjelasan |
|---------|-----------|
| Validasi data | Selalu validasi di server action |
| Authorization | Cek user role sebelum mutasi |
| Error handling | Return error state, jangan throw |
| `revalidatePath` | Revalidate setelah create/update/delete |
| Loading state | Pakai `useFormStatus()` untuk button loading |
