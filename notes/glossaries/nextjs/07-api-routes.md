# API Route Handlers

## Route Handlers

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `route.ts` | File untuk API endpoint | `app/api/users/route.ts` → `/api/users` |
| HTTP methods | `GET`, `POST`, `PUT`, `PATCH`, `DELETE` | `export async function GET(request)` |
| `NextRequest` | Extended Request object Next.js | `import { NextRequest } from 'next/server'` |
| `NextResponse` | Extended Response object | `return NextResponse.json({ data })` |

```tsx
// app/api/users/route.ts — GET & POST
import { NextRequest, NextResponse } from 'next/server';

export async function GET(request: NextRequest) {
  const users = await db.user.findMany();
  return NextResponse.json(users);
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  const user = await db.user.create({ data: body });
  return NextResponse.json(user, { status: 201 });
}
```

---

## Dynamic Route Handlers

```tsx
// app/api/users/[id]/route.ts
import { NextRequest, NextResponse } from 'next/server';

type Params = { params: { id: string } };

export async function GET(request: NextRequest, { params }: Params) {
  const user = await db.user.findUnique({ where: { id: Number(params.id) } });

  if (!user) {
    return NextResponse.json({ error: 'User not found' }, { status: 404 });
  }

  return NextResponse.json(user);
}

export async function PUT(request: NextRequest, { params }: Params) {
  const body = await request.json();
  const updated = await db.user.update({
    where: { id: Number(params.id) },
    data: body,
  });
  return NextResponse.json(updated);
}

export async function DELETE(request: NextRequest, { params }: Params) {
  await db.user.delete({ where: { id: Number(params.id) } });
  return NextResponse.json({ success: true });
}
```

---

## Request & Response

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `request.json()` | Parse JSON body | `const body = await request.json()` |
| `request.nextUrl` | URL object (searchParams, pathname) | `request.nextUrl.searchParams.get('q')` |
| `request.headers` | HTTP headers | `request.headers.get('Authorization')` |
| `request.cookies` | Cookies | `request.cookies.get('token')` |
| `NextResponse.json()` | JSON response | `NextResponse.json({ data })` |
| `NextResponse.redirect()` | Redirect | `NextResponse.redirect(new URL('/login', request.url))` |

```tsx
// app/api/search/route.ts — Query params
import { NextRequest, NextResponse } from 'next/server';

export async function GET(request: NextRequest) {
  const searchParams = request.nextUrl.searchParams;
  const query = searchParams.get('q');
  const page = Number(searchParams.get('page') || '1');

  const results = await db.product.findMany({
    where: { nama: { contains: query } },
    skip: (page - 1) * 20,
    take: 20,
  });

  return NextResponse.json({
    data: results,
    page,
    total: results.length,
  });
}

// app/api/auth/login/route.ts — Response dengan cookies
export async function POST(request: NextRequest) {
  const body = await request.json();
  const token = await generateToken(body);

  const response = NextResponse.json({ success: true });

  response.cookies.set('token', token, {
    httpOnly: true,
    secure: true,
    maxAge: 60 * 60 * 24, // 24 jam
    path: '/',
  });

  return response;
}
```

---

## Middleware di Route Handler

```tsx
// app/api/products/route.ts
import { NextResponse } from 'next/server';

export async function GET(request: Request) {
  // Cek authorization
  const authHeader = request.headers.get('authorization');
  if (!authHeader?.startsWith('Bearer ')) {
    return NextResponse.json({ error: 'Unauthorized' }, { status: 401 });
  }

  try {
    const products = await db.product.findMany();
    return NextResponse.json(products);
  } catch (error) {
    return NextResponse.json(
      { error: 'Internal Server Error' },
      { status: 500 }
    );
  }
}
```

---

## CORS di Route Handler

```tsx
// app/api/cors/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function GET(request: NextRequest) {
  return new NextResponse(JSON.stringify({ message: 'CORS enabled' }), {
    headers: {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE',
      'Access-Control-Allow-Headers': 'Content-Type, Authorization',
    },
  });
}

export async function OPTIONS(request: NextRequest) {
  return new NextResponse(null, {
    headers: {
      'Access-Control-Allow-Origin': '*',
      'Access-Control-Allow-Methods': 'GET, POST, PUT, DELETE',
      'Access-Control-Allow-Headers': 'Content-Type, Authorization',
    },
  });
}
```

---

## Streaming Response

```tsx
// app/api/stream/route.ts
export async function GET() {
  const encoder = new TextEncoder();
  const stream = new ReadableStream({
    async start(controller) {
      for (let i = 0; i < 10; i++) {
        await new Promise(r => setTimeout(r, 500));
        controller.enqueue(encoder.encode(`data: ${i}\n\n`));
      }
      controller.close();
    },
  });

  return new Response(stream, {
    headers: {
      'Content-Type': 'text/event-stream',
      'Cache-Control': 'no-cache',
      'Connection': 'keep-alive',
    },
  });
}
```
