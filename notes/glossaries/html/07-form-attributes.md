# 07 - Form Attributes

## Atribut Input

| Atribut        | Penjelasan                                     | Contoh                                                     |
| -------------- | ---------------------------------------------- | ---------------------------------------------------------- |
| `name`         | Nama field (dikirim ke server sebagai key)     | `<input type="text" name="username" />`                    |
| `value`        | Nilai default input                            | `<input type="text" name="nama" value="Rizky" />`          |
| `placeholder`  | Teks petunjuk (hilang saat mengetik)           | `<input type="text" placeholder="Masukkan nama..." />`     |
| `required`     | Input wajib diisi                              | `<input type="text" name="nama" required />`               |
| `readonly`     | Input hanya bisa dibaca (tetap dikirim)        | `<input type="text" value="Tidak bisa diubah" readonly />` |
| `disabled`     | Input nonaktif (tidak dikirim ke server)       | `<input type="text" value="Nonaktif" disabled />`          |
| `autofocus`    | Fokus otomatis saat halaman dimuat             | `<input type="text" name="cari" autofocus />`              |
| `autocomplete` | Saran otomatis browser (on/off/name/email/dll) | `<input type="text" name="nama" autocomplete="on" />`      |

## Validasi

| Atribut       | Penjelasan                                   | Contoh                                                                    |
| ------------- | -------------------------------------------- | ------------------------------------------------------------------------- |
| `min` / `max` | Batas minimal/maksimal (number, date, range) | `<input type="number" min="0" max="100" />`                               |
| `step`        | Kelipatan nilai                              | `<input type="number" step="5" />`                                        |
| `minlength`   | Panjang minimal teks                         | `<input type="text" minlength="3" />`                                     |
| `maxlength`   | Panjang maksimal teks                        | `<input type="text" maxlength="20" />`                                    |
| `pattern`     | Validasi dengan regex                        | `<input type="text" pattern="[A-Z]{3}[0-9]{3}" title="Format: ABC123" />` |
| `multiple`    | Mengizinkan multiple values (file, email)    | `<input type="file" multiple />`                                          |

```html
<input type="date" min="2024-01-01" max="2024-12-31" />
<input type="range" min="0" max="10" step="2" />
<textarea maxlength="500"></textarea>
<input type="tel" pattern="08[0-9]{8,11}" title="08xxxxxxxxx" />
<input type="email" multiple placeholder="pisahkan dengan koma" />
```

Custom validation via JS:

```html
<input type="text" id="username" />
<span id="error" style="color: red;"></span>
<script>
  document.querySelector("form").addEventListener("submit", (e) => {
    let input = document.getElementById("username");
    if (input.value.length < 3) {
      e.preventDefault();
      document.getElementById("error").textContent = "Minimal 3 karakter!";
    }
  });
</script>
```

## CSS Pseudo-classes untuk Form

| Pseudo-class         | Penjelasan                      | Contoh CSS                                        |
| -------------------- | ------------------------------- | ------------------------------------------------- |
| `:focus`             | Saat input aktif/diklik         | `input:focus { border-color: blue; }`             |
| `:valid`             | Input valid                     | `input:valid { border-color: green; }`            |
| `:invalid`           | Input tidak valid               | `input:invalid { border-color: red; }`            |
| `:required`          | Input wajib diisi               | `input:required { border-left: 3px solid red; }`  |
| `:optional`          | Input opsional                  | `input:optional { border-left: 3px solid gray; }` |
| `:disabled`          | Input nonaktif                  | `input:disabled { opacity: 0.5; }`                |
| `:enabled`           | Input aktif                     | `input:enabled { }`                               |
| `:in-range`          | Nilai dalam range               | `input:in-range { background: lightgreen; }`      |
| `:out-of-range`      | Nilai di luar range             | `input:out-of-range { background: lightcoral; }`  |
| `:placeholder-shown` | Saat placeholder masih terlihat | `input:placeholder-shown { font-style: italic; }` |

### Contoh Validasi Visual

```html
<style>
  input {
    border: 2px solid gray;
    padding: 8px;
  }
  input:focus {
    border-color: #0066ff;
    outline: none;
  }
  input:valid {
    border-color: #00cc66;
  }
  input:invalid {
    border-color: #ff3333;
  }
  input:required {
    border-left-width: 5px;
  }
</style>

<form>
  <input type="text" placeholder="Nama" required />
  <input type="email" placeholder="Email" required />
  <input type="number" placeholder="Umur" min="1" max="150" />
  <button type="submit">Kirim</button>
</form>
```
