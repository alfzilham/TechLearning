# Phase 5: Next.js 15

**Durasi:** 28 hari (Minggu 8-11)
**Tujuan:** Fullstack application dengan App Router, Database, dan Authentication

---

## Kenapa Next.js?

React hanya library untuk UI. Next.js adalah **framework** yang memberi struktur lengkap: routing, data fetching, rendering (SSR/SSG), API routes, optimasi gambar, middleware, dan banyak lagi. Dengan Next.js, satu codebase bisa handle frontend dan backend.

---

## Minggu 8: Next.js Dasar

### Hari 1: Setup & App Router

**Konsep:**
- `npx create-next-app@latest` — setup dengan TypeScript, Tailwind, ESLint, App Router
- Struktur folder `app/`
- File-based routing:
  - `app/page.tsx` → `/`
  - `app/about/page.tsx` → `/about`
  - `app/blog/[slug]/page.tsx` → `/blog/hello-world`
- `layout.tsx` — layout yang membungkus halaman
- `loading.tsx` — loading state (Suspense otomatis)
- `error.tsx` — error boundary
- `not-found.tsx` — 404 page

**Tugas:**
```tsx
// Buat project Next.js baru
// Bikin halaman: /, /about, /contact
// Layout dengan navbar + footer
// loading.tsx untuk setiap halaman
// not-found.tsx kustom
```

---

### Hari 2: Server Components vs Client Components

**Konsep:**
- Semua komponen di Next.js **server component** secara default
- Server Component: render di server, tidak punya interaktivitas, bisa `async`
- Client Component: perlu `'use client'`, punya hooks, event handlers, browser API
- **Server Component** bisa:
  - Akses database langsung
  - Baca file
  - Tidak mengirim JS ke client
- **Client Component** bisa:
  - useState, useEffect, event handlers
  - Browser API (localStorage, dll)
  - Tapi: lebih berat, lebih banyak JS

**Aturan Praktis:**
```
Bisa server component? → Server Component
Butuh interaktivitas?   → Client Component (serendah mungkin di pohon komponen)
```

**Tugas:**
```tsx
// 1. Buat halaman /users yang fetch data di Server Component (async component)
// 2. Buat SearchBar sebagai Client Component
// 3. Paham "lifting client boundary" — taruh 'use client' di komponen terkecil
```

---

### Hari 3: Data Fetching — Server Side

**Konsep:**
- `async` component: langsung `await fetch()` di komponen
- Caching: `fetch()` otomatis di-cache (DEFAULT)
- Revalidation:
  - Time-based: `next: { revalidate: 3600 }` — re-render setiap 1 jam
  - On-demand: `revalidatePath()` atau `revalidateTag()`
- `generateStaticParams()` — static page generation
- `generateMetadata()` — SEO tiap halaman

**Tugas:**
```tsx
// 1. Halaman /blog dengan daftar post (fetch dari API)
// 2. Halaman /blog/[slug] dengan generateStaticParams
// 3. generateMetadata untuk SEO title + description
// 4. ISR: revalidate setiap 60 detik
```

---

### Hari 4: Client-Side Data Fetching

**Konsep:**
- Client component + `useEffect` + fetch (seperti React biasa)
- `use()` hook di React 19 untuk unwrap Promise
- SWR / TanStack Query (opsional — untuk caching client)
- Server Action vs Client fetch — kapan pake yang mana

**Tugas:**
```tsx
// 1. Buat halaman /dashboard yang fetch data real-time
// 2. Search bar dengan debounce (client-side fetch)
// 3. Infinite scroll / load more
```

---

### Hari 5: Server Actions

**Konsep:**
- `'use server'` — function yang jalan di server tapi bisa dipanggil dari client
- `form action={serverAction}` — form submission tanpa JavaScript
- `useActionState()` — hook untuk mengelola state server action
- Revalidasi setelah action: `revalidatePath()`
- Error handling di server action
- Loading state dengan `useActionState()` pending

**Tugas:**
```tsx
// 1. Form kontak dengan server action
// 2. validasi input di server
// 3. Tampilkan pesan sukses/error
// 4. Redirect setelah submit
```

---

### Hari 6: API Routes (Route Handlers)

**Konsep:**
- `app/api/route.ts` → `GET`, `POST`, `PUT`, `DELETE`
- `export async function GET(request: NextRequest)`
- `NextRequest`, `NextResponse`
- Request body: `request.json()`
- Search params: `request.nextUrl.searchParams`
- CORS headers kalo perlu

**Tugas:**
```tsx
// Buat API endpoints:
// GET /api/posts → daftar posts
// GET /api/posts/[id] → detail post
// POST /api/contact → simpan pesan kontak
// Test dengan Postman atau fetch dari browser
```

---

### Hari 7: Mini Project Week 1 — Blog Sederhana

Buat blog sederhana dengan:
1. **Halaman utama** — daftar artikel (fetch di server component)
2. **Detail artikel** — `/blog/[slug]` dengan metadata
3. **Form kontak** — server action
4. **API route** — untuk akses data dari luar
5. **Loading & Error states** — di setiap halaman
6. **Responsive** dengan Tailwind

---

## Minggu 9: Database & ORM

### Hari 8: Database Setup & Prisma

**Konsep:**
- Prisma: ORM untuk TypeScript
- `npx prisma init`
- Schema: `datasource`, `generator`, `model`
- Migration: `npx prisma migrate dev`
- Studio: `npx prisma studio`
- CRUD dengan Prisma Client

**Setup:**
```bash
npm install prisma @prisma/client
npx prisma init
```

**Schema dasar:**
```prisma
model Post {
  id        String   @id @default(cuid())
  title     String
  content   String
  slug      String   @unique
  published Boolean  @default(false)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

**Tugas:**
```tsx
// 1. Setup Prisma + SQLite (biar gampang, no need PostgreSQL dulu)
// 2. Buat model Post
// 3. Seed data: 5 post
// 4. Buat halaman yang render posts dari database
```

---

### Hari 9: CRUD dengan Prisma + Server Actions

**Konsep:**
- Prisma queries: `create`, `findMany`, `findUnique`, `update`, `delete`
- Pagination: `skip`, `take`
- Filter: `where`, `orderBy`
- Relation: `include`, `select`

**Tugas:**
```tsx
// Buat full CRUD posts:
// - Halaman daftar post (read)
// - Form create post (server action + prisma create)
// - Edit page (server action + prisma update)
// - Delete button (server action + prisma delete)
// - Validasi dengan Zod
```

---

### Hari 10: Models & Relations

**Konsep:**
- Relasi: one-to-many, many-to-many, one-to-one
- Relational queries: `include`, `where` dengan relation filter

**Schema:**
```prisma
model User {
  id    String  @id @default(cuid())
  name  String
  email String  @unique
  posts Post[]
}

model Post {
  id      String   @id @default(cuid())
  title   String
  content String
  author  User     @relation(fields: [authorId], references: [id])
  authorId String
  tags    TagOnPost[]
}

model Tag {
  id    String      @id @default(cuid())
  name  String      @unique
  posts TagOnPost[]
}

model TagOnPost {
  post   Post   @relation(fields: [postId], references: [id])
  postId String
  tag    Tag    @relation(fields: [tagId], references: [id])
  tagId  String

  @@id([postId, tagId])
}
```

**Tugas:**
- Tambah model User, Tag ke blog
- Buat halaman post dengan author info
- Filter post berdasarkan tag

---

### Hari 11: Validation dengan Zod

**Konsep:**
- `npm install zod`
- Schema validation: `z.string().min(3).max(100)`
- Parse: `schema.parse(data)` — throw error kalo invalid
- Safe parse: `schema.safeParse(data)` — return result object
- Integrasi dengan form server action

**Tugas:**
```tsx
const postSchema = z.object({
  title: z.string().min(3, 'Judul minimal 3 karakter').max(100),
  content: z.string().min(10, 'Konten minimal 10 karakter'),
  slug: z.string().regex(/^[a-z0-9-]+$/, 'Slug hanya boleh huruf kecil, angka, dan strip'),
});

// Implementasi di server action create post
// Tampilkan error balik ke form
```

---

### Hari 12: Mini Project Minggu 9 — Blog dengan Database

Blog yang sudah connect ke database:
1. CRUD posts lengkap
2. User sebagai author
3. Tags untuk kategori
4. Validasi Zod
5. Pagination (10 post per halaman)
6. Search post by title

---

## Minggu 10: Authentication

### Hari 13: Auth Dasar — NextAuth.js / Auth.js

**Konsep:**
- `npm install next-auth@beta` (Auth.js v5)
- `auth.ts` — konfigurasi auth
- Providers: Credentials (email/password), Google, GitHub
- `auth()` — server function untuk cek session
- `useSession()` — client hook
- `signIn()`, `signOut()`

**Tugas:**
```tsx
// 1. Setup NextAuth.js dengan Credentials provider
// 2. Halaman login
// 3. Protected route: redirect ke /login kalo belum auth
// 4. Tampilkan user info di navbar
// 5. Logout button
```

---

### Hari 14: Register & Password Hashing

**Konsep:**
- `bcryptjs` untuk hash password
- `hash(password, saltRounds)` — simpan hashed password di database
- `compare(password, hashed)` — verifikasi login
- Jangan pernah simpan plain text password

**Tugas:**
```tsx
// 1. Halaman register: name, email, password
// 2. Validasi: email unique, password minimal 8 char
// 3. Hash password dengan bcryptjs
// 4. Simpan user ke database
// 5. Login dengan email + password yang sudah dihash
```

---

### Hari 15: Middleware & Protected Routes

**Konsep:**
- `middleware.ts` di root project
- `NextResponse.next()`, `NextResponse.redirect()`
- `export { default } from "next-auth/middleware"` — Auth.js built-in
- Atau middleware kustom: `export function middleware(request)`

**Tugas:**
```tsx
// 1. middleware.ts yang protect /dashboard dan /admin
// 2. Redirect ke /login jika belum auth
// 3. Role-based: hanya admin bisa akses /admin
// 4. Public routes: /, /blog, /about — tidak perlu auth
```

---

### Hari 16: User Profile & Settings

**Tugas:**
```tsx
// 1. Halaman /profile — tampilkan user info
// 2. Edit profile: name, bio, avatar
// 3. Change password form
// 4. Delete account (dengan konfirmasi)
```

---

### Hari 17-20: Capstone Project (Bagian 1)

Mulai project akhir: **Fullstack Application with Auth**.

Ide project (pilih salah satu atau buat sendiri):
1. **Task Manager** — project management dengan team
2. **E-commerce Mini** — produk, cart, order
3. **Forum / Q&A** — pertanyaan, jawaban, vote
4. **Booking System** — jadwal, reservasi

**Minimum requirements:**
- Authentication (register, login, logout)
- Protected routes
- CRUD dengan database
- Server Actions untuk mutation
- Validasi Zod
- Responsive UI
- 3+ models dengan relasi

---

## Minggu 11: Advanced Next.js

### Hari 21: Middleware, Cookies & Headers

**Konsep:**
- `cookies()` — baca/set cookie di server component
- `headers()` — baca request headers
- Middleware untuk: i18n, A/B testing, redirect based on country
- `next/headers` vs `next/navigation`

---

### Hari 22: Image Optimization & Metadata

**Konsep:**
- `next/image`: `Image` component dengan lazy loading, responsive, WebP
- Remote images: tambah domain di `next.config.js`
- Metadata API: `generateMetadata`, `metadata` export
- Open Graph: `og:image`, `og:title`, `og:description`
- Dynamic metadata berdasarkan params

---

### Hari 23: Performance Optimization

**Konsep:**
- Lighthouse audit
- Bundle analyzer: `@next/bundle-analyzer`
- Dynamic import: `next/dynamic`
- Streaming: `loading.tsx` + Suspense boundaries
- `useMemo` & `useCallback` di client components
- Image optimization sudah otomatis dengan `next/image`
- `next.config.js`: `images.remotePatterns`, `experimental`

---

### Hari 24: Error Handling & Logging

**Konsep:**
- `error.tsx` — error boundary per segment
- `global-error.tsx` — untuk root layout
- Error logging (console.error di server action, dll)
- Sentry setup (opsional)
- Toast notification untuk user feedback

---

### Hari 25: Testing — Unit Test

**Konsep:**
- `npm install vitest @testing-library/react @testing-library/jest-dom`
- `vitest.config.ts`
- Test komponen: render, fire event, assert
- Test server action: mock database
- Test utility functions

**Tugas:**
```tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { describe, it, expect } from 'vitest';

// Test komponen Card, Button, Form
// Test utility functions
```

---

### Hari 26: Testing — E2E dengan Playwright

**Konsep:**
- `npm init playwright`
- E2E test: user flow lengkap
- Test: register → login → create post → edit → delete

**Tugas:**
```tsx
// Playwright test:
// 1. Buka halaman utama
// 2. Klik login → isi form → submit
// 3. Verifikasi redirect ke dashboard
```

---

### Hari 27-28: Capstone Project (Bagian 2) + Final Review

Selesaikan capstone project dengan:
- Testing (minimal 3 unit test + 2 E2E test)
- Error handling di semua level
- SEO metadata
- Performance audit > 90 di Lighthouse

---

## Referensi

- [Next.js Docs](https://nextjs.org/docs)
- [Prisma Docs](https://www.prisma.io/docs)
- [Auth.js](https://authjs.dev/)
- [Zod](https://zod.dev/)
- [Vitest](https://vitest.dev/)
- [Playwright](https://playwright.dev/)

## Checklist Penguasaan

Sebelum lanjut ke Fullstack Deep, pastikan bisa:
- [ ] Setup Next.js project dengan App Router
- [ ] Paham Server Component vs Client Component
- [ ] Data fetching: server side + client side
- [ ] Server Actions untuk form handling
- [ ] API Routes (Route Handlers)
- [ ] Database dengan Prisma ORM
- [ ] CRUD operations dengan database
- [ ] Authentication dengan Auth.js
- [ ] Middleware untuk protected routes
- [ ] Validasi input dengan Zod
- [ ] Image optimization & metadata
- [ ] Unit test + E2E test
