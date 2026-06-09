# 10 - DOM & Browser API

> **Catatan:** Kode di file ini hanya jalan di **browser**, bukan di Node.js.

## Seleksi Elemen

| Method                     | Penjelasan                               | Contoh                                    |
| -------------------------- | ---------------------------------------- | ----------------------------------------- |
| `getElementById()`         | Pilih elemen berdasarkan ID              | `document.getElementById("header")`       |
| `querySelector()`          | Pilih pertama cocok CSS selector         | `document.querySelector(".card")`         |
| `querySelectorAll()`       | Pilih semua cocok (NodeList)             | `document.querySelectorAll(".card")`      |
| `getElementsByClassName()` | Pilih berdasarkan class (HTMLCollection) | `document.getElementsByClassName("card")` |
| `getElementsByTagName()`   | Pilih berdasarkan tag                    | `document.getElementsByTagName("p")`      |

## Membuat & Manipulasi Elemen

| Method            | Penjelasan                       |
| ----------------- | -------------------------------- |
| `createElement()` | Membuat elemen HTML baru         |
| `appendChild()`   | Tambah elemen anak di akhir      |
| `prepend()`       | Tambah elemen anak di awal       |
| `insertBefore()`  | Sisipkan sebelum elemen tertentu |
| `removeChild()`   | Hapus elemen anak                |
| `remove()`        | Hapus elemen itu sendiri         |
| `replaceChild()`  | Ganti elemen anak                |

Contoh:

```js
let parent = document.querySelector(".container");
let baru = document.createElement("p");
baru.textContent = "Halo!";
parent.appendChild(baru);
```

## Konten & Atribut

| Method / Properti   | Penjelasan                          | Contoh                                    |
| ------------------- | ----------------------------------- | ----------------------------------------- |
| `textContent`       | Ambil/ubah teks (tanpa tag HTML)    | `el.textContent = "Teks baru"`            |
| `innerHTML`         | Ambil/ubah konten termasuk tag HTML | `el.innerHTML = "<strong>Bold</strong>"`  |
| `getAttribute()`    | Dapatkan nilai atribut              | `link.getAttribute("href")`               |
| `setAttribute()`    | Ubah nilai atribut                  | `link.setAttribute("href","https://...")` |
| `removeAttribute()` | Hapus atribut                       | `link.removeAttribute("target")`          |
| `hasAttribute()`    | Cek apakah atribut ada              | `link.hasAttribute("href")`               |

## Class List

| Method                 | Penjelasan                  | Contoh                                |
| ---------------------- | --------------------------- | ------------------------------------- |
| `classList.add()`      | Tambah class                | `el.classList.add("aktif")`           |
| `classList.remove()`   | Hapus class                 | `el.classList.remove("aktif")`        |
| `classList.toggle()`   | Toggle class (tambah/hapus) | `el.classList.toggle("aktif")`        |
| `classList.contains()` | Cek apakah class ada        | `el.classList.contains("aktif")`      |
| `classList.replace()`  | Ganti class                 | `el.classList.replace("lama","baru")` |

## Style

| Method / Properti    | Penjelasan                          | Contoh                        |
| -------------------- | ----------------------------------- | ----------------------------- |
| `element.style`      | Ubah style inline (camelCase)       | `el.style.color = "red"`      |
| `getComputedStyle()` | Dapatkan style final (termasuk CSS) | `window.getComputedStyle(el)` |

## Event

| Method                  | Penjelasan            | Contoh                                 |
| ----------------------- | --------------------- | -------------------------------------- |
| `addEventListener()`    | Tambah event listener | `btn.addEventListener("click", fn)`    |
| `removeEventListener()` | Hapus event listener  | `btn.removeEventListener("click", fn)` |

Event object properties:

```js
element.addEventListener("click", (e) => {
  e.preventDefault(); // cegah default
  e.stopPropagation(); // cegah bubbling
  console.log(e.type, e.target, e.clientX, e.clientY);
});
```

Jenis event umum:

- **Mouse:** `click`, `dblclick`, `mouseenter`, `mouseleave`, `mousemove`
- **Keyboard:** `keydown`, `keyup`
- **Form:** `submit`, `input`, `change`, `focus`, `blur`
- **Window:** `scroll`, `resize`, `load`, `DOMContentLoaded`

## Navigasi DOM

| Properti                 | Penjelasan          |
| ------------------------ | ------------------- |
| `parentElement`          | Induk element       |
| `children`               | HTMLCollection anak |
| `firstElementChild`      | Anak pertama        |
| `lastElementChild`       | Anak terakhir       |
| `previousElementSibling` | Saudara sebelumnya  |
| `nextElementSibling`     | Saudara setelahnya  |

## Window & Document

| Method / Properti          | Penjelasan                            |
| -------------------------- | ------------------------------------- |
| `window.location.href`     | URL lengkap / redirect                |
| `window.location.pathname` | Path URL                              |
| `localStorage.setItem()`   | Simpan data persisten                 |
| `localStorage.getItem()`   | Ambil data persisten                  |
| `sessionStorage.setItem()` | Simpan data (hilang saat tab ditutup) |
| `alert()`                  | Popup pesan                           |
| `confirm()`                | Konfirmasi true/false                 |
| `prompt()`                 | Input string dari user                |
