# 06 - Forms & Input

## Form Dasar

| Tag      | Penjelasan                               | Contoh                                            |
| -------- | ---------------------------------------- | ------------------------------------------------- |
| `<form>` | Membungkus input untuk dikirim ke server | `<form action="/proses" method="POST">...</form>` |

Atribut `<form>`:

| Atribut        | Penjelasan                        | Contoh                          |
| -------------- | --------------------------------- | ------------------------------- |
| `action`       | URL tujuan pengiriman             | `action="/submit"`              |
| `method`       | Metode pengiriman (GET/POST)      | `method="POST"`                 |
| `enctype`      | Untuk upload file                 | `enctype="multipart/form-data"` |
| `target`       | Hasil di tab/frame mana           | `target="_blank"`               |
| `novalidate`   | Matikan validasi bawaan browser   | `novalidate`                    |
| `autocomplete` | Aktifkan/nonaktifkan autocomplete | `autocomplete="on"`             |

## Input Fields

### Tipe Teks

| Tag               | Penjelasan                     | Contoh                                                         |
| ----------------- | ------------------------------ | -------------------------------------------------------------- |
| `type="text"`     | Input teks biasa               | `<input type="text" name="nama" placeholder="Nama lengkap" />` |
| `type="email"`    | Input email                    | `<input type="email" name="email" />`                          |
| `type="password"` | Input password                 | `<input type="password" name="password" />`                    |
| `type="search"`   | Input pencarian                | `<input type="search" name="q" placeholder="Cari..." />`       |
| `type="url"`      | Input URL                      | `<input type="url" name="website" />`                          |
| `type="tel"`      | Input nomor telepon            | `<input type="tel" name="phone" />`                            |
| `<textarea>`      | Input teks panjang (multiline) | `<textarea name="pesan" rows="4"></textarea>`                  |

### Tipe Angka & Tanggal

| Tag                     | Penjelasan            | Contoh                                                |
| ----------------------- | --------------------- | ----------------------------------------------------- |
| `type="number"`         | Input angka           | `<input type="number" min="0" max="150" />`           |
| `type="range"`          | Slider                | `<input type="range" min="0" max="100" value="50" />` |
| `type="date"`           | Input tanggal         | `<input type="date" name="tanggal" />`                |
| `type="time"`           | Input waktu           | `<input type="time" name="jam" />`                    |
| `type="datetime-local"` | Input tanggal + waktu | `<input type="datetime-local" name="waktu" />`        |
| `type="month"`          | Input bulan           | `<input type="month" name="bulan" />`                 |
| `type="week"`           | Input minggu          | `<input type="week" name="minggu" />`                 |

### Tipe Pilihan

| Tag               | Penjelasan                   | Contoh                                                              |
| ----------------- | ---------------------------- | ------------------------------------------------------------------- |
| `type="checkbox"` | Checkbox (bisa pilih banyak) | `<input type="checkbox" name="hobi" value="coding" />`              |
| `type="radio"`    | Radio (hanya satu pilihan)   | `<input type="radio" name="gender" value="pria" />`                 |
| `<select>`        | Dropdown                     | `<select name="kota"><option value="jkt">Jakarta</option></select>` |
| `<option>`        | Opsi dalam select            | `<option value="bdg">Bandung</option>`                              |

```html
<select name="hobi" multiple>
  <option value="membaca">Membaca</option>
  <option value="olahraga">Olahraga</option>
</select>
```

### Tipe Khusus

| Tag             | Penjelasan                       | Contoh                                                |
| --------------- | -------------------------------- | ----------------------------------------------------- |
| `type="file"`   | Upload file                      | `<input type="file" name="foto" accept="image/*" />`  |
| `type="color"`  | Color picker                     | `<input type="color" name="warna" value="#ff0000" />` |
| `type="hidden"` | Input tersembunyi (tidak tampil) | `<input type="hidden" name="token" value="abc123" />` |

### Tipe Tombol

| Tag             | Penjelasan                      | Contoh                                                         |
| --------------- | ------------------------------- | -------------------------------------------------------------- |
| `type="submit"` | Tombol kirim form               | `<input type="submit" value="Kirim" />`                        |
| `type="reset"`  | Tombol reset form               | `<input type="reset" value="Reset" />`                         |
| `type="button"` | Tombol biasa (untuk JavaScript) | `<input type="button" value="Klik" onclick="alert('Halo')" />` |

## Button

| Tag        | Penjelasan                            | Contoh                                 |
| ---------- | ------------------------------------- | -------------------------------------- |
| `<button>` | Tombol lebih fleksibel dari `<input>` | `<button type="submit">Kirim</button>` |

```html
<button type="button" onclick="alert('Hello!')">Klik</button>
<button type="submit"><img src="icon.svg" alt="" /> Kirim Data</button>
<button disabled>Tombol Nonaktif</button>
```

## Label

| Tag       | Penjelasan                            | Contoh                              |
| --------- | ------------------------------------- | ----------------------------------- |
| `<label>` | Label untuk input (fokus saat diklik) | `<label for="email">Email:</label>` |

```html
<!-- Cara 1: wrap input -->
<label>Nama: <input type="text" name="nama" /></label>

<!-- Cara 2: pakai for -->
<label for="email">Email:</label>
<input type="email" id="email" name="email" />
```

## Fieldset & Legend

| Tag          | Penjelasan                       | Contoh                                                  |
| ------------ | -------------------------------- | ------------------------------------------------------- |
| `<fieldset>` | Mengelompokkan input dalam kotak | `<fieldset><legend>Data Pribadi</legend>...</fieldset>` |
| `<legend>`   | Judul/keterangan fieldset        | `<legend>Data Pribadi</legend>`                         |

```html
<fieldset>
  <legend>Data Pribadi</legend>
  <label>Nama: <input type="text" name="nama" /></label>
  <label>Umur: <input type="number" name="umur" /></label>
</fieldset>

<fieldset disabled>
  <legend>Bagian Terkunci</legend>
  <input type="text" placeholder="Tidak bisa diisi" />
</fieldset>
```

## Datalist

| Tag          | Penjelasan                      | Contoh                                                                                  |
| ------------ | ------------------------------- | --------------------------------------------------------------------------------------- |
| `<datalist>` | Input dengan saran autocomplete | `<input list="buah-list" /><datalist id="buah-list"><option value="Apel" /></datalist>` |

```html
<label for="buah">Pilih buah:</label>
<input list="buah-list" id="buah" name="buah" />
<datalist id="buah-list">
  <option value="Apel" />
  <option value="Mangga" />
  <option value="Jeruk" />
</datalist>
```

## Output

| Tag        | Penjelasan                  | Contoh                            |
| ---------- | --------------------------- | --------------------------------- |
| `<output>` | Menampilkan hasil kalkulasi | `<output name="hasil">0</output>` |

```html
<form oninput="hasil.value = parseInt(a.value) + parseInt(b.value)">
  <input type="number" name="a" value="0" /> +
  <input type="number" name="b" value="0" /> =
  <output name="hasil">0</output>
</form>
```
