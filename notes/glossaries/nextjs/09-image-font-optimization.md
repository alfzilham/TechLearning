# Image, Font & SEO

## next/image

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `next/image` | Optimasi gambar otomatis | `import Image from 'next/image'` |
| `width` & `height` | Ukuran gambar (wajib) | `width={800} height={600}` |
| `fill` | Mengisi parent container | `fill className="object-cover"` |
| `priority` | Prioritaskan load (LCP) | `priority` untuk gambar di atas lipatan |
| `placeholder` | Placeholder saat loading | `placeholder="blur"` |
| Remote images | Perlu `remotePatterns` di config | `next.config.js` |

```tsx
import Image from 'next/image';
import logo from './logo.png'; // Local image (auto width/height)

// Local image
export default function Logo() {
  return (
    <Image
      src={logo}
      alt="Logo"
      priority // LCP optimization
      placeholder="blur" // Blur-up effect
    />
  );
}

// Remote image
export default function ProductImage({ src, alt }: { src: string; alt: string }) {
  return (
    <Image
      src={src}
      alt={alt}
      width={400}
      height={300}
      className="rounded-lg"
      sizes="(max-width: 768px) 100vw, 400px"
    />
  );
}
```

```js
// next.config.js — remote image domains
module.exports = {
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'images.example.com',
      },
      {
        protocol: 'https',
        hostname: '**.cdn.com',
      },
    ],
  },
};
```

---

## next/font

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `next/font` | Optimasi font otomatis | `import { Inter } from 'next/font/google'` |
| Google Fonts | Variable fonts support | `const inter = Inter({ subsets: ['latin'] })` |
| Local fonts | Font dari file lokal | `import localFont from 'next/font/local'` |
| `variable` | CSS variable | `inter.variable` → `--font-inter` |

```tsx
// Google Font
import { Inter, Roboto_Mono } from 'next/font/google';

const inter = Inter({
  subsets: ['latin'],
  variable: '--font-inter', // CSS variable
});

const mono = Roboto_Mono({
  subsets: ['latin'],
  display: 'swap',
});

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="id" className={`${inter.variable} ${mono.variable}`}>
      <body style={{ fontFamily: 'var(--font-inter)' }}>
        {children}
      </body>
    </html>
  );
}
```

```tsx
// Local Font
import localFont from 'next/font/local';

const myFont = localFont({
  src: './fonts/my-font.woff2',
  display: 'swap',
});
```

---

## Metadata & SEO

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `metadata` export | Static metadata object | `export const metadata = { title: '...' }` |
| `generateMetadata` | Dynamic metadata | `export async function generateMetadata()` |
| `Metadata` type | TypeScript type | `import type { Metadata } from 'next'` |

```tsx
import type { Metadata } from 'next';

// Static metadata
export const metadata: Metadata = {
  title: {
    default: 'My App',
    template: '%s | My App', // "About | My App"
  },
  description: 'My Next.js application',
  openGraph: {
    title: 'My App',
    description: 'My Next.js application',
    images: ['/og-image.png'],
  },
  robots: {
    index: true,
    follow: true,
  },
};

// Dynamic metadata
export async function generateMetadata({ params }: Props): Promise<Metadata> {
  const post = await getPost(params.slug);
  return {
    title: post.title,
    description: post.excerpt,
    openGraph: {
      title: post.title,
      images: [post.image],
    },
    alternates: {
      canonical: `/blog/${post.slug}`,
    },
  };
}
```

---

## Sitemap & Robots

```tsx
// app/sitemap.ts
import { MetadataRoute } from 'next';

export default async function sitemap(): Promise<MetadataRoute.Sitemap> {
  const baseUrl = 'https://example.com';
  const posts = await getPosts();

  const blogEntries = posts.map(post => ({
    url: `${baseUrl}/blog/${post.slug}`,
    lastModified: post.updatedAt,
    changeFrequency: 'weekly' as const,
    priority: 0.8,
  }));

  return [
    {
      url: baseUrl,
      lastModified: new Date(),
      changeFrequency: 'daily',
      priority: 1,
    },
    ...blogEntries,
  ];
}

// app/robots.ts
import { MetadataRoute } from 'next';

export default function robots(): MetadataRoute.Robots {
  return {
    rules: {
      userAgent: '*',
      allow: '/',
      disallow: '/dashboard/',
    },
    sitemap: 'https://example.com/sitemap.xml',
  };
}
```
