# 08 Utility Types

## Object Manipulation

| Utility        | Penjelasan                              | Contoh                       |
| -------------- | --------------------------------------- | ---------------------------- |
| `Partial<T>`   | Semua properti jadi optional            | `Partial<User>`              |
| `Required<T>`  | Semua properti jadi wajib               | `Required<User>`             |
| `Readonly<T>`  | Semua properti jadi readonly            | `Readonly<User>`             |
| `Pick<T, K>`   | Ambil subset properti                   | `Pick<User, "id" \| "name">` |
| `Omit<T, K>`   | Hapus properti tertentu                 | `Omit<User, "password">`     |
| `Record<K, V>` | Object dengan key & value tipe tertentu | `Record<string, number>`     |

## Union & Function

| Utility          | Penjelasan                   | Contoh                                         |
| ---------------- | ---------------------------- | ---------------------------------------------- |
| `Exclude<T, U>`  | Hapus dari union             | `Exclude<string \| number, string>` → `number` |
| `Extract<T, U>`  | Ambil dari union             | `Extract<string \| number, string>` → `string` |
| `NonNullable<T>` | Hapus `null` & `undefined`   | `NonNullable<string \| null>` → `string`       |
| `ReturnType<T>`  | Ambil return type fungsi     | `ReturnType<typeof fn>`                        |
| `Parameters<T>`  | Ambil tuple parameter fungsi | `Parameters<typeof fn>`                        |
| `Awaited<T>`     | Ambil tipe dari Promise      | `Awaited<Promise<string>>` → `string`          |

## String Manipulation

| Utility           | Penjelasan            | Contoh                              |
| ----------------- | --------------------- | ----------------------------------- |
| `Capitalize<T>`   | Huruf pertama kapital | `Capitalize<"hello">` → `"Hello"`   |
| `Uncapitalize<T>` | Huruf pertama kecil   | `Uncapitalize<"Hello">` → `"hello"` |
| `Uppercase<T>`    | Semua huruf kapital   | `Uppercase<"hello">` → `"HELLO"`    |
| `Lowercase<T>`    | Semua huruf kecil     | `Lowercase<"Hello">` → `"hello"`    |

```typescript
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}

// Object utilities
type PartialUser = Partial<User>;
// { id?: number; name?: string; email?: string; password?: string }

type JustName = Pick<User, "id" | "name">;
// { id: number; name: string }

type PublicUser = Omit<User, "password">;
// { id: number; name: string; email: string }

type NameMap = Record<string, string>;
// { [key: string]: string }

// Union utilities
type Status = "active" | "inactive" | "deleted";
type ActiveStatus = Exclude<Status, "deleted">;
// "active" | "inactive"

type HasLength = Extract<
  string | number | { length: number },
  { length: number }
>;
// string | { length: number } (string punya .length)

type NonNullableStr = NonNullable<string | null | undefined>;
// string

// Function utilities
function greet(name: string, age: number): string {
  return `${name} is ${age}`;
}
type GreetReturn = ReturnType<typeof greet>; // string
type GreetParams = Parameters<typeof greet>; // [string, number]

// Promise
type PromiseResult = Awaited<Promise<Promise<string>>>; // string

// String manipulation
type Caps = Capitalize<"hello">; // "Hello"
type Lower = Lowercase<"HELLO">; // "hello"
type Upper = Uppercase<"hello">; // "HELLO"
type Uncap = Uncapitalize<"Hello">; // "hello"
```
