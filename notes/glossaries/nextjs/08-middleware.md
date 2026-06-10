# Middleware

## Dasar Middleware

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `middleware.ts` | File di root `src/` atau project root | `export function middleware(request: NextRequest)` |
| `matcher` | Tentukan route mana yang diproses | `export const config = { matcher: ['/dashboard/:path*'] }` |
| `NextResponse.next()` | Lanjutkan request | Default |
| `NextResponse.redirect()` | Redirect ke URL lain | Auth guard |
| `NextResponse.rewrite()` | Tampilkan URL beda dari konten beda | A/B testing |

```tsx
// middleware.ts — di root project (samping app folder)
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  console.log('Middleware running for:', request.nextUrl.pathname);
  return NextResponse.next();
}

// Hanya jalan untuk route tertentu
export const config = {
  matcher: ['/dashboard/:path*', '/api/:path*'],
};
```

---

## Matcher Patterns

| Pattern | Match | Contoh |
|---------|-------|--------|
| `/dashboard/:path*` | /dashboard dan semua sub-route | `/dashboard`, `/dashboard/settings` |
| `/api/:path*` | Semua API route | `/api/users`, `/api/products/1` |
| `/((?!api|_next).*)` | Semua kecuali api & _next | `/about`, `/contact` |
| `/about` | Exact match | Hanya `/about` |

```tsx
export const config = {
  matcher: [
    // Dashboard & sub-routes
    '/dashboard/:path*',
    // API routes
    '/api/:path*',
    // Semua kecuali static files
    '/((?!_next/static|_next/image|favicon.ico).*)',
  ],
};
```

---

## Auth Guard Middleware

```tsx
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  const token = request.cookies.get('token')?.value;
  const { pathname } = request.nextUrl;

  // Route yang butuh login
  const protectedRoutes = ['/dashboard', '/profile', '/settings'];
  const isProtected = protectedRoutes.some(route => pathname.startsWith(route));

  if (isProtected && !token) {
    const loginUrl = new URL('/login', request.url);
    loginUrl.searchParams.set('redirect', pathname);
    return NextResponse.redirect(loginUrl);
  }

  // Jika sudah login, redirect dari /login ke /dashboard
  if (token && pathname === '/login') {
    return NextResponse.redirect(new URL('/dashboard', request.url));
  }

  return NextResponse.next();
}

export const config = {
  matcher: ['/dashboard/:path*', '/profile/:path*', '/settings/:path*', '/login'],
};
```

---

## Redirect & Rewrite

```tsx
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  const { pathname } = request.nextUrl;

  // Redirect old URL ke new URL
  if (pathname.startsWith('/old-blog')) {
    const newPath = pathname.replace('/old-blog', '/blog');
    return NextResponse.redirect(new URL(newPath, request.url));
  }

  // Rewrite — tampilkan konten berbeda tapi URL tetap
  if (pathname.startsWith('/country')) {
    const country = request.geo?.country || 'ID';
    return NextResponse.rewrite(
      new URL(`/${country}${pathname}`, request.url)
    );
  }

  // Add custom headers
  const response = NextResponse.next();
  response.headers.set('x-custom-header', 'hello');
  return response;
}
```

---

## i18n Middleware

```tsx
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

const locales = ['id', 'en'];
const defaultLocale = 'id';

export function middleware(request: NextRequest) {
  const { pathname } = request.nextUrl;

  // Cek apakah pathname sudah mengandung locale
  const hasLocale = locales.some(locale =>
    pathname.startsWith(`/${locale}/`) || pathname === `/${locale}`
  );

  if (hasLocale) return NextResponse.next();

  // Redirect ke locale default
  return NextResponse.redirect(
    new URL(`/${defaultLocale}${pathname}`, request.url)
  );
}

export const config = {
  matcher: ['/((?!api|_next|.*\\..*).*)'],
};
```

---

## Response Headers

```tsx
import { NextResponse } from 'next/server';

export function middleware() {
  const response = NextResponse.next();

  // Security headers
  response.headers.set('X-Frame-Options', 'DENY');
  response.headers.set('X-Content-Type-Options', 'nosniff');
  response.headers.set('Referrer-Policy', 'strict-origin-when-cross-origin');
  response.headers.set(
    'Content-Security-Policy',
    "default-src 'self'"
  );

  return response;
}
```
