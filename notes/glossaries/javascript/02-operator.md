# 02 - Operator

## Aritmatika

| Operator | Penjelasan                  | Contoh   | Output     |
| -------- | --------------------------- | -------- | ---------- |
| `+`      | Penjumlahan / concat string | `5 + 3`  | `8`        |
| `-`      | Pengurangan                 | `10 - 4` | `6`        |
| `*`      | Perkalian                   | `5 * 3`  | `15`       |
| `/`      | Pembagian                   | `10 / 3` | `3.333...` |
| `%`      | Modulus (sisa bagi)         | `10 % 3` | `1`        |
| `**`     | Eksponen / pangkat          | `2 ** 3` | `8`        |

## Perbandingan

| Operator                | Penjelasan                   | Contoh      | Output  |
| ----------------------- | ---------------------------- | ----------- | ------- |
| `==`                    | Sama (loose, tipe diabaikan) | `5 == "5"`  | `true`  |
| `===`                   | Sama (strict, nilai + tipe)  | `5 === "5"` | `false` |
| `!=`                    | Tidak sama (loose)           | `5 != "5"`  | `false` |
| `!==`                   | Tidak sama (strict)          | `5 !== "5"` | `true`  |
| `>` / `<` / `>=` / `<=` | Lebih besar / kecil / dll    | `5 > 3`     | `true`  |

## Logika

| Operator | Penjelasan                      | Contoh                     | Output |
| -------- | ------------------------------- | -------------------------- | ------ |
| `&&`     | AND — true jika kedua sisi true | `umur >= 17 && punyaSIM`   | `true` |
| `\|\|`   | OR — true jika salah satu true  | `cash > 0 \|\| credit > 0` | `true` |
| `!`      | NOT — membalik boolean          | `!false`                   | `true` |

## Penugasan

| Operator | Penjelasan         | Contoh   | Nilai akhir |
| -------- | ------------------ | -------- | ----------- |
| `=`      | Assign nilai       | `a = 10` | `10`        |
| `+=`     | Tambah lalu assign | `a += 5` | `15`        |
| `-=`     | Kurang lalu assign | `a -= 3` | `12`        |
| `*=`     | Kali lalu assign   | `a *= 2` | `24`        |
| `/=`     | Bagi lalu assign   | `a /= 4` | `6`         |

## Khusus JavaScript

| Operator     | Penjelasan                                                | Contoh                           | Output      |
| ------------ | --------------------------------------------------------- | -------------------------------- | ----------- |
| `??`         | Nullish coalescing — ambil kanan jika kiri null/undefined | `null ?? "Tamu"`                 | `"Tamu"`    |
| `?.`         | Optional chaining — akses properti aman                   | `user?.alamat?.kota`             | `undefined` |
| `...`        | Spread / Rest — menyebar array/object                     | `[...[1,2], 3]`                  | `[1,2,3]`   |
| `typeof`     | Mengecek tipe data                                        | `typeof 42`                      | `"number"`  |
| `instanceof` | Cek instance dari class                                   | `new Date() instanceof Date`     | `true`      |
| `delete`     | Hapus properti object                                     | `delete user.umur`               | -           |
| `?:`         | Ternary — if-else satu baris                              | `umur >= 17 ? "Dewasa" : "Anak"` | `"Dewasa"`  |
| `++` / `--`  | Increment / Decrement 1                                   | `let c=0; c++`                   | `1`         |

Contoh spread:

```js
let arr1 = [1, 2, 3];
let arr2 = [...arr1, 4, 5];
console.log(arr2); // [1, 2, 3, 4, 5]

let obj1 = { a: 1, b: 2 };
let obj2 = { ...obj1, c: 3 };
console.log(obj2); // { a: 1, b: 2, c: 3 }
```
