# 02 - Text Formatting

## Inline Text Semantics

| Tag            | Penjelasan                                   | Contoh                                           |
| -------------- | -------------------------------------------- | ------------------------------------------------ |
| `<strong>`     | Teks tebal, makna serius/urgent              | `<strong>sangat penting</strong>`                |
| `<b>`          | Teks tebal tanpa makna khusus                | `<b>tebal biasa</b>`                             |
| `<em>`         | Teks miring dengan penekanan                 | `<em>sangat</em> suka`                           |
| `<i>`          | Teks miring tanpa makna khusus               | `<i>alumni</i>`                                  |
| `<u>`          | Teks garis bawah                             | `<u>teks bergaris bawah</u>`                     |
| `<mark>`       | Teks di-highlight/ditandai                   | `<mark>ini penting</mark>`                       |
| `<small>`      | Teks ukuran kecil (catatan kaki)             | `<small>Harga belum termasuk pajak</small>`      |
| `<del>`        | Teks dicoret (dihapus)                       | `<del>Rp100.000</del>`                           |
| `<ins>`        | Teks baru dimasukkan (garis bawah)           | `<ins>50%</ins>`                                 |
| `<sub>`        | Subscript (bawah garis normal)               | `H<sub>2</sub>O`                                 |
| `<sup>`        | Superscript (atas garis normal)              | `25m<sup>2</sup>`                                |
| `<code>`       | Teks kode program (monospace)                | `<code>console.log()</code>`                     |
| `<pre>`        | Teks preformatted (format dipertahankan)     | `<pre>...kode...</pre>`                          |
| `<blockquote>` | Kutipan panjang (diindent)                   | `<blockquote><p>Kutipan</p></blockquote>`        |
| `<q>`          | Kutipan pendek (otomatis tanda petik)        | `<q>Aku akan datang</q>`                         |
| `<abbr>`       | Singkatan dengan tooltip via `title`         | `<abbr title="HTML">HTML</abbr>`                 |
| `<address>`    | Info kontak (miring otomatis)                | `<address>Email: user@example.com</address>`     |
| `<time>`       | Waktu/tanggal machine-readable               | `<time datetime="2024-12-25">25 Des 2024</time>` |
| `<span>`       | Container inline tanpa makna (untuk styling) | `<span style="color: red;">merah</span>`         |

Contoh blockquote:

```html
<blockquote>
  <p>Ilmu adalah cahaya yang menerangi kegelapan.</p>
  <cite>— Seorang bijak</cite>
</blockquote>
```

Contoh pre + code:

```html
<pre>
function halo() {
  console.log("Halo!");
}
</pre>
```

## Formatting Lain

| Tag     | Penjelasan                   | Contoh                                 |
| ------- | ---------------------------- | -------------------------------------- |
| `<bdo>` | Override arah teks           | `<bdo dir="rtl">Teks dari kanan</bdo>` |
| `<wbr>` | Tempat potong baris opsional | `halaman/<wbr />panjang`               |
