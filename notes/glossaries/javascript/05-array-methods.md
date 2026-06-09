# 05 - Array Methods

## Menambah & Menghapus

| Method      | Penjelasan             | Contoh             | Output                  |
| ----------- | ---------------------- | ------------------ | ----------------------- |
| `push()`    | Tambah elemen di akhir | `[1,2].push(3)`    | `[1,2,3]`               |
| `pop()`     | Hapus elemen terakhir  | `[1,2,3].pop()`    | `3`, array jadi `[1,2]` |
| `unshift()` | Tambah elemen di awal  | `[2,3].unshift(1)` | `[1,2,3]`               |
| `shift()`   | Hapus elemen pertama   | `[1,2,3].shift()`  | `1`, array jadi `[2,3]` |

## Mengakses & Mencari

| Method        | Penjelasan                              | Contoh                                | Output |
| ------------- | --------------------------------------- | ------------------------------------- | ------ |
| `length`      | Panjang array (properti)                | `[1,2,3].length`                      | `3`    |
| `indexOf()`   | Cari index elemen                       | `["apel","mangga"].indexOf("mangga")` | `1`    |
| `includes()`  | Cek apakah array berisi nilai           | `["apel"].includes("apel")`           | `true` |
| `find()`      | Ambil elemen pertama yang lolos kondisi | `[5,12,8].find(el=>el>10)`            | `12`   |
| `findIndex()` | Index elemen pertama yang lolos kondisi | `[5,12,8].findIndex(el=>el>10)`       | `1`    |
| `some()`      | Ada minimal satu yang lolos?            | `[1,3,5,8].some(el=>el%2===0)`        | `true` |
| `every()`     | Semua elemen lolos?                     | `[2,4,6].every(el=>el%2===0)`         | `true` |

## Memotong & Menyambung

| Method     | Penjelasan                         | Contoh                         | Output           |
| ---------- | ---------------------------------- | ------------------------------ | ---------------- |
| `slice()`  | Potong array (tidak ubah asli)     | `["a","b","c","d"].slice(1,3)` | `["b","c"]`      |
| `splice()` | Hapus/tambah di tengah (ubah asli) | `[1,2,3].splice(1,1,"x")`      | jadi `[1,"x",3]` |
| `concat()` | Gabung array                       | `[1,2].concat([3,4])`          | `[1,2,3,4]`      |
| `join()`   | Gabung elemen jadi string          | `[1,2,3].join("-")`            | `"1-2-3"`        |

## Transformasi (Paling Penting!)

| Method          | Penjelasan                              | Contoh                           | Output    |
| --------------- | --------------------------------------- | -------------------------------- | --------- |
| `forEach()`     | Jalankan fungsi tiap elemen (no return) | `arr.forEach(fn)`                | -         |
| `map()`         | Buat array baru hasil transformasi      | `[1,2,3].map(n=>n*2)`            | `[2,4,6]` |
| `filter()`      | Buat array baru yang lolos kondisi      | `[1..6].filter(n=>n%2===0)`      | `[2,4,6]` |
| `reduce()`      | Reduksi array jadi satu nilai           | `[1,2,3,4].reduce((a,c)=>a+c,0)` | `10`      |
| `reduceRight()` | Sama seperti reduce (kanan ke kiri)     | `["a","b","c"].reduceRight(...)` | `"cba"`   |

## Sorting & Reverse

| Method      | Penjelasan                | Contoh              | Output    |
| ----------- | ------------------------- | ------------------- | --------- |
| `sort()`    | Urutkan array (ubah asli) | `[3,1,2].sort()`    | `[1,2,3]` |
| `reverse()` | Balik urutan (ubah asli)  | `[1,2,3].reverse()` | `[3,2,1]` |

Contoh sort angka:

```js
let angka = [5, 20, 1, 100];
angka.sort((a, b) => a - b); // ascending
console.log(angka); // [1, 5, 20, 100]
```

## Lainnya

| Method            | Penjelasan                   | Contoh                 | Output              |
| ----------------- | ---------------------------- | ---------------------- | ------------------- |
| `flat()`          | Ratakan array bertingkat     | `[1,[2,3]].flat()`     | `[1,2,3]`           |
| `fill()`          | Isi array dengan nilai       | `[1,2,3].fill(0,1,3)`  | `[1,0,0]`           |
| `Array.from()`    | Buat array dari iterable     | `Array.from("Halo")`   | `["H","a","l","o"]` |
| `Array.isArray()` | Cek apakah suatu nilai array | `Array.isArray([1,2])` | `true`              |
