# 13 - Timers & Console

## Timers

| Fungsi                | Penjelasan                        | Contoh                                      |
| --------------------- | --------------------------------- | ------------------------------------------- |
| `setTimeout(fn, ms)`  | Jalankan sekali setelah delay     | `setTimeout(() => console.log("ok"), 2000)` |
| `clearTimeout(id)`    | Batalkan setTimeout               | `clearTimeout(timeoutId)`                   |
| `setInterval(fn, ms)` | Jalankan berulang setiap interval | `setInterval(() => count++, 1000)`          |
| `clearInterval(id)`   | Hentikan setInterval              | `clearInterval(intervalId)`                 |

Contoh:

```js
console.log("Mulai");
setTimeout(() => {
  console.log("Jalan setelah 2 detik");
}, 2000);
console.log("Selesai");
// Output: "Mulai", "Selesai", (2 detik) "Jalan setelah 2 detik"

let count = 0;
const intervalId = setInterval(() => {
  count++;
  console.log("Detik ke-" + count);
  if (count >= 5) clearInterval(intervalId);
}, 1000);
```

## Console

| Method                         | Penjelasan                     | Contoh                                         |
| ------------------------------ | ------------------------------ | ---------------------------------------------- |
| `console.log()`                | Cetak pesan                    | `console.log("Halo", 123, {a:1})`              |
| `console.error()`              | Cetak error (merah)            | `console.error("Terjadi error!")`              |
| `console.warn()`               | Cetak peringatan (kuning)      | `console.warn("Peringatan!")`                  |
| `console.info()`               | Cetak informasi                | `console.info("Info penting")`                 |
| `console.table()`              | Tampilkan sebagai tabel        | `console.table(users)`                         |
| `console.group()`              | Kelompokkan log (nested)       | `console.group("Label")`                       |
| `console.time()` / `timeEnd()` | Ukur waktu eksekusi            | `console.time("id")` / `console.timeEnd("id")` |
| `console.count()`              | Hitung berapa kali dipanggil   | `console.count("label")`                       |
| `console.assert()`             | Cetak error jika kondisi false | `console.assert(x>10, "msg")`                  |
| `console.clear()`              | Bersihkan console              | `console.clear()`                              |
| `console.trace()`              | Tampilkan stack trace          | `console.trace("Dari mana?")`                  |
| `console.dir()`                | Tampilkan object sebagai tree  | `console.dir(document.body)`                   |
