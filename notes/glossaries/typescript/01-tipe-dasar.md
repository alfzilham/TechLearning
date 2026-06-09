# 01 Tipe Dasar

## Tipe Primitif

| Konsep      | Penjelasan                     | Contoh                                  |
| ----------- | ------------------------------ | --------------------------------------- |
| `string`    | Teks / karakter                | `let nama: string = "Alice"`            |
| `number`    | Angka (integer & float)        | `let umur: number = 25`                 |
| `boolean`   | `true` / `false`               | `let aktif: boolean = true`             |
| `null`      | Nilai kosong yang disengaja    | `let data: null = null`                 |
| `undefined` | Nilai belum diisi              | `let x: undefined = undefined`          |
| `void`      | Fungsi tanpa return value      | `function log(): void { ... }`          |
| `never`     | Fungsi tidak pernah selesai    | `function error(): never { throw ... }` |
| `any`       | Matikan type-check (hindari!)  | `let bebas: any = "apa aja"`            |
| `unknown`   | Aman versi `any` — perlu guard | `let y: unknown = "cek dulu"`           |

## Type Inference & Typeof

| Konsep           | Penjelasan                        | Contoh                         |
| ---------------- | --------------------------------- | ------------------------------ |
| Type inference   | TS otomatis infer tipe dari value | `let msg = "Hello"` → `string` |
| `typeof` runtime | Cek tipe di JS runtime            | `typeof x === "string"`        |
| `typeof` type    | Ambil tipe dari value di TS       | `type Nama = typeof nama`      |

```typescript
// Tipe dasar
let nama: string = "Alice";
let umur: number = 25;
let aktif: boolean = true;
let kosong: null = null;
let belumDiisi: undefined = undefined;

// void
function logPesan(pesan: string): void {
  console.log(pesan);
}

// never
function throwError(msg: string): never {
  throw new Error(msg);
}

// any (hindari)
let bebas: any = "bisa string";
bebas = 42; // ok, tapi bahaya

// unknown (lebih aman)
let data: unknown = "fetch result";
if (typeof data === "string") {
  console.log(data.toUpperCase());
}

// Type inference
let pesan = "Hello TS"; // inferred sebagai string
// pesan = 42; // ❌ error

// typeof type
const user = { id: 1, name: "Alice" };
type UserType = typeof user;
// { id: number; name: string }
```
