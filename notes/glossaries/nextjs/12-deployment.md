# Deployment & Config

## Vercel Deploy

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Vercel deploy | Deploy otomatis dari Git | Push ke main → auto deploy |
| Environment variables | `process.env` di dashboard Vercel | `SECRET_KEY` di project settings |
| Preview deployments | Setiap PR punya URL preview | `my-app-git-feature.vercel.app` |
| Analytics | Web Vitals, speed insights | Enable di dashboard |
| Cron Jobs | Scheduled serverless functions | `vercel.json` → `crons` |

```bash
# Deploy via Vercel CLI
npm i -g vercel
vercel          # Deploy to preview
vercel --prod   # Deploy to production

# Or connect GitHub repo to Vercel
# 1. Push to GitHub
# 2. Import repo di vercel.com
# 3. Auto deploy on push
```

---

## Environment Variables

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `.env.local` | Local development (jangan di-commit) | `DATABASE_URL=...` |
| `.env` | Default values (bisa di-commit) | `NEXT_PUBLIC_URL=http://localhost:3000` |
| `NEXT_PUBLIC_` | Prefix untuk client-side env | `NEXT_PUBLIC_API_KEY=...` |
| Vercel dashboard | Production env vars | Settings → Environment Variables |

```env
# .env.local
DATABASE_URL=postgresql://user:pass@localhost:5432/mydb
AUTH_SECRET=my-secret-key
GITHUB_ID=abc123
GITHUB_SECRET=def456

# NEXT_PUBLIC_ — bisa diakses di client
NEXT_PUBLIC_API_URL=https://api.example.com
```

```tsx
// Akses environment variables
// Server Component
const dbUrl = process.env.DATABASE_URL;

// Client Component (hanya NEXT_PUBLIC_)
"use client";
const apiUrl = process.env.NEXT_PUBLIC_API_URL;
```

---

## next.config.js

```js
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  // Image optimization
  images: {
    remotePatterns: [
      { protocol: 'https', hostname: 'images.unsplash.com' },
    ],
  },

  // Redirects
  async redirects() {
    return [
      { source: '/old-page', destination: '/new-page', permanent: true },
      { source: '/blog/:slug', destination: '/posts/:slug', permanent: true },
    ];
  },

  // Headers (security, CORS)
  async headers() {
    return [
      {
        source: '/api/:path*',
        headers: [
          { key: 'Access-Control-Allow-Origin', value: '*' },
        ],
      },
    ];
  },

  // Bundle analyzer
  productionBrowserSourceMaps: false,

  // Standalone output (Docker)
  output: 'standalone',
};

module.exports = nextConfig;
```

---

## ISR (Incremental Static Regeneration)

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `revalidate` | Auto re-generate halaman statis | `fetch(url, { next: { revalidate: 60 } })` |
| `on-demand` | Manual revalidate via API | `revalidatePath()` atau `revalidateTag()` |

```tsx
// On-demand revalidation API
// app/api/revalidate/route.ts
import { revalidatePath, revalidateTag } from 'next/cache';
import { NextRequest, NextResponse } from 'next/server';

export async function POST(request: NextRequest) {
  const secret = request.headers.get('x-revalidate-secret');

  if (secret !== process.env.REVALIDATE_SECRET) {
    return NextResponse.json({ error: 'Unauthorized' }, { status: 401 });
  }

  // Revalidate specific path
  revalidatePath('/products');

  // Revalidate by tag
  revalidateTag('products');

  return NextResponse.json({ revalidated: true });
}
```

---

## Standalone Output (Docker)

```js
// next.config.js
module.exports = {
  output: 'standalone',
};
```

```dockerfile
# Dockerfile
FROM node:20-alpine AS base
FROM base AS deps
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci

FROM base AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run build

FROM base AS runner
WORKDIR /app
ENV NODE_ENV=production
COPY --from=builder /app/.next/standalone ./
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next/static ./.next/static

EXPOSE 3000
CMD ["node", "server.js"]
```

---

## Analytics & Monitoring

```tsx
// app/layout.tsx — Vercel Analytics
import { Analytics } from '@vercel/analytics/react';
import { SpeedInsights } from '@vercel/speed-insights/next';

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html>
      <body>
        {children}
        <Analytics />
        <SpeedInsights />
      </body>
    </html>
  );
}
```
