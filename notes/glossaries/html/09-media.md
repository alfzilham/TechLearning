# 09 - Media (Audio, Video, Iframe)

## Audio

| Tag / Atribut | Penjelasan                               | Contoh                                                                |
| ------------- | ---------------------------------------- | --------------------------------------------------------------------- |
| `<audio>`     | Memutar file audio                       | `<audio controls><source src="lagu.mp3" type="audio/mpeg" /></audio>` |
| `controls`    | Tampilkan tombol play/pause/volume       | `<audio controls src="lagu.mp3"></audio>`                             |
| `autoplay`    | Putar otomatis (sering diblokir browser) | `<audio autoplay src="lagu.mp3"></audio>`                             |
| `loop`        | Ulang terus                              | `<audio loop controls src="lagu.mp3"></audio>`                        |
| `muted`       | Diam (wajib untuk autoplay)              | `<audio muted autoplay src="lagu.mp3"></audio>`                       |
| `preload`     | Mulai download (none/metadata/auto)      | `<audio preload="metadata" controls src="lagu.mp3"></audio>`          |

## Video

| Tag / Atribut        | Penjelasan                    | Contoh                                                                                         |
| -------------------- | ----------------------------- | ---------------------------------------------------------------------------------------------- |
| `<video>`            | Memutar file video            | `<video controls width="640" height="360"><source src="video.mp4" type="video/mp4" /></video>` |
| `controls`           | Tampilkan tombol kontrol      | `<video controls src="video.mp4"></video>`                                                     |
| `autoplay` + `muted` | Putar otomatis tanpa suara    | `<video autoplay muted loop src="video.mp4"></video>`                                          |
| `poster`             | Gambar thumbnail sebelum play | `<video controls poster="thumbnail.jpg" src="video.mp4"></video>`                              |
| `width` / `height`   | Ukuran video                  | `<video width="100%" height="auto" controls src="video.mp4"></video>`                          |
| `loop`               | Ulang terus                   | `<video loop controls src="video.mp4"></video>`                                                |
| `<track>`            | Subtitle/teks ke video        | `<track kind="subtitles" src="subs/id.vtt" srclang="id" label="Indonesia" />`                  |

Jenis `kind` pada `<track>`: `subtitles`, `captions`, `descriptions`, `chapters`, `metadata`.

```html
<video controls src="video.mp4">
  <track
    kind="subtitles"
    src="subs/id.vtt"
    srclang="id"
    label="Indonesia"
    default
  />
  <track kind="subtitles" src="subs/en.vtt" srclang="en" label="English" />
  <track kind="captions" src="subs/captions.vtt" label="Captions" />
</video>
```

## Iframe

| Tag / Atribut     | Penjelasan                   | Contoh                                                                  |
| ----------------- | ---------------------------- | ----------------------------------------------------------------------- |
| `<iframe>`        | Menyematkan halaman web lain | `<iframe src="https://example.com" width="800" height="600"></iframe>`  |
| `allowfullscreen` | Izinkan fullscreen           | `<iframe src="..." allowfullscreen></iframe>`                           |
| `loading`         | Lazy loading                 | `<iframe src="..." loading="lazy"></iframe>`                            |
| `sandbox`         | Batasi keamanan              | `<iframe src="..." sandbox="allow-scripts allow-same-origin"></iframe>` |

Contoh embed YouTube:

```html
<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/VIDEO_ID"
  title="Video YouTube"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
  allowfullscreen
></iframe>
```

Contoh embed Google Maps:

```html
<iframe
  width="600"
  height="450"
  style="border: 0;"
  loading="lazy"
  allowfullscreen
  referrerpolicy="no-referrer-when-downgrade"
  src="https://www.google.com/maps/embed?pb=!1m18..."
></iframe>
```

## Object & Embed

| Tag        | Penjelasan                                     | Contoh                                                                                   |
| ---------- | ---------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `<object>` | Menyematkan konten eksternal (PDF, Flash)      | `<object data="dokumen.pdf" type="application/pdf" width="600" height="400"></object>`   |
| `<embed>`  | Menyematkan konten eksternal (lebih sederhana) | `<embed src="file.swf" type="application/x-shockwave-flash" width="600" height="400" />` |

## Source

| Tag        | Penjelasan                                         | Contoh                                         |
| ---------- | -------------------------------------------------- | ---------------------------------------------- |
| `<source>` | Multiple format media untuk kompatibilitas browser | `<source src="audio.mp3" type="audio/mpeg" />` |

```html
<audio controls>
  <source src="audio.mp3" type="audio/mpeg" />
  <source src="audio.ogg" type="audio/ogg" />
  <source src="audio.wav" type="audio/wav" />
</audio>

<video controls>
  <source src="video.mp4" type="video/mp4" />
  <source src="video.webm" type="video/webm" />
  <source src="video.ogv" type="video/ogg" />
</video>
```
