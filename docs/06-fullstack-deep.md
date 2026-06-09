# Phase 6: Fullstack Deep Dive

**Durasi:** 35 hari (Minggu 12-16)
**Tujuan:** Engineer-grade skills: deployment, security, performance, state management, CI/CD

---

## Minggu 12: Deployment & DevOps

### Hari 1: Vercel Deployment

**Konsep:**
- Deploy ke Vercel dari GitHub
- Environment variables di Vercel dashboard
- Domains kustom (custom domain)
- Preview deployments (setiap PR)
- Analytics & Speed Insights

**Tugas:**
```bash
# Push project ke GitHub
# Connect ke Vercel
# Deploy production
# Setup custom domain (atau .vercel.app)
```

---

### Hari 2: PostgreSQL Production

**Konsep:**
- SQLite hanya untuk development
- Production: PostgreSQL
- Provider: Neon (serverless), Supabase, Railway
- Migration di production: `prisma migrate deploy`
- Connection pooling
- Backup & restore

**Tugas:**
- Setup PostgreSQL di Neon (free tier)
- Update connection string di .env
- Run migration
- Verifikasi data bisa diakses

---

### Hari 3-4: CI/CD dengan GitHub Actions

**Konsep:**
- `.github/workflows/ci.yml`
- Run test otomatis di setiap PR
- Lint check: `next lint`
- Type check: `tsc --noEmit`
- Build check: `npm run build`

**Tugas:**
```yaml
# .github/workflows/ci.yml
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      - run: npm ci
      - run: npm run lint
      - run: npm run typecheck
      - run: npm run test
```

---

### Hari 5: Environment Variables & Secrets

**Konsep:**
- `.env.local` — local development (jangan di-commit)
- `.env.example` — template (wajib di-commit)
- `.env.production` — production overrides
- Jangan commit secrets! Tambahin `.env*.local` di `.gitignore`
- Vercel environment variables

**Tugas:**
- Buat `.env.example` untuk project
- Dokumentasi semua env vars

---

### Hari 6-7: Mini Project — Deploy Fullstack App

Deploy capstone project ke production:
- Vercel + Neon PostgreSQL
- CI/CD pipeline
- Custom domain
- Environment variables terkelola
- Lighthouse score > 90

---

## Minggu 13: Security

### Hari 8-9: Web Security Fundamentals

**Konsep:**
- **XSS (Cross-Site Scripting)**: jangan `dangerouslySetInnerHTML` di React kalo ga perlu
- **CSRF (Cross-Site Request Forgery)**: Next.js Server Actions otomatis proteksi
- **SQL Injection**: Prisma otomatis prevent (parameterized queries)
- **Rate Limiting**: proteksi API dari spam
- **Helmet**: security headers
- **Input sanitization**: selalu validasi & sanitasi input user

**Tugas:**
```tsx
// 1. Implementasi rate limiting di API route
// 2. Security headers di next.config.js
// 3. Input sanitasi: strip HTML tags dari input user
```

---

### Hari 10-11: Auth Security

**Konsep:**
- Session vs JWT — kapan pake yang mana
- CSRF token untuk form
- Brute force protection (rate limit login)
- Email verification (opsional)
- Password policy
- 2FA (Google Authenticator)

**Tugas:**
- Rate limiter di route login
- Password strength checker
- Session timeout/expiry

---

### Hari 12: Data Protection & Privacy

**Konsep:**
- GDPR basics
- Jangan log password atau sensitive data
- Data encryption at rest
- Input validation sebagai lapisan keamanan pertama
- Prisma field: `@@map`, `@map` untuk keamanan

---

## Minggu 14: Performance & State Management

### Hari 13-14: Advanced Performance

**Konsep:**
- React.memo — kapan berguna, kapan tidak
- `useMemo` & `useCallback` patterns
- Bundle splitting: dynamic import
- Image optimization strategies
- Font optimization: `next/font`
- Caching strategies: `stale-while-revalidate`
- Streaming & Suspense patterns
- Web Vitals: LCP, FID, CLS

**Tugas:**
- Audit current project dengan Lighthouse
- Fix 3 performance issues
- Implementasi image lazy loading
- Analisis bundle size dengan `@next/bundle-analyzer`

---

### Hari 15-16: State Management Lanjutan

**Konsep:**
- React Context + useReducer pattern
- Zustand: lightweight state management
- TanStack Query (React Query): server state management
- Kapan pake:
  - **Local state**: useState (komponen sendiri)
  - **Global client state**: Zustand / Context (theme, auth)
  - **Server state**: TanStack Query (data dari API)
  - **URL state**: useSearchParams (filter, search query)

**Tugas:**
```tsx
// Implementasi Zustand untuk cart state
// Implementasi TanStack Query untuk fetching data
```

---

### Hari 17: Architecture Patterns

**Konsep:**
- **Presentation / Container pattern** — pisahkan logic dari UI
- **Compound component pattern** — komponen fleksibel
- **Render props** vs **Hooks**
- **Singleton pattern** untuk service
- **Repository pattern** untuk database access

**Tugas:**
Refactor project dengan repository pattern:
```tsx
// Buat layer: service layer
// src/lib/services/post-service.ts
// src/lib/repositories/post-repository.ts
// Komponen hanya panggil service
```

---

## Minggu 15: Advanced Topics

### Hari 18-19: i18n (Internationalization)

**Konsep:**
- `next-intl` atau `i18next`
- Middleware untuk deteksi bahasa
- Translation files (`en.json`, `id.json`)
- Dynamic content translation

**Tugas:**
- Setup i18n di project
- English + Indonesia
- Language switcher

---

### Hari 20-21: File Upload

**Konsep:**
- Upload dengan Server Actions
- Upload ke Vercel Blob / AWS S3 / Uploadthing
- Image optimization setelah upload
- Validation: file type, size limit

**Tugas:**
- Upload gambar profile user
- Upload image untuk post thumbnail
- Preview sebelum upload

---

### Hari 22: WebSocket & Real-time

**Konsep:**
- WebSocket basics
- Server-Sent Events (SSE)
- Polling vs WebSocket vs SSE
- Pusher / Ably / Socket.io (kapan butuh)
- Next.js Route Handler untuk SSE

**Tugas:**
- Live notification
- Real-time counter

---

### Hari 23-24: Search Engine Optimization

**Konsep:**
- Metadata API (dalam)
- Open Graph & Twitter Cards
- JSON-LD structured data
- Sitemap generation: `app/sitemap.ts`
- robots.txt: `app/robots.ts`
- Core Web Vitals
- SSR untuk SEO (yang Next.js sudah handle)

**Tugas:**
- Generate sitemap dinamis
- JSON-LD untuk blog post
- Optimasi Core Web Vitals

---

### Hari 25: Error Monitoring & Logging

**Konsep:**
- Sentry setup untuk Next.js
- Error logging di server action
- Client-side error tracking
- Log levels: debug, info, warn, error
- Structured logging

---

## Minggu 16: Engineer Readiness

### Hari 26-27: Code Review Skills

**Apa yang dicari dalam code review:**
1. **Functionality** — Apakah kode berfungsi seperti yang diharapkan?
2. **Edge cases** — Apa yang terjadi kalo input kosong/null/undefined?
3. **Error handling** — Apakah error ditangani dengan baik?
4. **Performance** — Apakah ada bottleneck?
5. **Security** — Apakah ada celah keamanan?
6. **Readability** — Apakah kode mudah dibaca?
7. **Consistency** — Apakah mengikuti pattern yang sudah ada?

**Tugas:**
Review code dari project sebelumnya dengan checklist di atas.

---

### Hari 28: Testing Deep Dive

**Konsep:**
- Unit test: vitest + testing-library
- Integration test: test component + API
- E2E test: Playwright
- Coverage: `vitest run --coverage`
- Test pyramid:

```
      ╱ E2E ╲         ← sedikit, mahal, coverage luas
     ╱ Integration ╲   ← medium
    ╱   Unit Test   ╲  ← banyak, cepat, coverage detail
```

**Tugas:**
Tambah test coverage sampai > 70%.

---

### Hari 29: Open Source Contribution

**Cara berkontribusi ke open source:**
1. Cari issue labeled `good first issue` di repositori Next.js, Prisma, atau library yang dipakai
2. Baca CONTRIBUTING.md
3. Fork → branch → fix → PR
4. Jangan takut ditolak — itu proses belajar

**Tugas:**
Cari 3 issue yang bisa dikerjakan (tidak harus dikerjakan sekarang, cukup riset).

---

### Hari 30: Build Portfolio

Buat website portfolio dengan (gunakan Next.js):
1. About me
2. Projects (dengan link live + GitHub)
3. Skills
4. Blog
5. Contact form (server action)
6. Deploy ke Vercel

Ini akan jadi **wajah profesional** Anda sebagai software engineer.

---

### Hari 31-32: Mock Interview

**Technical questions yang harus bisa dijawab:**
1. "Apa perbedaan server component dan client component?"
2. "Bagaimana cara kerja React reconciliation?"
3. "Jelaskan Virtual DOM"
4. "Apa itu closure? Beri contoh"
5. "Bagaimana cara optimasi performa di Next.js?"
6. "Apa perbedaan useState dan useReducer?"
7. "Jelaskan cara kerja authentication flow di aplikasi Next.js"
8. "Bagaimana cara mengamankan API dari serangan?"

**Coding challenge:**
Buat function sederhana di whiteboard (atau editor tanpa auto-complete):
- Fibonacci sequence
- Palindrome check
- Array unique
- Debounce function

---

### Hari 33-35: Final Portfolio Review & Career

1. Review portfolio website
2. Setup LinkedIn profile
3. Buat CV yang highlight skill dan project
4. Setup GitHub profile dengan README
5. Planning next steps: apa yang ingin dipelajari selanjutnya

---

## Referensi

- [Vercel Docs](https://vercel.com/docs)
- [Neon PostgreSQL](https://neon.tech/docs)
- [GitHub Actions Docs](https://docs.github.com/en/actions)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [Web.dev](https://web.dev/learn/)
- [Zustand](https://github.com/pmndrs/zustand)
- [TanStack Query](https://tanstack.com/query/latest)
- [Sentry](https://docs.sentry.io/platforms/javascript/guides/nextjs/)
