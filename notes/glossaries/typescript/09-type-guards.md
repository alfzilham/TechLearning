# 09 Type Guards

| Konsep                         | Penjelasan                                 | Contoh                                                     |
| ------------------------------ | ------------------------------------------ | ---------------------------------------------------------- |
| `typeof` guard                 | Cek tipe primitif runtime                  | `typeof x === "string"`                                    |
| `instanceof` guard             | Cek instance class                         | `x instanceof Date`                                        |
| `in` operator                  | Cek keberadaan properti                    | `"name" in obj`                                            |
| Custom type guard              | Fungsi return `x is Type`                  | `function isStr(x: any): x is string`                      |
| Discriminated union            | Union dengan field pembeda (`kind`)        | `type Shape = Circle \| Square` (dengan `kind`)            |
| `never` exhaustive check       | Pastikan semua case tertangani             | `const _exhaustive: never = x`                             |
| `as` assertion                 | Paksa tipe (hati-hati)                     | `(x as string).length`                                     |
| `satisfies` operator (TS 4.9+) | Validasi tipe tanpa mengubah inferred type | `const c = { name: "x" } satisfies Record<string, string>` |

```typescript
// typeof guard
function process(value: string | number): string {
  if (typeof value === "string") {
    return value.toUpperCase(); // TS tahu ini string
  }
  return value.toFixed(2); // TS tahu ini number
}

// instanceof guard
class Dog {
  bark() {
    return "Woof!";
  }
}
class Cat {
  meow() {
    return "Meow!";
  }
}

function speak(animal: Dog | Cat): string {
  if (animal instanceof Dog) return animal.bark();
  return animal.meow();
}

// in operator
interface Car {
  drive(): void;
}
interface Boat {
  sail(): void;
}
function move(v: Car | Boat) {
  if ("drive" in v) v.drive();
  else v.sail();
}

// Custom type guard
interface Fish {
  swim(): void;
}
interface Bird {
  fly(): void;
}
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}
function movePet(pet: Fish | Bird) {
  if (isFish(pet))
    pet.swim(); // TS tahu ini Fish
  else pet.fly();
}

// Discriminated union
type Circle = { kind: "circle"; radius: number };
type Square = { kind: "square"; side: number };
type Shape = Circle | Square;

function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.side ** 2;
  }
}

// never exhaustive check
function assertNever(x: never): never {
  throw new Error("Unexpected: " + x);
}
function areaExhaustive(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.side ** 2;
    default:
      return assertNever(shape); // error jika ada case baru
  }
}

// as assertion
const input: unknown = "teks";
const length = (input as string).length;

// satisfies operator (TS 4.9+)
const config = {
  api: "https://api.com",
  timeout: 5000,
} satisfies Record<string, string | number>;
// config.api — TS tahu ini string (not string | number)
```
