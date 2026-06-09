# 04 - Functions

## Deklarasi Function

| Jenis                | Penjelasan                                  | Contoh                           | Output |
| -------------------- | ------------------------------------------- | -------------------------------- | ------ |
| Function Declaration | Bisa dipanggil sebelum deklarasi (hoisting) | `function sapa(n){return"Halo"}` | -      |
| Function Expression  | Disimpan ke variable, tidak hoisted         | `const sapa = function(n){...}`  | -      |
| Arrow Function `=>`  | Singkat, tidak punya `this` sendiri         | `const dbl=x=>x*2`               | -      |

Contoh:

```js
function sapa(nama) {
  return "Halo, " + nama + "!";
}
console.log(sapa("Rizky")); // "Halo, Rizky!"

const kaliDua = (x) => x * 2;
console.log(kaliDua(5)); // 10
```

## Parameter Khusus

| Jenis                    | Penjelasan                        | Contoh                    | Output         |
| ------------------------ | --------------------------------- | ------------------------- | -------------- |
| Default Parameter        | Nilai default jika argumen kosong | `sapa()` (default="Tamu") | `"Halo, Tamu"` |
| Rest Parameter `...args` | Kumpulkan sisa argumen ke array   | `jumlahkan(1,2,3,4)`      | `10`           |

## Function Khusus

| Jenis        | Penjelasan                                 | Contoh                      |
| ------------ | ------------------------------------------ | --------------------------- |
| IIFE         | Function langsung jalan saat didefinisikan | `(function(){...})()`       |
| Callback     | Function dikirim sebagai argumen           | `proses("Rizky", callback)` |
| Higher-Order | Menerima/mengembalikan function lain       | `buatPengali(3)(5)` => `15` |
| Recursive    | Memanggil dirinya sendiri                  | `faktorial(5)` => `120`     |

Contoh:

```js
// IIFE
(function () {
  console.log("Jalan otomatis!");
})();

// Callback
function proses(nama, callback) {
  callback("Halo " + nama);
}
proses("Rizky", (pesan) => console.log(pesan));

// Recursive
function faktorial(n) {
  if (n <= 1) return 1;
  return n * faktorial(n - 1);
}
console.log(faktorial(5)); // 120

// Higher-Order
function buatPengali(pengali) {
  return (angka) => angka * pengali;
}
const kali3 = buatPengali(3);
console.log(kali3(5)); // 15
```

## Method di Object

| Cara             | Penjelasan                       | Contoh        | Output               |
| ---------------- | -------------------------------- | ------------- | -------------------- |
| Method shorthand | Function sebagai properti object | `user.sapa()` | `"Halo, saya Rizky"` |

```js
const user = {
  nama: "Rizky",
  sapa() {
    return "Halo, saya " + this.nama;
  },
};
console.log(user.sapa()); // "Halo, saya Rizky"
```
