# 04 - Lists

## Unordered List (Bullet)

| Tag    | Penjelasan                | Contoh                                  |
| ------ | ------------------------- | --------------------------------------- |
| `<ul>` | Daftar dengan bullet/poin | `<ul><li>Apel</li><li>Mangga</li></ul>` |
| `<li>` | Item dalam list           | `<li>Apel</li>`                         |

Contoh nested list:

```html
<ul>
  <li>
    Buah
    <ul>
      <li>Apel</li>
      <li>Mangga</li>
    </ul>
  </li>
  <li>
    Sayur
    <ul>
      <li>Wortel</li>
      <li>Bayam</li>
    </ul>
  </li>
</ul>
```

## Ordered List (Number)

| Tag / Atribut | Penjelasan                       | Contoh                                   |
| ------------- | -------------------------------- | ---------------------------------------- |
| `<ol>`        | Daftar berurut dengan angka      | `<ol><li>Bangun</li><li>Mandi</li></ol>` |
| `type`        | Jenis penomoran (1/A/a/I/i)      | `<ol type="A">`                          |
| `start`       | Mulai dari angka tertentu        | `<ol start="5">`                         |
| `reversed`    | Urutan terbalik (besar ke kecil) | `<ol reversed>`                          |
| `value`       | Override nomor item tertentu     | `<li value="10">`                        |

```html
<ol type="1">
  <li>Angka (default)</li>
</ol>
<ol type="A">
  <li>Huruf kapital</li>
</ol>
<ol type="a">
  <li>Huruf kecil</li>
</ol>
<ol type="I">
  <li>Romawi kapital</li>
</ol>
<ol type="i">
  <li>Romawi kecil</li>
</ol>
```

```html
<ol start="5">
  <li>Item 5</li>
  <li>Item 6</li>
</ol>

<ol reversed>
  <li>Peringkat 3</li>
  <li>Peringkat 2</li>
  <li>Peringkat 1</li>
</ol>

<ol>
  <li>Item 1</li>
  <li value="10">Item 10 (loncat)</li>
  <li>Item 11</li>
</ol>
```

## Description List

| Tag    | Penjelasan                                 | Contoh                                                     |
| ------ | ------------------------------------------ | ---------------------------------------------------------- |
| `<dl>` | Daftar istilah + deskripsi (seperti kamus) | `<dl><dt>HTML</dt><dd>HyperText Markup Language</dd></dl>` |
| `<dt>` | Istilah yang dijelaskan                    | `<dt>HTML</dt>`                                            |
| `<dd>` | Deskripsi dari istilah                     | `<dd>HyperText Markup Language</dd>`                       |

```html
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language — bahasa markup untuk web.</dd>
  <dt>CSS</dt>
  <dd>Cascading Style Sheets — bahasa untuk styling.</dd>
</dl>
```

Multi-value description:

```html
<dl>
  <dt>Warna Dasar</dt>
  <dd>Merah</dd>
  <dd>Kuning</dd>
  <dd>Biru</dd>
</dl>
```

## Kombinasi & Styling

List horizontal via CSS:

```html
<style>
  .inline-list li {
    display: inline;
    margin-right: 10px;
  }
</style>
<ul class="inline-list">
  <li>Menu 1</li>
  <li>Menu 2</li>
  <li>Menu 3</li>
</ul>
```

Custom bullet via CSS:

```html
<style>
  .custom-list {
    list-style-type: square;
  }
  .emoji-list {
    list-style-type: none;
  }
  .emoji-list li::before {
    content: "✅ ";
  }
</style>

<ul class="custom-list">
  <li>Kotak</li>
</ul>

<ul class="emoji-list">
  <li>Sudah selesai</li>
</ul>
```
