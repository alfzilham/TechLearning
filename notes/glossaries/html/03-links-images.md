# 03 - Links & Images

## Links

| Tag / Atribut | Penjelasan                            | Contoh                                       |
| ------------- | ------------------------------------- | -------------------------------------------- |
| `<a>`         | Membuat hyperlink ke URL/halaman lain | `<a href="https://google.com">Ke Google</a>` |
| `target`      | Cara membuka link                     | `target="_blank"` (tab baru)                 |
| `rel`         | Hubungan dengan link yang dituju      | `rel="noopener noreferrer"`                  |
| `download`    | Mendownload file saat diklik          | `<a href="file.pdf" download>Download</a>`   |
| `title`       | Tooltip saat hover                    | `title="Ke Google"`                          |

Contoh link:

```html
<a href="tentang.html">Ke halaman tentang</a>
<a href="#bagian2">Ke bagian 2 (anchor)</a>
<a href="mailto:user@example.com">Kirim email</a>
<a href="tel:+62812345678">Telepon</a>
<a href="https://google.com" target="_blank" rel="noopener noreferrer">Aman</a>
<a href="https://example.com" rel="nofollow">Jangan follow SEO</a>
<a href="file.pdf" download="nama-file-baru.pdf">Download PDF</a>
```

## Images

| Tag / Atribut      | Penjelasan                                    | Contoh                                                                             |
| ------------------ | --------------------------------------------- | ---------------------------------------------------------------------------------- |
| `<img>`            | Menampilkan gambar                            | `<img src="foto.jpg" alt="Deskripsi" />`                                           |
| `src`              | Path file gambar                              | `src="images/foto.jpg"`                                                            |
| `alt`              | Teks alternatif (penting untuk aksesibilitas) | `alt="Gunung Bromo saat sunrise"`                                                  |
| `width` / `height` | Ukuran gambar                                 | `width="800" height="600"`                                                         |
| `loading`          | Lazy loading                                  | `loading="lazy"`                                                                   |
| `srcset`           | Responsive image (multiple ukuran)            | `srcset="foto-320.jpg 320w, foto-640.jpg 640w"`                                    |
| `<figure>`         | Konten gambar dengan keterangan               | `<figure><img src="diagram.png" /><figcaption>Keterangan</figcaption></figure>`    |
| `<picture>`        | Gambar responsive dengan multiple sources     | `<picture><source media="..." srcset="..." /><img src="fallback.jpg" /></picture>` |

Contoh srcset:

```html
<img
  src="foto.jpg"
  srcset="foto-320.jpg 320w, foto-640.jpg 640w, foto-1024.jpg 1024w"
  sizes="(max-width: 600px) 100vw, 50vw"
  alt="Foto responsive"
/>
```

Contoh picture:

```html
<picture>
  <source media="(min-width: 1024px)" srcset="besar.webp" />
  <source media="(min-width: 600px)" srcset="sedang.webp" />
  <source srcset="kecil.webp" />
  <img src="fallback.jpg" alt="Gambar" />
</picture>
```

### Image Formats

```html
<img src="foto.webp" alt="Foto" />
<!-- WebP: kompresi lebih baik -->
<img src="icon.svg" alt="Icon" width="32" />
<!-- SVG: scalable vector -->
<img src="animasi.gif" alt="Animasi" />
<!-- GIF: animasi -->
<img src="data:image/png;base64,iVBOR..." alt="Icon" />
<!-- Base64 inline -->
```

## Image Maps

| Tag      | Penjelasan                            | Contoh                                                         |
| -------- | ------------------------------------- | -------------------------------------------------------------- |
| `<map>`  | Mendefinisikan image map              | `<map name="petamap">...</map>`                                |
| `<area>` | Area yang bisa diklik dalam image map | `<area shape="rect" coords="0,0,100,100" href="area1.html" />` |

```html
<img src="peta.jpg" alt="Peta" usemap="#petamap" />
<map name="petamap">
  <area shape="rect" coords="0,0,100,100" href="area1.html" alt="Area 1" />
  <area shape="circle" coords="200,200,50" href="area2.html" alt="Area 2" />
  <area
    shape="poly"
    coords="100,100,150,200,50,200"
    href="area3.html"
    alt="Area 3"
  />
</map>
```
