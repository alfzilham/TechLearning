# Phase 2: JavaScript Fundamental

**Durasi:** 14 hari (Minggu 2-3)
**Tujuan:** Membuat aplikasi interaktif (Todo List + Fetch API) tanpa framework

---

## Kenapa JavaScript?

JavaScript adalah otak dari web. HTML cuma struktur, CSS cuma tampilan. JavaScript yang bikin web jadi *hidup*. Sebelum menyentuh React atau TypeScript, Anda harus paham JavaScript murni dulu.

---

## Minggu 2: Dasar-Dasar JS

### Hari 1: Variables & Data Types

**Konsep:**
- `console.log()` — cara debugging paling dasar
- `let`, `const` (kenapa `var` sudah ditinggalkan)
- Data types: `string`, `number`, `boolean`, `null`, `undefined`, `object`
- `typeof` operator
- String concatenation vs template literals (`` `Hello ${name}` ``)
- Basic operators: `+`, `-`, `*`, `/`, `%`, `**`
- Comparison: `===` vs `==`, `!==`, `>`, `<`
- Logical: `&&`, `||`, `!`

**Tugas:**
```js
// Buka browser console (F12) atau buat file .js dan jalanin pake Node
// 1. Buat variable nama, umur, statusMenikah
// 2. Cetak "Halo, nama saya [nama]. Umur saya [umur] tahun."
// 3. Buat program cek: jika umur >= 17, cetak "Sudah dewasa", jika tidak "Masih anak-anak"
// 4. Buat program yang menghasilkan true/false: "Apakah nama Anda lebih dari 5 karakter?"
```

---

### Hari 2: Functions & Scope

**Konsep:**
- Function declaration: `function nama() {}`
- Function expression: `const nama = function() {}`
- Arrow function: `const nama = () => {}`
- Parameters & arguments
- Return value (fungsi TANPA return mengembalikan `undefined`)
- Scope: global vs local (`{}` block scope)
- Hoisting (function declaration di-hoist, expression tidak)

**Tugas:**
```js
// 1. Buat function hitungLuasPersegi(sisi) yang return sisi * sisi
// 2. Buat function greet(nama) yang return "Halo, {nama}!"
// 3. Buat function cekGenap(angka) yang return true jika genap
// 4. Buat arrow function kali(a, b) => a * b
// 5. Panggil semua function dan console.log hasilnya
```

---

### Hari 3: Conditional & Looping

**Konsep:**
- `if`, `else if`, `else`
- Ternary: `kondisi ? nilaiTrue : nilaiFalse`
- `switch` (kapan berguna)
- `for` loop: `for (let i = 0; i < 10; i++)`
- `while` loop
- `break` dan `continue`

**Tugas:**
```js
// 1. Buat function nilaiGrade(nilai) yang return "A"/"B"/"C"/"D"/"E" berdasarkan range nilai
// 2. Cetak angka 1-100, tapi untuk kelipatan 3 cetak "Fizz", 5 cetak "Buzz",
//    kelipatan 3 dan 5 cetak "FizzBuzz" (FizzBuzz test)
// 3. Buat function printBintang(n) yang cetak:
//    *
//    **
//    ***
//    ****
```

---

### Hari 4: Objects

**Konsep:**
- Object literal: `const user = { name: 'John', age: 25 }`
- Access: dot notation (`user.name`) vs bracket (`user['name']`)
- Add/update/delete property
- Nested object
- `this` keyword di dalam method
- Object destructuring: `const { name, age } = user`
- Spread operator: `const newUser = { ...user, city: 'Jakarta' }`
- `Object.keys()`, `Object.values()`, `Object.entries()`

**Tugas:**
```js
// 1. Buat object 'buku' dengan properti: judul, penulis, tahun, genre, harga
// 2. Tambah method getInfo() yang return string dengan info lengkap buku
// 3. Buat array of objects 'daftarBuku' dengan 5 buku
// 4. Looping daftarBuku dan cetak judul + penulis setiap buku
```

---

### Hari 5: Arrays & High-Order Functions

**Konsep:**
- Array methods: `push`, `pop`, `shift`, `unshift`, `slice`, `splice`
- Looping: `for`, `forEach`
- Transform: `map()`
- Filter: `filter()`
- Reduce: `reduce()` (akumulasi)
- Find: `find()`, `findIndex()`
- `some()`, `every()`
- Array destructuring: `const [a, b] = [1, 2]`

**Tugas:**
```js
const angka = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// 1. Gunakan map untuk menggandakan setiap angka
// 2. Gunakan filter untuk ambil angka genap saja
// 3. Gunakan reduce untuk jumlah semua angka
// 4. Buat array of objects orang = [{nama, umur, kota}, ...]
// 5. Filter orang yang umur > 25
// 6. Map untuk ambil daftar nama saja
```

---

### Hari 6: DOM Manipulation

**Konsep:**
- `document.querySelector()`, `document.querySelectorAll()`
- `document.getElementById()`, `document.getElementsByClassName()`
- Mengubah content: `.textContent`, `.innerHTML`
- Mengubah style: `.style.property = 'value'`
- Add/remove class: `.classList.add()`, `.remove()`, `.toggle()`
- Create element: `document.createElement()`, `.appendChild()`
- Remove element: `.remove()`

**Tugas:**
```html
<!-- Buat file index.html dengan: -->
<button id="addCard">Tambah Card</button>
<div id="container"></div>

<script>
// 1. Saat button diklik, tambah card baru ke container
// 2. Setiap card berisi: judul, deskripsi, tombol hapus
// 3. Tombol hapus menghapus card tersebut
</script>
```

---

### Hari 7: Events

**Konsep:**
- `.addEventListener('click', handler)`
- Event types: `click`, `submit`, `input`, `change`, `keydown`, `keyup`, `mouseover`
- Event object (`event.target`, `event.preventDefault()`)
- Event delegation (event bubbling)
- Form submission: `form.addEventListener('submit', handler)`

**Tugas:**
Buat halaman dengan:
- Form input nama + tombol submit
- Saat submit, nama muncul di list di bawah form
- Tombol hapus di setiap item list
- Input kosong setelah submit
- Form tidak boleh submit kalo input kosong (validasi)

---

## Minggu 3: Intermediate JS

### Hari 8: Async JavaScript — Callback & Promise

**Konsep:**
- Synchronous vs Asynchronous
- `setTimeout()`, `setInterval()`
- Callback hell (kenapa ini masalah)
- `Promise`: `resolve`, `reject`, `.then()`, `.catch()`, `.finally()`
- `Promise.all()`, `Promise.race()`

**Tugas:**
```js
// 1. Buat function delay(ms) yang return Promise yang resolve setelah ms milidetik
// 2. Simulasi: ambil data user (1 detik), lalu ambil data post (1 detik setelahnya)
//    pake Promise chain (.then)
// 3. Buat Promise yang random: 50% resolve "Berhasil", 50% reject "Gagal"
```

---

### Hari 9: Async/Await & Fetch API

**Konsep:**
- `async function`, `await`
- Error handling: `try {} catch {}` + `finally {}`
- `fetch()`: GET data dari API
- Response: `response.json()`, `response.ok`, `response.status`
- Loading state, error state, empty state

**Tugas:**
```js
// 1. Fetch dari https://jsonplaceholder.typicode.com/posts
// 2. Tampilkan 10 post pertama di console
// 3. Bikin fungsi async getPost(id) yang ambil 1 post
// 4. Error handling: kalo fetch gagal, tampilkan pesan error
```

---

### Hari 10: DOM + Fetch — API Explorer

**Tugas Final Hari Ini:**
Buat halaman HTML yang:

1. **Fetch data** dari `https://jsonplaceholder.typicode.com/users`
2. **Render** setiap user sebagai card (nama, email, perusahaan, kota)
3. **Search bar** untuk filter user berdasarkan nama
4. **Klik card** → tampilkan detail user (modal atau section terpisah)
5. **Loading state** saat fetching
6. **Error state** kalo fetch gagal

**Teknis:**
- Semua JS murni (no framework)
- DOM manipulation untuk render
- `async/await` untuk fetch
- `try/catch` untuk error handling

---

### Hari 11: ES6+ Features

**Konsep:**
- Spread & Rest operator (`...`)
- Default parameter: `function greet(nama = 'Tamu')`
- Optional chaining: `user?.address?.city`
- Nullish coalescing: `const name = input ?? 'Default'`
- Short-circuit: `const name = input || 'Default'` (bedanya dengan ??)
- `import` / `export` (ES modules)
- Modules: file `.js` bisa `export` dan `import`

---

### Hari 12: Local Storage & Data Persistence

**Konsep:**
- `localStorage.setItem()`, `.getItem()`, `.removeItem()`, `.clear()`
- `JSON.stringify()` — convert object ke string
- `JSON.parse()` — convert string ke object
- Keterbatasan localStorage: synchronous, 5-10MB, string only

**Tugas:**
Modifikasi Todo List (hari 7):
- Todo tersimpan di localStorage
- Saat halaman di-refresh, todo tetap ada
- Fitur: tambah, hapus, toggle selesai

---

### Hari 13: Mini Project — Todo List App Lengkap

**Spesifikasi:**
Buat Todo List App dengan fitur:

1. **Tambah todo** (form input + submit)
2. **Hapus todo** (tombol hapus per item)
3. **Toggle selesai** (coret text kalo selesai)
4. **Filter**: All / Active / Completed
5. **Counter**: "3 items left"
6. **Clear completed**: hapus semua yang sudah selesai
7. **Local storage**: data tetap ada setelah refresh
8. **Styled dengan CSS** (pakai yang sudah dipelajari di Phase 1)

**DILARANG:**
- Framework/Library
- Copy-paste dari internet

---

### Hari 14: JavaScript Fundamentals — Review & Final Test

**Tes Akhir (Tanpa bantuan siapa pun):**

```js
// 1. TULIS fungsi yang menerima array angka dan return array berisi angka genap saja
// 2. TULIS fungsi yang menerima array of objects {nama, nilai} dan return rata-rata nilai
// 3. JELASKAN perbedaan let, const, var
// 4. JELASKAN apa itu closure (tanpa lihat catatan)
// 5. JELASKAN cara kerja Promise dan async/await
```

**Jika semua bisa dijawab tanpa lihat catatan, Anda siap lanjut ke TypeScript.**

---

## Referensi

- [MDN: JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [javascript.info](https://javascript.info/) — tutorial JS paling komprehensif
- [JS Fiddle / CodePen](https://codepen.io/) — playground
- [JSONPlaceholder](https://jsonplaceholder.typicode.com/) — free fake API untuk latihan

## Checklist Penguasaan

Sebelum lanjut ke TypeScript, pastikan bisa:
- [ ] Menulis function dengan berbagai cara (declaration, expression, arrow)
- [ ] Manipulasi array dengan map, filter, reduce
- [ ] Mengerti scope dan closure
- [ ] Melakukan DOM manipulation
- [ ] Menangani event (click, submit, dll)
- [ ] Fetch API + async/await + error handling
- [ ] Local storage untuk persistensi data
- [ ] Membuat aplikasi dari 0 tanpa bantuan
