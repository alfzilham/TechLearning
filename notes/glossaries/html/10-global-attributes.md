# 10 - Global Attributes

## Atribut Global — Bisa Dipakai di SEMUA Elemen HTML

| Atribut           | Penjelasan                                    | Contoh                                                     |
| ----------------- | --------------------------------------------- | ---------------------------------------------------------- |
| `id`              | Identitas unik (hanya satu per halaman)       | `<div id="header">Header</div>`                            |
| `class`           | Klasifikasi elemen (bisa lebih dari satu)     | `<div class="card active">Card</div>`                      |
| `style`           | Inline CSS langsung di elemen                 | `<p style="color: red;">Teks merah</p>`                    |
| `title`           | Tooltip saat hover                            | `<p title="Ini tooltip">Hover di sini</p>`                 |
| `lang`            | Bahasa konten elemen                          | `<html lang="id">`, `<p lang="en">`                        |
| `dir`             | Arah teks (ltr / rtl)                         | `<p dir="rtl">نص عربي</p>`                                 |
| `hidden`          | Menyembunyikan elemen (seperti display: none) | `<p hidden>Pesan rahasia</p>`                              |
| `tabindex`        | Urutan fokus saat tekan Tab                   | `<input type="text" tabindex="1" />`                       |
| `data-*`          | Custom attribute untuk menyimpan data         | `<div data-id="123" data-nama="Rizky">User Card</div>`     |
| `contenteditable` | Elemen bisa diedit langsung oleh user         | `<p contenteditable="true">Edit teks ini!</p>`             |
| `spellcheck`      | Aktifkan/nonaktifkan spellcheck               | `<textarea spellcheck="false">Tanpa spellcheck</textarea>` |
| `draggable`       | Elemen bisa di-drag                           | `<img src="foto.jpg" draggable="true" alt="Foto" />`       |
| `translate`       | Izin konten diterjemahkan                     | `<p translate="no">Nama Brand™</p>`                        |
| `accesskey`       | Shortcut keyboard untuk elemen                | `<button accesskey="s">Simpan (Alt+S)</button>`            |
| `autofocus`       | Fokus otomatis ke input saat halaman dimuat   | `<input type="text" autofocus />`                          |
| `slot`            | Digunakan dengan Web Component (shadow DOM)   | `<span slot="title">Judul</span>`                          |

Contoh `data-*` dengan JavaScript:

```html
<div data-id="123" data-nama="Rizky" data-role="admin" data-active="true">
  User Card
</div>

<script>
  const el = document.querySelector("[data-id='123']");
  console.log(el.dataset.id); // "123"
  console.log(el.dataset.nama); // "Rizky"
  console.log(el.dataset.role); // "admin"
  console.log(el.dataset.active); // "true"
</script>
```

Contoh `contenteditable`:

```html
<div contenteditable="true">
  <h2>Judul yang bisa diedit</h2>
  <p>Klik dan edit teks ini langsung!</p>
</div>
```

Contoh `tabindex`:

```html
<input type="text" tabindex="1" placeholder="Pertama" />
<input type="text" tabindex="3" placeholder="Ketiga" />
<input type="text" tabindex="2" placeholder="Kedua" />
<button tabindex="-1">Tidak bisa di-tab</button>
```

Contoh `hidden` dengan toggle:

```html
<button
  onclick="this.nextElementSibling.hidden = !this.nextElementSibling.hidden"
>
  Toggle
</button>
<p hidden>Konten yang bisa ditampilkan</p>
```
