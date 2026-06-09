# 01 - Tipe Data & Variable

## Variable Declaration

| Keyword | Penjelasan                            | Contoh                                  | Output |
| ------- | ------------------------------------- | --------------------------------------- | ------ |
| `var`   | Function-scoped, bisa di-redeclare    | `var nama = "Rizky"; var nama = "Budi"` | -      |
| `let`   | Block-scoped, tidak bisa di-redeclare | `let umur = 25; umur = 30`              | -      |
| `const` | Block-scoped, tidak bisa reassign     | `const phi = 3.14`                      | -      |

Contoh lengkap:

```js
var nama = "Rizky";
var nama = "Budi"; // bisa redeclare
console.log(nama); // "Budi"

let umur = 25;
umur = 30;

const phi = 3.14;
```

## Tipe Data Primitif

| Tipe        | Penjelasan                                | Contoh                         | Output        |
| ----------- | ----------------------------------------- | ------------------------------ | ------------- |
| `string`    | Teks, diapit kutip tunggal/ganda/backtick | `` `Halo ${nama}` ``           | `"Halo Budi"` |
| `number`    | Angka integer dan desimal                 | `let x = 3.14`                 | -             |
| `boolean`   | Nilai `true` atau `false`                 | `let isActive = true`          | -             |
| `null`      | Nilai kosong yang disengaja               | `let data = null`              | -             |
| `undefined` | Variable belum diberi nilai               | `let sesuatu`                  | `undefined`   |
| `BigInt`    | Angka besar melebihi batas Number         | `123...90n`                    | -             |
| `Symbol`    | Nilai unik untuk key object               | `Symbol("id") == Symbol("id")` | `false`       |

## Pengecekan Tipe

| Method            | Penjelasan                         | Contoh                   | Output     |
| ----------------- | ---------------------------------- | ------------------------ | ---------- |
| `typeof`          | Mengecek tipe data nilai           | `typeof "Halo"`          | `"string"` |
| `Array.isArray()` | Mengecek apakah nilai adalah array | `Array.isArray([1,2,3])` | `true`     |

## Konversi Tipe

| Fungsi      | Penjelasan                     | Contoh          | Output  |
| ----------- | ------------------------------ | --------------- | ------- |
| `String()`  | Mengubah nilai menjadi string  | `String(123)`   | `"123"` |
| `Number()`  | Mengubah nilai menjadi number  | `Number("123")` | `123`   |
| `Boolean()` | Mengubah nilai menjadi boolean | `Boolean(1)`    | `true`  |
