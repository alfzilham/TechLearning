# 03 - Conditionals & Loops

## Conditionals

| Statement                 | Penjelasan                           | Contoh                     | Output           |
| ------------------------- | ------------------------------------ | -------------------------- | ---------------- |
| `if` / `else if` / `else` | Menjalankan kode berdasarkan kondisi | `nilai=85; if(nilai>=80)`  | `"B"`            |
| `switch`                  | Percabangan berdasarkan nilai tetap  | `switch("senin")`          | `"Mulai kerja!"` |
| Ternary `?:`              | If-else satu baris                   | `umur>=17?"Dewasa":"Anak"` | `"Dewasa"`       |

Contoh:

```js
let nilai = 85;
if (nilai >= 90) console.log("A");
else if (nilai >= 80) console.log("B");
else console.log("C");
```

## Loops (Perulangan)

| Loop         | Penjelasan                        | Contoh                   | Output             |
| ------------ | --------------------------------- | ------------------------ | ------------------ |
| `for`        | Perulangan dengan counter         | `for(let i=0; i<3; i++)` | `0, 1, 2`          |
| `while`      | Loop selama kondisi true          | `while(i<3)`             | `0, 1, 2`          |
| `do...while` | Loop minimal sekali               | `do{...} while(i<3)`     | `0, 1, 2`          |
| `for...of`   | Loop array/iterable (ambil value) | `for(let item of buah)`  | `"apel", "mangga"` |
| `for...in`   | Loop object/array (ambil key)     | `for(let key in user)`   | `"nama: Rizky"`    |

Contoh:

```js
let buah = ["apel", "mangga", "jeruk"];
for (let item of buah) console.log(item);
```

## Kontrol Loop

| Keyword    | Penjelasan                   | Contoh               | Output      |
| ---------- | ---------------------------- | -------------------- | ----------- |
| `break`    | Menghentikan loop sepenuhnya | `if(i===5) break`    | `0,1,2,3,4` |
| `continue` | Lewati iterasi saat ini      | `if(i===2) continue` | `0,1,3,4`   |
