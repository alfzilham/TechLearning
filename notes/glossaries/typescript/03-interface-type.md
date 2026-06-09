# 03 Interface & Type

## Interface

| Konsep          | Penjelasan               | Contoh                                        |
| --------------- | ------------------------ | --------------------------------------------- |
| `interface`     | Definisi shape object    | `interface User { id: number; name: string }` |
| Optional `?`    | Properti boleh tidak ada | `email?: string`                              |
| `readonly`      | Properti hanya baca      | `readonly id: number`                         |
| Index signature | Properti dinamis         | `[key: string]: any`                          |
| `extends`       | Warisi interface lain    | `interface Admin extends User {}`             |

## Type Alias

| Konsep           | Penjelasan                    | Contoh                                |
| ---------------- | ----------------------------- | ------------------------------------- |
| `type` alias     | Buat nama untuk tipe          | `type ID = number`                    |
| Union `\|`       | Salah satu dari beberapa tipe | `type Status = "aktif" \| "nonaktif"` |
| Intersection `&` | Gabung dua tipe               | `type A = B & C`                      |
| Literal type     | Tipe dengan value spesifik    | `type Role = "admin" \| "user"`       |

## Interface vs Type

| Aspek               | interface        | type                                         |
| ------------------- | ---------------- | -------------------------------------------- |
| Declaration merging | ✅ bisa ditambah | ❌ tidak bisa                                |
| Extends/inheritance | `extends`        | `&` intersection                             |
| Union & tuple       | ❌               | ✅ `type A = string \| number`               |
| Mapped types        | ❌               | ✅ `type Opt<T> = { [K in keyof T]?: T[K] }` |

```typescript
// Interface dasar
interface User {
  readonly id: number;
  name: string;
  email?: string; // optional
}

// Index signature
interface Dictionary {
  [key: string]: string;
}
const dict: Dictionary = { hello: "halo" };

// Interface inheritance
interface Admin extends User {
  role: "admin";
}

// Type alias
type ID = number | string;
type Status = "aktif" | "nonaktif";

// Intersection type
type Named = { name: string };
type Aged = { age: number };
type Person = Named & Aged;
// Person = { name: string; age: number }

// Literal type
type Direction = "up" | "down" | "left" | "right";

// Declaration merging (hanya interface)
interface Product {
  name: string;
}
interface Product {
  price: number;
}
// Product sekarang = { name: string; price: number }

// Contoh pemakaian
const user: User = { id: 1, name: "Alice" };
const admin: Admin = { id: 2, name: "Bob", role: "admin" };
const dir: Direction = "up";
```
