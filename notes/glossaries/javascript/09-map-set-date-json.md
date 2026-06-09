# 09 - Map, Set, Date, JSON

## Map

| Method / Properti | Penjelasan                   | Contoh            | Output |
| ----------------- | ---------------------------- | ----------------- | ------ |
| `new Map()`       | Map dengan key bisa apa saja | `new Map()`       | -      |
| `map.set(k, v)`   | Tambah/update entry          | `map.set("a", 1)` | -      |
| `map.get(k)`      | Ambil value berdasarkan key  | `map.get("a")`    | `1`    |
| `map.has(k)`      | Cek apakah key ada           | `map.has("a")`    | `true` |
| `map.delete(k)`   | Hapus entry                  | `map.delete("a")` | -      |
| `map.size`        | Jumlah entry (properti)      | `map.size`        | `2`    |
| `map.clear()`     | Hapus semua entry            | `map.clear()`     | -      |

Contoh:

```js
let map = new Map();
map.set("nama", "Rizky");
map.set(123, "Number key");
console.log(map.get("nama")); // "Rizky"
console.log(map.has(123)); // true
```

## Set

| Method / Properti | Penjelasan                         | Contoh             | Output     |
| ----------------- | ---------------------------------- | ------------------ | ---------- |
| `new Set()`       | Simpan nilai unik (tanpa duplikat) | `new Set([1,1,2])` | `Set{1,2}` |
| `set.add(v)`      | Tambah nilai                       | `set.add(1)`       | -          |
| `set.has(v)`      | Cek apakah nilai ada               | `set.has(2)`       | `true`     |
| `set.delete(v)`   | Hapus nilai                        | `set.delete(2)`    | -          |
| `set.size`        | Jumlah nilai unik                  | `set.size`         | `3`        |
| `set.clear()`     | Hapus semua nilai                  | `set.clear()`      | -          |

Contoh:

```js
let set = new Set([1, 2, 3, 3, 4, 4, 5]);
console.log([...set]); // [1, 2, 3, 4, 5]
```

## Date

| Method                                         | Penjelasan                  | Contoh                             | Output              |
| ---------------------------------------------- | --------------------------- | ---------------------------------- | ------------------- |
| `new Date()`                                   | Buat objek tanggal/waktu    | `new Date()`                       | waktu sekarang      |
| `getFullYear()`                                | Tahun                       | `date.getFullYear()`               | `2024`              |
| `getMonth()`                                   | Bulan (0=Jan)               | `date.getMonth()`                  | `0`                 |
| `getDate()`                                    | Tanggal                     | `date.getDate()`                   | `15`                |
| `getDay()`                                     | Hari (0=Minggu)             | `date.getDay()`                    | `1`                 |
| `getHours()` / `getMinutes()` / `getSeconds()` | Jam / menit / detik         | -                                  | -                   |
| `getTime()`                                    | Timestamp ms sejak 1970     | `date.getTime()`                   | -                   |
| `setFullYear()` / `setMonth()` / `setDate()`   | Set tahun / bulan / tanggal | `date.setFullYear(2025)`           | -                   |
| `toDateString()`                               | Format tanggal readable     | `date.toDateString()`              | `"Mon Jan 15 2024"` |
| `toISOString()`                                | Format ISO                  | `date.toISOString()`               | `"2024-01-15T..."`  |
| `toLocaleDateString()`                         | Format lokal                | `date.toLocaleDateString("id-ID")` | `"15/1/2024"`       |

Contoh:

```js
let date = new Date(2024, 0, 15, 9, 30, 45);
console.log(date.getFullYear()); // 2024
console.log(date.getMonth()); // 0 (Januari)
console.log(date.getDate()); // 15
```

## JSON

| Method             | Penjelasan                    | Contoh                  | Output      |
| ------------------ | ----------------------------- | ----------------------- | ----------- |
| `JSON.stringify()` | Object/array jadi string JSON | `JSON.stringify({a:1})` | `'{"a":1}'` |
| `JSON.parse()`     | String JSON jadi object/array | `JSON.parse('{"a":1}')` | `{a:1}`     |
