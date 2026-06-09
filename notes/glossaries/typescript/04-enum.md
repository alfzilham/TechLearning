# 04 Enum

| Konsep                 | Penjelasan                              | Contoh                                          |
| ---------------------- | --------------------------------------- | ----------------------------------------------- |
| Numeric enum           | Default mulai dari 0                    | `enum Arah { Atas, Bawah }`                     |
| Enum dengan nilai awal | Set custom start                        | `enum Arah { Atas = 1, Bawah }`                 |
| String enum            | Nilai berupa string                     | `enum Warna { Merah = "RED", Hijau = "GREEN" }` |
| `const enum`           | Inline saat compile (hilang di runtime) | `const enum Arah { Atas, Bawah }`               |
| Reverse mapping        | Akses nama dari nilai (numeric only)    | `Arah[0] // "Atas"`                             |
| Enum as type           | Gunakan enum sebagai tipe parameter     | `function move(a: Arah)`                        |
| Computed values        | Nilai dihitung saat runtime             | `enum E { X = someFunc() }`                     |

```typescript
// Numeric enum (default 0, 1, 2...)
enum Direction {
  Up, // 0
  Down, // 1
  Left, // 2
  Right, // 3
}
let dir: Direction = Direction.Up; // 0

// Numeric enum dengan custom start
enum Direction2 {
  Up = 1,
  Down, // 2
  Left, // 3
  Right, // 4
}

// Reverse mapping (numeric only)
console.log(Direction[0]); // "Up"
console.log(Direction.Up); // 0
console.log(Direction["Up"]); // 0

// String enum
enum Color {
  Red = "MERAH",
  Green = "HIJAU",
  Blue = "BIRU",
}
console.log(Color.Red); // "MERAH"
// ⚠️ String enum TIDAK punya reverse mapping

// const enum — di-inline saat kompilasi
const enum Size {
  Small = "S",
  Medium = "M",
  Large = "L",
}
let mySize = Size.Medium; // jadi "M" di JS output

// Enum sebagai tipe
function move(direction: Direction): void {
  console.log("Moving", direction);
}
move(Direction.Up);

// Enum dengan computed values
function getValue(): number {
  return Date.now();
}
enum Computed {
  A = getValue(),
  B = A + 1,
}

// Heterogeneous enum (campur — tidak disarankan)
enum Mixed {
  Yes = "YA",
  No = 0,
}
```
