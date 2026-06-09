# Mindmap — Koneksi Antar Konsep

```
                        ┌──────────────────────────────────────────────────────────────────────────────────────────────────┐
                        │                                            FULLSTACK ENGINEER                                     │
                        └──────────────────────────────────────────────────────────────────────────────────────────────────┘
                                                              │
            ┌─────────────────────────────────────────────────┼─────────────────────────────────────────────────────────────┐
            │                                                 │                                                             │
      FRONTEND                                           BACKEND                                                      DEVOPS
            │                                                 │                                                             │
   ┌────────┴────────┐                               ┌────────┴────────┐                                          ┌────────┴────────┐
   │                 │                               │                 │                                          │                 │
┌──┴──┐          ┌───┴────┐                    ┌────┴─────┐     ┌────┴─────┐                                ┌────┴─────┐    ┌────┴─────┐
│HTML │          │ CSS    │                    │ Database  │     │  API     │                                │  Git     │    │  Deploy  │
└──┬──┘          └───┬────┘                    └────┬──────┘     └────┬──────┘                                └────┬─────┘    └────┬─────┘
   │                 │                              │                │                                           │               │
   │           ┌─────┴──────┐                  ┌────┴──────┐   ┌────┴──────┐                              ┌────┴──────┐   ┌────┴──────┐
   │           │ Box Model  │                  │PostgreSQL  │   │REST API   │                              │ branching  │   │  Vercel   │
   │           │ Flexbox    │                  │Prisma ORM  │   │Server     │                              │ commit     │   │  Railway  │
   │           │ Grid       │                  │Migrations  │   │Actions    │                              │ PR         │   │  Docker   │
   │           │ Responsive │                  │Relations   │   │Route      │                              │            │   │           │
   │           └────────────┘                  │Seed       │   │Handlers   │                              └────────────┘   └────────────┘
   │                                            └────────────┘   │Validation │
   │                                                            │(Zod)      │
   │         ┌──────────────────┐                                └────────────┘
   │         │                  │
   │     ┌───┴──────────────┐   │
   │     │   JAVASCRIPT     │   │
   │     └───┬──────────────┘   │
   │         │                  │
   │    ┌────┴──────────┐      │
   │    │  Variables    │      │
   │    │  Functions    │      │
   │    │  Scope        │      │
   │    │  Closure      │      │
   │    │  Objects      │      │
   │    │  Arrays       │      │
   │    │  Promise      │      │
   │    │  Async/Await  │      │
   │    │  DOM          │      │
   │    └────┬──────────┘      │
   │         │                 │
   │    ┌────┴──────────┐      │
   │    │  TypeScript   │      │
   │    │  ───────────  │      │
   │    │  Types        │      │
   │    │  Interfaces   │      │
   │    │  Generics     │      │
   │    │  Union Types  │      │
   │    └────┬──────────┘      │
   │         │                 │
   │    ┌────┴──────────┐      │
   │    │    REACT      │      │
   │    │  ───────────  │      │
   │    │  Components   │      │
   │    │  JSX          │      │
   │    │  Props        │      │
   │    │  State        │      │
   │    │  Hooks        │      │
   │    │  Effects      │      │
   │    │  Context      │      │
   │    │  Router       │      │
   │    └────┬──────────┘      │
   │         │                 │
   │    ┌────┴──────────┐      │
   │    │   NEXT.JS     │      │
   │    │  ───────────  │      │
   │    │  App Router   │      │
   │    │  Server Comp  │      │
   │    │  Client Comp  │      │
   │    │  Data Fetch   │      │
   │    │  Middleware   │      │
   │    │  Auth         │      │
   │    │  Server       │      │
   │    │  Actions      │      │
   │    └────┬──────────┘      │
   │         │                 │
```

## Dependency Graph

```
HTML ──► CSS ──► JavaScript ──► TypeScript ──► React ──► Next.js ──► Fullstack
  │        │           │              │            │            │            │
  │        │           │              │            │            │       ┌────┴────┐
  │        │           │              │            │            │       │Database │
  │        │           │              │            │            │       │ Auth    │
  │        │           │              │            │            │       │ Testing │
  │        │           │              │            │            │       │ Deploy  │
  │        │           │              │            │            │       └─────────┘
  │        │           │              │            │            │
  ▼        ▼           ▼              ▼            ▼            ▼
Struktur Tampilan   Logika        Type Safety   Komponen     Framework
```

## Prerequisite Chain

```
Ingin ini?                    Harus kuasai ini dulu
──────────                    ─────────────────────
React                         JavaScript (ES6+)
Next.js                       React
TypeScript                    JavaScript
Prisma                        SQL dasar
Testing                       React + JavaScript
Deployment                    Git + Terminal
```
