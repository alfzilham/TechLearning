# Phase 3: TypeScript

**Durasi:** 7 hari (Minggu 4)
**Tujuan:** Menulis JavaScript dengan type safety

---

## Kenapa TypeScript?

TypeScript adalah JavaScript dengan type checking. Bayangkan Anda punya asisten yang teriak "INI ERROR!" sebelum kode dijalanin, daripada nunggu error muncul di browser pas user lagi pake. TypeScript menangkap bug di **compile time**, bukan **runtime**.

---

### Hari 1: Setup & Basic Types

**Konsep:**
- Install TypeScript: `npm install -g typescript`
- `tsc --init` → generates `tsconfig.json`
- Compile: `tsc file.ts` → menghasilkan `file.js`
- `tsc --watch` → auto-compile setiap ada perubahan
- Basic types: `string`, `number`, `boolean`, `null`, `undefined`, `void`, `never`, `any`
- Type annotation: `const nama: string = "John"`
- Type inference (TS otomatis detect type)

**Tugas:**
```ts
// Buat file basic.ts
// 1. Buat variable dengan type annotation: nama (string), umur (number), isActive (boolean)
// 2. Buat function greet(nama: string): string yang return "Halo, {nama}"
// 3. Buat function add(a: number, b: number): number
// 4. Coba passing string ke parameter number — lihat error TS
// 5. Compile dan jalanin hasil JS-nya
```

---

### Hari 2: Type vs Interface

**Konsep:**
- `type`: `type User = { name: string; age: number }`
- `interface`: `interface User { name: string; age: number }`
- Perbedaan: interface bisa di-extend (`extends`), type bisa union (`|`) & intersection (`&`)
- Optional properties (`?`)
- Readonly properties (`readonly`)
- `extends` untuk interface, `&` untuk type

**Tugas:**
```ts
// 1. Buat interface Product { id, name, price, category?, readonly createdAt }
// 2. Buat interface DigitalProduct extends Product { downloadLink, fileSize }
// 3. Buat type Status = 'active' | 'inactive' | 'pending' (union type)
// 4. Buat function printProduct(product: Product): void
// 5. Panggil dengan object valid → ok, hapus field required → error
```

---

### Hari 3: Arrays, Tuples & Enums

**Konsep:**
- Array types: `string[]` atau `Array<string>`
- Tuple: `[string, number]` — array dengan jumlah & type tetap
- `enum`: kumpulan constant yang related

```ts
enum Role {
  Admin = 'ADMIN',
  User = 'USER',
  Guest = 'GUEST'
}
```

**Tugas:**
```ts
// 1. Buat array of Product (dari hari 2)
// 2. Buat tuple [string, number] untuk [nama, harga]
// 3. Buat enum Category { Electronics, Clothing, Food }
// 4. Buat function filterByCategory(products: Product[], category: Category): Product[]
```

---

### Hari 4: Generics

**Konsep:**
- Kenapa generics? — menghindari `any` dan tetap fleksibel
- `<T>` — type parameter
- `function identity<T>(arg: T): T`
- Generic constraints: `<T extends HasId>`
- Generic interface

**Tugas:**
```ts
// 1. Buat generic function getFirstElement<T>(arr: T[]): T | undefined
// 2. Buat generic interface ApiResponse<T> { data: T; status: number; message: string }
// 3. Buat function fetchData<T>(url: string): Promise<ApiResponse<T>>
// 4. Gunakan ApiResponse<User> dan ApiResponse<Product[]>
```

---

### Hari 5: Utility Types & Type Narrowing

**Konsep:**
- `Partial<T>` — semua property optional
- `Required<T>` — semua property wajib
- `Pick<T, K>` — ambil beberapa property
- `Omit<T, K>` — hapus beberapa property
- `Record<K, V>` — object dengan key/value tertentu
- Type narrowing:
  - `typeof` guard: `if (typeof x === 'string')`
  - `instanceof` guard
  - Discriminated union: `type Shape = Circle | Square` dengan `kind` property

**Tugas:**
```ts
interface User { id: number; name: string; email: string; role: string }

// 1. Partial<User> untuk update user (tidak perlu semua field)
// 2. Pick<User, 'id' | 'name'> untuk list view
// 3. Omit<User, 'email'> untuk public profile
// 4. Buat discriminated union untuk bentuk: Circle (radius) | Square (side) | Triangle (base, height)
// 5. Function calculateArea yang narrowing berdasarkan type
```

---

### Hari 6: TypeScript dengan DOM

**Konsep:**
- Type assertion: `const input = document.getElementById('name') as HTMLInputElement`
- `HTMLElement`, `HTMLInputElement`, `HTMLButtonElement`
- Event types: `MouseEvent`, `KeyboardEvent`, `SubmitEvent`
- `const form = document.querySelector('form')!` — non-null assertion

**Tugas:**
Refactor project Todo List (dari Phase 2) ke TypeScript:
- Ganti semua `.js` ke `.ts`
- Tambah type untuk Todo item: `interface Todo { id: number; text: string; completed: boolean }`
- Type assertion untuk DOM elements
- Function signature dengan type

---

### Hari 7: TypeScript Configuration & Final Project

**Konsep:**
- `tsconfig.json`:
  - `strict: true` — aktivasikan semua strict checking
  - `target: "ES2020"` — versi JS output
  - `module: "ESNext"` — module system
  - `outDir: "./dist"` — folder output
  - `rootDir: "./src"` — folder source
  - `noUnusedLocals: true`
  - `noUnusedParameters: true`
- `tsc --noEmit` — cek type tanpa compile

**Final Project:**
Convert semua project Phase 1 & 2 ke TypeScript:
1. Landing Page HTML → tidak perlu (HTML bukan TS)
2. Todo List → `.ts` dengan strict type
3. Fetch API Explorer → `.ts` dengan type

**Checklist Penguasaan:**
- [ ] Paham perbedaan `type` dan `interface`
- [ ] Bisa bikin generic function
- [ ] Menggunakan utility types (Partial, Pick, Omit)
- [ ] Menerapkan discriminated union
- [ ] Bisa setup tsconfig.json
- [ ] Todo List jalan dengan strict TypeScript tanpa error

---

## Referensi

- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeScript Playground](https://www.typescriptlang.org/play)
- [Type Challenges](https://github.com/type-challenges/type-challenges) — latihan type
