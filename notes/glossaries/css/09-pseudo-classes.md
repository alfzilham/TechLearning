# 09 - Pseudo-classes

Pseudo-class adalah selector yang memilih elemen berdasarkan **keadaan** (state).

## Dynamic Pseudo-classes

| Selector         | Penjelasan                                   | Contoh                                              |
| ---------------- | -------------------------------------------- | --------------------------------------------------- |
| `:hover`         | Saat mouse di atas elemen                    | `a:hover { color: red; }`                           |
| `:active`        | Saat elemen sedang diklik                    | `button:active { transform: scale(0.95); }`         |
| `:focus`         | Saat elemen mendapat fokus (klik / tab)      | `input:focus { border-color: #0066ff; }`          |
| `:focus-within`  | Parent yang mengandung elemen fokus          | `form:focus-within { border-color: blue; }`         |
| `:focus-visible` | Fokus terlihat (biasanya keyboard)           | `button:focus-visible { outline: 2px solid blue; }` |
| `:visited`       | Link yang sudah pernah dikunjungi            | `a:visited { color: purple; }`                      |
| `:link`          | Link yang belum pernah dikunjungi            | `a:link { color: blue; }`                           |
| `:target`        | Elemen yang menjadi target URL (hash anchor) | `:target { background: yellow; }`                   |

---

## Structural Pseudo-classes

| Selector               | Penjelasan                            | Contoh                                         |
| ---------------------- | ------------------------------------- | ---------------------------------------------- |
| `:first-child`         | Anak pertama dari parent              | `li:first-child { font-weight: bold; }`        |
| `:last-child`          | Anak terakhir dari parent             | `li:last-child { border-bottom: none; }`       |
| `:first-of-type`       | Elemen pertama dari jenisnya          | `p:first-of-type { font-size: 1.2em; }`        |
| `:last-of-type`        | Elemen terakhir dari jenisnya         | `p:last-of-type { margin-bottom: 0; }`         |
| `:only-child`          | Satu-satunya anak                     | `p:only-child { text-align: center; }`         |
| `:only-of-type`        | Satu-satunya dari jenisnya            | `img:only-of-type { border: 3px solid gold; }` |
| `:nth-child(n)`        | Anak ke-n (urutan, bisa rumus)        | `li:nth-child(odd) { background: #f0f0f0; }` |
| `:nth-last-child(n)`   | Anak ke-n dari belakang               | `li:nth-last-child(2) { background: red; }`    |
| `:nth-of-type(n)`      | Anak ke-n dari jenisnya               | `p:nth-of-type(2) { color: blue; }`            |
| `:nth-last-of-type(n)` | Anak ke-n dari jenisnya dari belakang | `p:nth-last-of-type(1) { margin-bottom: 0; }`  |
| `:empty`               | Elemen tanpa anak (termasuk teks)     | `div:empty { display: none; }`                 |

```css
li:nth-child(3) {
  background: yellow;
}
li:nth-child(odd) {
  background: #f0f0f0;
}
li:nth-child(3n + 1) {
  background: blue;
}
```

---

## Negation & Selection

| Selector           | Penjelasan                                   | Contoh                                                   |
| ------------------ | -------------------------------------------- | -------------------------------------------------------- |
| `:not(selector)`   | Memilih elemen yang TIDAK cocok              | `input:not([type="submit"]) { border: 1px solid #ccc; }` |
| `:where(selector)` | Sama seperti selector, specificity = 0       | `:where(.card) p { color: blue; }`                       |
| `:is(selector)`    | Selector ringkas (specificity tertinggi)     | `:is(h1, h2, p) { margin: 0; }`                          |
| `:has(selector)`   | Parent selector — mengandung elemen tertentu | `.card:has(img) { padding: 0; }`                         |

```css
p:not(:first-child) {
  text-indent: 2em;
}
form:has(.error) {
  border-color: red;
}
```

---

## Form Pseudo-classes

| Selector                      | Penjelasan                      | Contoh                                            |
| ----------------------------- | ------------------------------- | ------------------------------------------------- |
| `:required` / `:optional`     | Input required / optional       | `input:required { border-left: 3px solid red; }`  |
| `:valid` / `:invalid`         | Input valid / tidak valid       | `input:valid { border-color: green; }`            |
| `:in-range` / `:out-of-range` | Input dalam / luar range        | `input:in-range { background: #e8f5e9; }`         |
| `:disabled` / `:enabled`      | Input disabled / enabled        | `button:disabled { opacity: 0.5; }`               |
| `:checked`                    | Checkbox / radio yang dicentang | `input:checked { accent-color: blue; }`           |
| `:placeholder-shown`          | Saat placeholder masih terlihat | `input:placeholder-shown { border-color: #ccc; }` |
| `:default`                    | Default button/input dalam form | `button:default { font-weight: bold; }`           |

---

## Contoh Lengkap

```css
/* Zebra striping tabel */
tr:nth-child(even) {
  background: #f9f9f9;
}

/* Card Hover */
.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
}

/* Style berdasarkan jumlah item */
li:only-child {
  list-style: none;
  text-align: center;
}

/* Highlight section yang di-anchor */
section:target {
  animation: flash 1s;
}

/* Form state */
input:focus:invalid {
  border-color: red;
  box-shadow: 0 0 0 2px rgba(255, 0, 0, 0.1);
}
input:focus:valid {
  border-color: green;
}
```
