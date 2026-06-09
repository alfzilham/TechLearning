# 05 Function

## Parameter & Return

| Konsep               | Penjelasan                       | Contoh                     |
| -------------------- | -------------------------------- | -------------------------- |
| Parameter type       | Tipe tiap parameter              | `(a: number, b: number)`   |
| Return type          | Tipe nilai kembali               | `(): string => "hello"`    |
| Optional param `?`   | Parameter boleh tidak dikirim    | `(name?: string)`          |
| Default param        | Nilai default jika tidak dikirim | `(name: string = "Guest")` |
| Rest param `...args` | Kumpulan sisa argumen            | `(...nums: number[])`      |

## Function Type & Overload

| Konsep              | Penjelasan                            | Contoh                                                                                    |
| ------------------- | ------------------------------------- | ----------------------------------------------------------------------------------------- |
| Arrow function type | Tipe untuk fungsi arrow               | `(a: number) => boolean`                                                                  |
| Function type alias | Nama untuk tipe fungsi                | `type Calc = (a: number) => number`                                                       |
| Overload signature  | Banyak signature sebelum implementasi | `function add(a: number, b: number): number; function add(a: string, b: string): string;` |
| `void` return       | Fungsi tidak return apa-apa           | `function log(): void`                                                                    |
| `never` return      | Fungsi throw / infinite loop          | `function fail(): never`                                                                  |

```typescript
// Parameter & return type
function add(a: number, b: number): number {
  return a + b;
}

// Optional & default param
function greet(name?: string): string {
  return `Hello ${name ?? "Guest"}`;
}
function greet2(name: string = "Guest"): string {
  return `Hello ${name}`;
}

// Rest parameter
function sum(...nums: number[]): number {
  return nums.reduce((a, b) => a + b, 0);
}

// Arrow function type
const double: (x: number) => number = (x) => x * 2;

// Function type alias
type MathOp = (a: number, b: number) => number;
const multiply: MathOp = (a, b) => a * b;
const divide: MathOp = (a, b) => a / b;

// Overload signature
function process(x: number): number;
function process(x: string): string;
function process(x: number | string): number | string {
  if (typeof x === "number") return x * 2;
  return x.toUpperCase();
}
console.log(process(5)); // 10
console.log(process("hello")); // "HELLO"

// void vs never
function log(msg: string): void {
  console.log(msg);
}
function throwErr(msg: string): never {
  throw new Error(msg);
}
function infinite(): never {
  while (true) {}
}
```
