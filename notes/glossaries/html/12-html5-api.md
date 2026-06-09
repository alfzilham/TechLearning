# 12 - HTML5 API & Advanced Features

## Canvas

| Tag        | Penjelasan                          | Contoh                                                     |
| ---------- | ----------------------------------- | ---------------------------------------------------------- |
| `<canvas>` | Menggambar grafik 2D via JavaScript | `<canvas id="myCanvas" width="400" height="300"></canvas>` |

```html
<script>
  const canvas = document.getElementById("myCanvas");
  const ctx = canvas.getContext("2d");

  ctx.fillStyle = "red";
  ctx.fillRect(10, 10, 100, 50); // Rectangle

  ctx.beginPath();
  ctx.arc(200, 100, 40, 0, Math.PI * 2); // Circle
  ctx.fillStyle = "blue";
  ctx.fill();

  ctx.font = "20px Arial";
  ctx.fillStyle = "black";
  ctx.fillText("Halo Canvas!", 50, 200); // Text

  ctx.beginPath();
  ctx.moveTo(0, 0);
  ctx.lineTo(300, 250); // Line
  ctx.strokeStyle = "green";
  ctx.lineWidth = 3;
  ctx.stroke();
</script>
```

## Drag & Drop

| Atribut / Event | Penjelasan               | Contoh                             |
| --------------- | ------------------------ | ---------------------------------- |
| `draggable`     | Buat elemen bisa di-drag | `<div draggable="true">Item</div>` |
| `ondragstart`   | Saat mulai drag          | `ondragstart="drag(event)"`        |
| `ondragover`    | Saat di atas target drop | `ondragover="allowDrop(event)"`    |
| `ondrop`        | Saat di-drop di target   | `ondrop="drop(event)"`             |

```html
<div id="drag1" draggable="true" ondragstart="drag(event)">
  Item yang bisa di-drag
</div>
<div id="dropzone" ondrop="drop(event)" ondragover="allowDrop(event)">
  Drop di sini
</div>

<script>
  function allowDrop(e) {
    e.preventDefault();
  }
  function drag(e) {
    e.dataTransfer.setData("text", e.target.id);
  }
  function drop(e) {
    e.preventDefault();
    const data = e.dataTransfer.getData("text");
    e.target.appendChild(document.getElementById(data));
  }
</script>
```

### Drag Events

```html
<div
  ondragstart="..."  <!-- mulai drag -->
  ondrag="..."       <!-- saat sedang drag -->
  ondragend="..."    <!-- selesai drag -->
  ondragenter="..."  <!-- masuk ke target -->
  ondragover="..."   <!-- di atas target -->
  ondragleave="..."  <!-- keluar dari target -->
  ondrop="..."       <!-- di-drop di target -->
></div>
```

## Details & Summary

| Tag         | Penjelasan                          | Contoh                                                    |
| ----------- | ----------------------------------- | --------------------------------------------------------- |
| `<details>` | Konten collapsible tanpa JavaScript | `<details><summary>Klik</summary><p>Konten</p></details>` |
| `<summary>` | Judul yang diklik untuk buka/tutup  | `<summary>Klik untuk membuka</summary>`                   |
| `open`      | Buka secara default                 | `<details open>...</details>`                             |

```html
<details>
  <summary>Klik untuk membuka</summary>
  <p>Ini konten yang tersembunyi.</p>
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
  </ul>
</details>

<details open>
  <summary>Terbuka sejak awal</summary>
  <p>Konten langsung terlihat.</p>
</details>
```

## Dialog

| Tag / Method  | Penjelasan                             | Contoh                               |
| ------------- | -------------------------------------- | ------------------------------------ |
| `<dialog>`    | Modal/popup native                     | `<dialog id="myDialog">...</dialog>` |
| `showModal()` | Tampil sebagai modal (dengan backdrop) | `dialog.showModal()`                 |
| `show()`      | Tampil tanpa backdrop                  | `dialog.show()`                      |
| `close()`     | Tutup dialog                           | `dialog.close("ok")`                 |

```html
<dialog id="myDialog">
  <h2>Konfirmasi</h2>
  <p>Apakah anda yakin ingin menghapus?</p>
  <form method="dialog">
    <button value="yes">Ya</button>
    <button value="no">Tidak</button>
  </form>
</dialog>

<button onclick="document.getElementById('myDialog').showModal()">
  Buka Dialog
</button>

<script>
  const dialog = document.getElementById("myDialog");
  dialog.addEventListener("close", () => {
    if (dialog.returnValue === "yes") console.log("User memilih Ya");
  });
</script>
```

## Datalist

| Tag          | Penjelasan                           | Contoh                                                                  |
| ------------ | ------------------------------------ | ----------------------------------------------------------------------- |
| `<datalist>` | Autocomplete suggestions untuk input | `<input list="negara-list" /><datalist id="negara-list">...</datalist>` |

```html
<label for="negara">Negara:</label>
<input list="negara-list" id="negara" name="negara" placeholder="Ketik..." />
<datalist id="negara-list">
  <option value="Indonesia" />
  <option value="Malaysia" />
  <option value="Singapura" />
</datalist>
```

## Progress & Meter

| Tag          | Penjelasan                            | Contoh                                                               |
| ------------ | ------------------------------------- | -------------------------------------------------------------------- |
| `<progress>` | Progress bar (tidak tentu atau pasti) | `<progress value="70" max="100">70%</progress>`                      |
| `<meter>`    | Nilai dalam range tertentu            | `<meter value="65" min="0" max="100" low="30" high="80">65%</meter>` |

```html
<!-- Progress tidak tentu (loading) -->
<progress></progress>

<!-- Progress pasti -->
<progress value="70" max="100">70%</progress>

<!-- Meter -->
<p>
  CPU Usage:
  <meter value="65" min="0" max="100" low="30" high="80" optimum="50">
    65%
  </meter>
</p>
<p>Disk: <meter value="85" min="0" max="100">85%</meter></p>
```

## Content Editable

| Atribut           | Penjelasan                            | Contoh                                  |
| ----------------- | ------------------------------------- | --------------------------------------- |
| `contenteditable` | Elemen bisa diedit langsung oleh user | `<div contenteditable="true">...</div>` |

```html
<div contenteditable="true">
  <h2>Judul yang bisa diedit</h2>
  <p>Klik dan edit teks ini langsung!</p>
</div>
<button onclick="alert(this.previousElementSibling.innerHTML)">
  Lihat HTML
</button>
```

Legacy formatting dengan `document.execCommand()`:

```html
<div contenteditable="true" id="editor">Teks yang bisa di-bold dsb.</div>
<button onclick="document.execCommand('bold')">Bold</button>
<button onclick="document.execCommand('italic')">Italic</button>
<button onclick="document.execCommand('underline')">Underline</button>
<button onclick="document.execCommand('insertUnorderedList')">List</button>
```

## Web Storage

| API              | Penjelasan                                             | Contoh                                            |
| ---------------- | ------------------------------------------------------ | ------------------------------------------------- |
| `localStorage`   | Data persisten (tidak hilang meskipun browser ditutup) | `localStorage.setItem("theme", "dark")`           |
| `sessionStorage` | Data sementara (hilang saat tab ditutup)               | `sessionStorage.setItem("sementara", "data ini")` |

```js
// localStorage
localStorage.setItem("theme", "dark");
localStorage.setItem("user", JSON.stringify({ nama: "Rizky" }));
console.log(localStorage.getItem("theme")); // "dark"
localStorage.removeItem("theme");
localStorage.clear();

// sessionStorage
sessionStorage.setItem("sementara", "data ini");
const data = sessionStorage.getItem("sementara");
sessionStorage.removeItem("sementara");
sessionStorage.clear();
```

## Geolocation

| API                     | Penjelasan              | Contoh                                                     |
| ----------------------- | ----------------------- | ---------------------------------------------------------- |
| `navigator.geolocation` | Mendapatkan posisi user | `navigator.geolocation.getCurrentPosition(success, error)` |

```js
if (navigator.geolocation) {
  navigator.geolocation.getCurrentPosition(
    (position) => {
      console.log("Latitude:", position.coords.latitude);
      console.log("Longitude:", position.coords.longitude);
    },
    (error) => {
      console.error("Error:", error.message);
    },
    { enableHighAccuracy: true, timeout: 5000 },
  );
} else {
  console.log("Geolocation tidak didukung");
}
```
