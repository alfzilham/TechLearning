# 07 - Number & Math

## Number Methods

| Method          | Penjelasan                                 | Contoh                     | Output    |
| --------------- | ------------------------------------------ | -------------------------- | --------- |
| `Number()`      | Ubah nilai jadi number                     | `Number("123")`            | `123`     |
| `parseInt()`    | Ubah string jadi integer                   | `parseInt("100px")`        | `100`     |
| `parseFloat()`  | Ubah string jadi float                     | `parseFloat("3.14")`       | `3.14`    |
| `toFixed()`     | Bulatkan ke jumlah desimal (return string) | `(3.14159).toFixed(2)`     | `"3.14"`  |
| `toPrecision()` | Bulatkan ke total digit (return string)    | `(123.456).toPrecision(4)` | `"123.5"` |
| `toString()`    | Ubah number jadi string                    | `(255).toString(16)`       | `"ff"`    |
| `isNaN()`       | Cek apakah NaN                             | `isNaN("abc")`             | `true`    |
| `isFinite()`    | Cek apakah nilai finite                    | `isFinite(1/0)`            | `false`   |

## Math Object

| Method                      | Penjelasan                     | Contoh                | Output       |
| --------------------------- | ------------------------------ | --------------------- | ------------ |
| `Math.round()`              | Bulatkan ke terdekat           | `Math.round(3.5)`     | `4`          |
| `Math.floor()`              | Bulatkan ke bawah              | `Math.floor(3.9)`     | `3`          |
| `Math.ceil()`               | Bulatkan ke atas               | `Math.ceil(3.1)`      | `4`          |
| `Math.trunc()`              | Potong desimal (buang pecahan) | `Math.trunc(3.9)`     | `3`          |
| `Math.random()`             | Angka acak 0-1                 | `Math.random()`       | `0.473`      |
| `Math.max()` / `Math.min()` | Nilai terbesar / terkecil      | `Math.max(1,5,3,9,2)` | `9`          |
| `Math.abs()`                | Nilai absolut                  | `Math.abs(-5)`        | `5`          |
| `Math.pow()`                | Perpangkatan                   | `Math.pow(2,3)`       | `8`          |
| `Math.sqrt()`               | Akar kuadrat                   | `Math.sqrt(25)`       | `5`          |
| `Math.PI`                   | Konstanta phi (π)              | `Math.PI`             | `3.14159...` |

Contoh random 1-10:

```js
let acak = Math.floor(Math.random() * 10) + 1;
console.log(acak); // misal: 7
```

## Nilai Spesial

| Nilai      | Penjelasan    | Contoh                |
| ---------- | ------------- | --------------------- |
| `Infinity` | Tak terhingga | `1 / 0` => `Infinity` |
| `NaN`      | Not a Number  | `"abc" * 2` => `NaN`  |
