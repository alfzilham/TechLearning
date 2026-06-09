# 10 Modules

## Export & Import

| Konsep           | Penjelasan                         | Contoh                                |
| ---------------- | ---------------------------------- | ------------------------------------- |
| `export`         | Export named declaration           | `export const x = 1`                  |
| `export default` | Export default (satu per file)     | `export default class User {}`        |
| Named import     | Import dengan nama eksak           | `import { x, y } from "./utils"`      |
| Default import   | Import nilai default               | `import utils from "./utils"`         |
| `import type`    | Import hanya tipe (runtime hilang) | `import type { User } from "./types"` |
| `export type`    | Export hanya tipe                  | `export type { User }`                |
| `import * as`    | Import semua sebagai namespace     | `import * as Utils from "./utils"`    |

## Declaration & Types

| Konsep                  | Penjelasan                           | Contoh                                               |
| ----------------------- | ------------------------------------ | ---------------------------------------------------- |
| Namespace (legacy)      | Internal module (hindari, pakai ESM) | `namespace MyLib { export const x = 1 }`             |
| `.d.ts` files           | Declaration file untuk JS murni      | `declare function add(a: number, b: number): number` |
| `declare module`        | Deklarasi module eksternal           | `declare module "some-lib" { ... }`                  |
| `@types` packages       | Package type definitions             | `npm install -D @types/lodash`                       |
| Triple-slash directives | Referensi file lain (legacy)         | `/// <reference path="./types.d.ts" />`              |

```typescript
// === math.ts (export) ===
export const PI = 3.14;
export function add(a: number, b: number): number {
  return a + b;
}
export default class Calculator {
  add(a: number, b: number) {
    return a + b;
  }
}

// === app.ts (import) ===
import Calculator, { add, PI } from "./math";
import type { SomeType } from "./types";
import * as MathUtils from "./math";

console.log(add(1, 2)); // 3
console.log(PI); // 3.14
const calc = new Calculator();
console.log(MathUtils.PI); // melalui namespace import

// === types.ts (export type) ===
export interface User {
  id: number;
  name: string;
}
export type Status = "active" | "inactive";

// export type — import-only type
export type { User, Status };

// === .d.ts example (globals.d.ts) ===
declare global {
  interface Window {
    myApp: { version: string };
  }
}

// === declare module ===
declare module "my-custom-lib" {
  export function doSomething(): void;
}

// === re-export ===
export { User } from "./types";
export * from "./math";

// === import for side effects ===
import "./polyfills";
```
