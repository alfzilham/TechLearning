# 11 - ES6+ Modern JavaScript

## Variable (ES6)

| Keyword | Penjelasan           | Contoh               |
| ------- | -------------------- | -------------------- |
| `let`   | Variable bisa diubah | `let x = 10; x = 20` |
| `const` | Variable tetap       | `const y = 10`       |

## Arrow Function (ES6)

| Bentuk                    | Contoh                               |
| ------------------------- | ------------------------------------ |
| Single param, single line | `const dbl = x => x * 2`             |
| Multi param               | `const add = (a,b) => a + b`         |
| Multi baris               | `const fn = (x) => { return x * 2 }` |

## Template Literal (ES6)

| Fitur       | Penjelasan             | Contoh                 |
| ----------- | ---------------------- | ---------------------- |
| Interpolasi | Expression dalam `${}` | `` `Halo ${nama}` ``   |
| Multi-line  | String banyak baris    | `` `Baris1\nBaris2` `` |

## Destructuring (ES6)

| Jenis         | Penjelasan                   | Contoh                            |
| ------------- | ---------------------------- | --------------------------------- |
| Array         | Ambil elemen ke variable     | `let [a,b] = [1,2]`               |
| Array skip    | Lewati elemen                | `let [a,,c] = [1,2,3]`            |
| Array swap    | Tukar variable               | `[a,b] = [b,a]`                   |
| Object        | Ambil properti ke variable   | `let {nama, umur} = user`         |
| Object rename | Ganti nama variable          | `let {nama: fullName} = user`     |
| Default value | Nilai default jika undefined | `let {hobi = "Tidak ada"} = user` |

## Spread & Rest (ES6)

| Operator            | Penjelasan             | Contoh                  | Output    |
| ------------------- | ---------------------- | ----------------------- | --------- |
| `...` spread array  | Sebar array            | `[...[1,2], 3]`         | `[1,2,3]` |
| `...` spread object | Sebar object           | `{...a, ...b}`          | -         |
| `...` rest param    | Kumpulkan sisa argumen | `function sum(...args)` | -         |

Contoh:

```js
let arr1 = [1, 2, 3];
let arr2 = [...arr1, 4, 5];
console.log(arr2); // [1, 2, 3, 4, 5]

let user = { nama: "Rizky", umur: 25 };
let detail = { ...user, kota: "Jakarta" };
```

## Default Parameter (ES6)

| Penjelasan                        | Contoh                | Output        |
| --------------------------------- | --------------------- | ------------- |
| Nilai default jika argumen kosong | `sapa(nama = "Tamu")` | `"Halo Tamu"` |

## Optional Chaining (ES2020)

| Operator | Penjelasan                              | Contoh               | Output      |
| -------- | --------------------------------------- | -------------------- | ----------- |
| `?.`     | Akses properti aman dari null/undefined | `user?.alamat?.kota` | `undefined` |

## Nullish Coalescing (ES2020)

| Operator | Penjelasan                           | Contoh              | Output      |
| -------- | ------------------------------------ | ------------------- | ----------- |
| `??`     | Ambil kanan jika kiri null/undefined | `null ?? "Default"` | `"Default"` |

## Promise & Async

| Method                 | Penjelasan                          | Contoh                              |
| ---------------------- | ----------------------------------- | ----------------------------------- |
| `Promise`              | Tangani operasi async               | `new Promise((res,rej) => {...})`   |
| `Promise.all()`        | Jalankan multiple promise paralel   | `Promise.all([p1, p2])`             |
| `Promise.race()`       | Ambil yang selesai paling cepat     | `Promise.race([p1, p2])`            |
| `Promise.allSettled()` | Tunggu semua selesai (sukses/gagal) | `Promise.allSettled([p1, p2])`      |
| `async / await`        | Cara bersih menulis Promise         | `async function fn() { await ... }` |

## Class (ES6)

| Fitur     | Penjelasan                    | Contoh                                     |
| --------- | ----------------------------- | ------------------------------------------ |
| `class`   | Blueprint untuk object        | `class Animal { constructor(nama) {...} }` |
| `extends` | Inheritance / turunan         | `class Kucing extends Animal {}`           |
| `super()` | Panggil constructor parent    | `super(nama)`                              |
| `static`  | Method class (tanpa instance) | `static info() {...}`                      |

## Modules (ES6)

| Keyword          | Penjelasan           | Contoh                                  |
| ---------------- | -------------------- | --------------------------------------- |
| `export`         | Ekspor dari file     | `export const PI = 3.14`                |
| `export default` | Ekspor default       | `export default function fn(){}`        |
| `import`         | Impor dari file lain | `import sapa, { PI } from "./utils.js"` |

## Shortcuts

| Operator             | Penjelasan                 | Contoh                         | Output |
| -------------------- | -------------------------- | ------------------------------ | ------ |
| `&&` untuk render    | Jalan jika truthy          | `isLogin && console.log("ok")` | -      |
| `\|\|` untuk default | Ambil kanan jika falsy     | `0 \|\| 100`                   | `100`  |
| Shorthand property   | Jika nama = key            | `let user = { nama }`          | -      |
| Method shorthand     | `sapa() {}` di object      | `{ sapa() { return "Hi" } }`   | -      |
| `??=`                | Assign jika null/undefined | `x ??= "default"`              | -      |
| `&&=`                | Assign AND                 | `a &&= false`                  | -      |
| `\|\|=`              | Assign OR                  | `b \|\|= true`                 | -      |
