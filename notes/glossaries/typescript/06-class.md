# 06 Class

| Konsep                | Penjelasan                            | Contoh                                       |
| --------------------- | ------------------------------------- | -------------------------------------------- |
| `public`              | Bisa diakses dari mana saja (default) | `public name: string`                        |
| `private`             | Hanya di dalam class                  | `private secret: string`                     |
| `protected`           | Class & turunan saja                  | `protected id: number`                       |
| `readonly`            | Hanya baca setelah inisialisasi       | `readonly id: number`                        |
| `abstract class`      | Class yang tidak bisa di-instantiate  | `abstract class Animal {}`                   |
| `abstract method`     | Method tanpa implementasi             | `abstract sound(): void`                     |
| `implements`          | Class mengikuti kontrak interface     | `class Dog implements Animal {}`             |
| `static`              | Milik class, bukan instance           | `static version: string`                     |
| Constructor shorthand | Langsung deklarasi + assign           | `constructor(public name: string) {}`        |
| Getter/Setter         | Properti dengan akses kontrol         | `get name(): string` / `set name(v: string)` |
| `this` type           | Return tipe class sendiri             | `setName(name: string): this`                |

```typescript
// Constructor shorthand
class Person {
  constructor(
    public name: string,
    private age: number,
    protected id: number,
    readonly createdAt: Date = new Date(),
  ) {}
}

// Getter & Setter
class Employee extends Person {
  private _salary: number = 0;

  get salary(): number {
    return this._salary;
  }

  set salary(value: number) {
    if (value < 0) throw new Error("Invalid");
    this._salary = value;
  }
}

// abstract class
abstract class Animal {
  abstract sound(): void;

  move(): void {
    console.log("Moving...");
  }
}

class Dog extends Animal {
  sound(): void {
    console.log("Woof!");
  }
}

// implements
interface Swimmer {
  swim(): void;
}
class Fish implements Swimmer {
  swim(): void {
    console.log("Swimming");
  }
}

// static
class Config {
  static readonly VERSION = "1.0.0";
  static getConfig(): string {
    return "config";
  }
}
console.log(Config.VERSION);

// this type — method chaining
class Builder {
  constructor(private value: number = 0) {}

  add(n: number): this {
    this.value += n;
    return this;
  }

  multiply(n: number): this {
    this.value *= n;
    return this;
  }

  result(): number {
    return this.value;
  }
}

const val = new Builder(1).add(2).multiply(3).result();
console.log(val); // 9
```
