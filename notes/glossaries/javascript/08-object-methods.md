# 08 - Object & Object Methods

## Object Basics

| Cara           | Penjelasan                      | Contoh                                       |
| -------------- | ------------------------------- | -------------------------------------------- |
| Object Literal | Cara paling umum membuat object | `let user = { nama: "Rizky", umur: 25 }`     |
| Akses properti | Dot notation atau bracket       | `user.nama` atau `user["nama"]`              |
| Ubah / Tambah  | Assign nilai ke properti        | `user.umur = 26` atau `user["kota"] = "Jkt"` |

## Object Methods (Static)

| Method                 | Penjelasan                                      | Contoh                          | Output      |
| ---------------------- | ----------------------------------------------- | ------------------------------- | ----------- |
| `Object.keys()`        | Array berisi semua key                          | `Object.keys({a:1,b:2})`        | `["a","b"]` |
| `Object.values()`      | Array berisi semua value                        | `Object.values({a:1,b:2})`      | `[1,2]`     |
| `Object.entries()`     | Array [key, value] tiap properti                | `Object.entries({a:1})`         | `[["a",1]]` |
| `Object.assign()`      | Salin properti ke target                        | `Object.assign({a:1},{b:2})`    | `{a:1,b:2}` |
| `Object.freeze()`      | Bekukan object (tak bisa diubah)                | `Object.freeze({nama:"Rizky"})` | -           |
| `Object.seal()`        | Segel (properti bisa diubah, tak bisa ditambah) | `Object.seal({nama:"Rizky"})`   | -           |
| `Object.hasOwn()`      | Cek properti milik sendiri (bukan warisan)      | `hasOwn(user,"nama")`           | `true`      |
| `Object.fromEntries()` | Array [key,value] jadi object                   | `fromEntries([["a",1]])`        | `{a:1}`     |

## Destructuring & Spread

| Teknik        | Penjelasan                          | Contoh                    | Output               |
| ------------- | ----------------------------------- | ------------------------- | -------------------- |
| Destructuring | Ambil properti ke variable terpisah | `let {nama, umur} = user` | -                    |
| Spread `...`  | Salin/gabung object                 | `{...user, kota:"Jkt"}`   | `{nama, umur, kota}` |

Contoh:

```js
let user = { nama: "Rizky", umur: 25 };
let { nama, umur } = user;
console.log(nama); // "Rizky"

let detail = { ...user, kota: "Jakarta" };
console.log(detail); // { nama: "Rizky", umur: 25, kota: "Jakarta" }
```

## Lainnya

| Fitur                 | Penjelasan                        | Contoh                      |
| --------------------- | --------------------------------- | --------------------------- |
| `in` operator         | Cek apakah properti ada di object | `"nama" in user` => `true`  |
| `delete`              | Hapus properti                    | `delete user.umur`          |
| Computed Property Key | Key dinamis dengan bracket        | `{[key]: "Rizky"}`          |
| Shorthand Property    | Jika nama variable = key          | `let user = { nama, umur }` |
