# 06 - String Methods

## Informasi String

| Method          | Penjelasan                      | Contoh                            | Output |
| --------------- | ------------------------------- | --------------------------------- | ------ |
| `length`        | Panjang string (properti)       | `"Halo Dunia".length`             | `10`   |
| `charAt()`      | Ambil karakter di index         | `"JavaScript".charAt(0)`          | `"J"`  |
| `indexOf()`     | Cari posisi pertama substring   | `"Halo Dunia".indexOf("Dunia")`   | `5`    |
| `lastIndexOf()` | Cari posisi terakhir substring  | `"Belajar a".lastIndexOf("a")`    | `15`   |
| `includes()`    | Cek apakah mengandung substring | `"Belajar Java".includes("Java")` | `true` |
| `startsWith()`  | Cek awalan string               | `"JavaScript".startsWith("Java")` | `true` |
| `endsWith()`    | Cek akhiran string              | `"JavaScript".endsWith("Script")` | `true` |

## Memotong String

| Method        | Penjelasan                            | Contoh                        | Output   |
| ------------- | ------------------------------------- | ----------------------------- | -------- |
| `slice()`     | Potong string (support index negatif) | `"JavaScript".slice(0,4)`     | `"Java"` |
| `substring()` | Potong string (tidak support negatif) | `"JavaScript".substring(0,4)` | `"Java"` |
| `substr()`    | Deprecated — pakai `slice`            | `"JS".substr(1,1)`            | `"S"`    |

## Transformasi String

| Method                      | Penjelasan                             | Contoh                   | Output     |
| --------------------------- | -------------------------------------- | ------------------------ | ---------- |
| `toUpperCase()`             | Ubah ke huruf kapital                  | `"Halo".toUpperCase()`   | `"HALO"`   |
| `toLowerCase()`             | Ubah ke huruf kecil                    | `"Halo".toLowerCase()`   | `"halo"`   |
| `trim()`                    | Hapus spasi awal & akhir               | `"  Halo  ".trim()`      | `"Halo"`   |
| `trimStart()` / `trimEnd()` | Hapus spasi awal/akhir saja            | `"  Halo  ".trimStart()` | `"Halo  "` |
| `repeat()`                  | Ulang string N kali                    | `"Ha".repeat(3)`         | `"HaHaHa"` |
| `padStart()` / `padEnd()`   | Tambah padding hingga panjang tertentu | `"5".padStart(3,"0")`    | `"005"`    |

## Manipulasi String

| Method         | Penjelasan              | Contoh                                 | Output          |
| -------------- | ----------------------- | -------------------------------------- | --------------- |
| `split()`      | Pecah string jadi array | `"a,b,c".split(",")`                   | `["a","b","c"]` |
| `replace()`    | Ganti substring pertama | `"suka apel".replace("apel","mangga")` | `"suka mangga"` |
| `replaceAll()` | Ganti semua substring   | `"apel apel".replaceAll("apel","x")`   | `"x x"`         |
| `concat()`     | Gabung string           | `"Halo".concat(" ","Dunia")`           | `"Halo Dunia"`  |

## Lainnya

| Method / Fitur    | Penjelasan                               | Contoh                          | Output          |
| ----------------- | ---------------------------------------- | ------------------------------- | --------------- |
| `match()`         | Cocokkan string dengan regex             | `"25 Jan 2024".match(/\d+/g)`   | `["25","2024"]` |
| `search()`        | Cari dengan regex (return index)         | `"Belajar Java".search(/Java/)` | `8`             |
| `localeCompare()` | Bandingkan string alphabet               | `"a".localeCompare("b")`        | `-1`            |
| `charCodeAt()`    | Dapatkan kode ASCII karakter             | `"A".charCodeAt(0)`             | `65`            |
| Template Literal  | Interpolasi & multi-line dengan backtick | `` `Halo ${nama}` ``            | -               |
