# 05 - Tables

## Table Dasar

| Tag       | Penjelasan                            | Contoh                     |
| --------- | ------------------------------------- | -------------------------- |
| `<table>` | Membuat tabel                         | `<table>...</table>`       |
| `<tr>`    | Baris tabel                           | `<tr><td>konten</td></tr>` |
| `<td>`    | Sel data tabel                        | `<td>Data</td>`            |
| `<th>`    | Header tabel (tebal, tengah otomatis) | `<th>Nama</th>`            |

```html
<table border="1">
  <tr>
    <td>Baris 1, Kolom 1</td>
    <td>Baris 1, Kolom 2</td>
  </tr>
  <tr>
    <td>Baris 2, Kolom 1</td>
    <td>Baris 2, Kolom 2</td>
  </tr>
</table>
```

## Table Sections

| Tag       | Penjelasan              | Contoh                                       |
| --------- | ----------------------- | -------------------------------------------- |
| `<thead>` | Kelompok header tabel   | `<thead><tr><th>Nama</th></tr></thead>`      |
| `<tbody>` | Kelompok body/isi tabel | `<tbody><tr><td>Data</td></tr></tbody>`      |
| `<tfoot>` | Kelompok footer tabel   | `<tfoot><tr><td>Rata-rata</td></tr></tfoot>` |

```html
<table>
  <thead>
    <tr>
      <th>Nama</th>
      <th>Nilai</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Rizky</td>
      <td>90</td>
    </tr>
    <tr>
      <td>Budi</td>
      <td>85</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Rata-rata</td>
      <td>87.5</td>
    </tr>
  </tfoot>
</table>
```

## Merging Cells

| Atribut   | Penjelasan                       | Contoh                           |
| --------- | -------------------------------- | -------------------------------- |
| `colspan` | Menggabungkan kolom (horizontal) | `<th colspan="2">Data Diri</th>` |
| `rowspan` | Menggabungkan baris (vertikal)   | `<th rowspan="2">Kelas A</th>`   |

```html
<table border="1">
  <tr>
    <th colspan="2">Data Diri</th>
  </tr>
  <tr>
    <td>Nama</td>
    <td>Rizky</td>
  </tr>
</table>

<table border="1">
  <tr>
    <th rowspan="2">Kelas A</th>
    <td>Rizky</td>
  </tr>
  <tr>
    <td>Budi</td>
  </tr>
</table>
```

## Atribut Tabel

| Atribut            | Penjelasan                               | Contoh                              |
| ------------------ | ---------------------------------------- | ----------------------------------- |
| `border`           | Ketebalan border tabel (pixel)           | `<table border="1">`                |
| `cellpadding`      | Jarak konten ke border cell              | `<table cellpadding="10">`          |
| `cellspacing`      | Jarak antar cell                         | `<table cellspacing="5">`           |
| `width` / `height` | Ukuran tabel                             | `<table width="100%" height="300">` |
| `scope`            | Header untuk kolom/baris (aksesibilitas) | `<th scope="col">Nama</th>`         |

## Caption

| Tag         | Penjelasan             | Contoh                                  |
| ----------- | ---------------------- | --------------------------------------- |
| `<caption>` | Judul/keterangan tabel | `<caption>Daftar Nilai Siswa</caption>` |

```html
<table>
  <caption>
    Daftar Nilai Siswa
  </caption>
  <tr>
    <th>Nama</th>
    <th>Nilai</th>
  </tr>
  <tr>
    <td>Rizky</td>
    <td>90</td>
  </tr>
</table>
```

## Column Group

| Tag          | Penjelasan                               | Contoh                                                        |
| ------------ | ---------------------------------------- | ------------------------------------------------------------- |
| `<colgroup>` | Group untuk styling per kolom            | `<colgroup><col style="background: lightblue;" /></colgroup>` |
| `<col>`      | Mendefinisikan satu kolom dalam colgroup | `<col span="2" style="background: lightgray;" />`             |

```html
<table>
  <colgroup>
    <col style="background-color: lightblue;" />
    <col span="2" style="background-color: lightgray;" />
  </colgroup>
  <tr>
    <th>Nama</th>
    <th>Nilai 1</th>
    <th>Nilai 2</th>
  </tr>
  <tr>
    <td>Rizky</td>
    <td>90</td>
    <td>85</td>
  </tr>
</table>
```

## Contoh Lengkap

```html
<table
  border="1"
  cellpadding="8"
  style="border-collapse: collapse; width: 100%;"
>
  <caption>
    Data Siswa
  </caption>
  <thead>
    <tr>
      <th rowspan="2">No</th>
      <th rowspan="2">Nama</th>
      <th colspan="2">Nilai</th>
      <th rowspan="2">Status</th>
    </tr>
    <tr>
      <th>Ujian</th>
      <th>Tugas</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>Rizky</td>
      <td>90</td>
      <td>85</td>
      <td>Lulus</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Budi</td>
      <td>75</td>
      <td>80</td>
      <td>Lulus</td>
    </tr>
  </tbody>
</table>
```
