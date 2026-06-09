# 07 Generics

| Konsep                        | Penjelasan                            | Contoh                                     |
| ----------------------------- | ------------------------------------- | ------------------------------------------ |
| `<T>` basic                   | Generic type parameter                | `function id<T>(arg: T): T { return arg }` |
| Constraint `<T extends Type>` | Batasi generic hanya ke tipe tertentu | `<T extends { length: number }>`           |
| Multiple `<T, U>`             | Banyak type parameter                 | `function pair<T, U>(a: T, b: U): [T, U]`  |
| Generic interface             | Interface dengan type parameter       | `interface Box<T> { value: T }`            |
| Generic class                 | Class dengan type parameter           | `class Stack<T> { ... }`                   |
| Generic function              | Fungsi dengan type parameter          | `function first<T>(arr: T[]): T`           |
| Default type `<T = string>`   | Nilai default type parameter          | `function create<T = string>(val: T)`      |
| `keyof` constraint            | Parameter terbatas pada key object    | `<T extends keyof U>`                      |

```typescript
// Generic function dasar
function identity<T>(arg: T): T {
  return arg;
}
const num = identity(42); // number
const str = identity("hi"); // string

// Multiple type parameters
function pair<T, U>(a: T, b: U): [T, U] {
  return [a, b];
}
const result = pair("hello", 42); // [string, number]

// Constraint dengan extends
function getLength<T extends { length: number }>(arg: T): number {
  return arg.length;
}
getLength("hello"); // 5
getLength([1, 2, 3]); // 3
// getLength(42);    // ❌ error — number tidak punya .length

// Generic interface
interface Box<T> {
  value: T;
  get(): T;
  set(value: T): void;
}

// Generic class
class Stack<T> {
  private items: T[] = [];

  push(item: T): void {
    this.items.push(item);
  }

  pop(): T | undefined {
    return this.items.pop();
  }
}
const numStack = new Stack<number>();
numStack.push(1);
numStack.push(2);

// Default type parameter
function createArray<T = string>(length: number, value: T): T[] {
  return Array(length).fill(value);
}
const strings = createArray(3, "a"); // string[]

// keyof constraint
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}
const user = { name: "Alice", age: 30 };
getProperty(user, "name"); // string
getProperty(user, "age"); // number
// getProperty(user, "email"); // ❌ error
```
