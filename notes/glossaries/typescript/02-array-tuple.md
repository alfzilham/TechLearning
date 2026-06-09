# 02 Array & Tuple

| Konsep              | Penjelasan                         | Contoh                                        |
| ------------------- | ---------------------------------- | --------------------------------------------- |
| `type[]`            | Array dengan tipe elemen           | `let angka: number[] = [1, 2, 3]`             |
| `Array<type>`       | Generic syntax array               | `let nama: Array<string> = ["a", "b"]`        |
| `[string, number]`  | Tuple — array tetap panjang & tipe | `let pair: [string, number] = ["umur", 25]`   |
| `readonly` array    | Mencegah mutasi array              | `const arr: readonly number[] = [1, 2]`       |
| `readonly` tuple    | Tuple yang tidak bisa diubah       | `let pos: readonly [number, number] = [0, 0]` |
| Label pada tuple    | Beri nama tiap posisi (TS 4+)      | `let range: [from: number, to: number]`       |
| Destructuring array | Ekstrak elemen array               | `const [a, b] = [1, 2]`                       |
| Destructuring tuple | Ekstrak tuple dengan label         | `const [nama, val] = pair`                    |

```typescript
// Array syntax
let angka: number[] = [1, 2, 3];
let nama: Array<string> = ["Alice", "Bob"];
let campuran: (string | number)[] = ["teks", 42];

// readonly array
const bacaan: readonly number[] = [1, 2, 3];
// bacaan.push(4); // ❌ error

// Tuple dasar
let pair: [string, number] = ["umur", 25];
// pair = [25, "umur"]; // ❌ error urutan salah

// Tuple dengan label (TS 4+)
let range: [from: number, to: number] = [0, 100];

// readonly tuple
let pos: readonly [number, number] = [10, 20];
// pos[0] = 5; // ❌ error

// Destructuring array
const [pertama, kedua] = [1, 2, 3];
console.log(pertama, kedua); // 1, 2

// Destructuring tuple
const [key, value]: [string, number] = ["skor", 95];
console.log(key, value); // "skor", 95

// Tuple dengan rest element
let list: [string, ...number[]] = ["x", 1, 2, 3];
```
