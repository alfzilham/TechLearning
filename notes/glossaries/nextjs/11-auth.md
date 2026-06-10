# Authentication

## Auth.js (NextAuth.js v5)

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `NextAuth()` | Setup auth handler | `import NextAuth from 'next-auth'` |
| Providers | Google, GitHub, Credentials, dll | `providers: [GithubProvider]` |
| `auth()` | Get session di Server Component | `const session = await auth()` |
| `signIn()` | Trigger login | `signIn('github')` |
| `signOut()` | Logout | `signOut()` |

```tsx
// app/api/auth/[...nextauth]/route.ts
import NextAuth from 'next-auth';
import GitHub from 'next-auth/providers/github';
import Google from 'next-auth/providers/google';
import Credentials from 'next-auth/providers/credentials';
import { PrismaAdapter } from '@auth/prisma-adapter';
import { db } from '@/lib/db';

const handler = NextAuth({
  adapter: PrismaAdapter(db),
  providers: [
    GitHub({
      clientId: process.env.GITHUB_ID!,
      clientSecret: process.env.GITHUB_SECRET!,
    }),
    Google({
      clientId: process.env.GOOGLE_ID!,
      clientSecret: process.env.GOOGLE_SECRET!,
    }),
    Credentials({
      name: 'credentials',
      credentials: {
        email: { label: 'Email', type: 'email' },
        password: { label: 'Password', type: 'password' },
      },
      async authorize(credentials) {
        const user = await db.user.findUnique({
          where: { email: credentials.email },
        });

        if (!user || !user.password) return null;

        const valid = await bcrypt.compare(credentials.password, user.password);
        return valid ? user : null;
      },
    }),
  ],
  pages: {
    signIn: '/login',
    error: '/error',
  },
  session: { strategy: 'jwt' },
  callbacks: {
    async jwt({ token, user }) {
      if (user) token.role = user.role;
      return token;
    },
    async session({ session, token }) {
      if (session.user) session.user.role = token.role;
      return session;
    },
  },
});

export { handler as GET, handler as POST };
```

---

## Auth di Server Component

```tsx
import { auth } from '@/app/api/auth/[...nextauth]/route';

export default async function Dashboard() {
  const session = await auth();

  if (!session?.user) {
    return <p>Anda harus login</p>;
  }

  return (
    <div>
      <h1>Dashboard</h1>
      <p>Selamat datang, {session.user.name}!</p>
      <p>Email: {session.user.email}</p>
      <p>Role: {session.user.role}</p>
    </div>
  );
}
```

---

## Middleware Auth

```tsx
// middleware.ts
import { withAuth } from 'next-auth/middleware';
import { NextResponse } from 'next/server';

export default withAuth(
  function middleware(req) {
    const token = req.nextauth.token;
    const path = req.nextUrl.pathname;

    // Admin-only routes
    if (path.startsWith('/admin') && token?.role !== 'admin') {
      return NextResponse.redirect(new URL('/dashboard', req.url));
    }

    return NextResponse.next();
  },
  {
    callbacks: {
      authorized: ({ token }) => !!token, // Harus login
    },
  }
);

export const config = {
  matcher: ['/dashboard/:path*', '/profile/:path*', '/admin/:path*'],
};
```

---

## Auth di Client Component

```tsx
"use client";
import { useSession, signIn, signOut } from 'next-auth/react';

export default function AuthButton() {
  const { data: session, status } = useSession();

  if (status === 'loading') return <p>Loading...</p>;

  if (session) {
    return (
      <div className="flex items-center gap-4">
        <img src={session.user?.image} alt="" className="w-8 h-8 rounded-full" />
        <span>{session.user?.name}</span>
        <button onClick={() => signOut()} className="btn-danger">
          Logout
        </button>
      </div>
    );
  }

  return (
    <div className="flex gap-2">
      <button onClick={() => signIn('github')} className="btn">
        Login with GitHub
      </button>
      <button onClick={() => signIn('google')} className="btn">
        Login with Google
      </button>
    </div>
  );
}
```

---

## Provider Wrapper

```tsx
// app/Provider.tsx
"use client";
import { SessionProvider } from 'next-auth/react';

export default function Provider({ children }: { children: React.ReactNode }) {
  return <SessionProvider>{children}</SessionProvider>;
}

// app/layout.tsx
import Provider from './Provider';

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html>
      <body>
        <Provider>{children}</Provider>
      </body>
    </html>
  );
}
```
