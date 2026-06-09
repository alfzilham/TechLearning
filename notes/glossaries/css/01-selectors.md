# 01 - CSS Selectors

## Basic Selectors

| Selector        | Penjelasan                               | Contoh                              |
| --------------- | ---------------------------------------- | ----------------------------------- |
| `element`       | Memilih semua elemen dengan tag tertentu | `p { color: blue; }`                |
| `.class`        | Memilih elemen dengan class tertentu     | `.card { border: 1px solid #ccc; }` |
| `#id`           | Memilih satu elemen dengan ID tertentu   | `#header { background: navy; }`     |
| `*` (Universal) | Memilih SEMUA elemen                     | `* { margin: 0; padding: 0; }`      |

Contoh lengkap:

```css
p {
  color: blue;
}
h1 {
  font-size: 24px;
}
.card {
  border: 1px solid #ccc;
  padding: 16px;
}
.highlight {
  background: yellow;
}
#header {
  background: navy;
  color: white;
}
#submit-btn {
  background: green;
}
```

```html
<div class="card highlight">Card dengan border dan background kuning</div>
<div id="header">Header</div>
<button id="submit-btn">Kirim</button>
```

---

## Combinator Selectors

| Selector                   | Penjelasan                             | Contoh                          |
| -------------------------- | -------------------------------------- | ------------------------------- |
| `A B` (Descendant)         | Elemen B di dalam A (semua level)      | `div p { color: red; }`         |
| `A > B` (Child)            | Anak langsung B dari A (level pertama) | `div > p { color: blue; }`      |
| `A + B` (Adjacent Sibling) | B langsung setelah A (selevel)         | `h2 + p { font-weight: bold; }` |
| `A ~ B` (General Sibling)  | Semua B setelah A (selevel)            | `h2 ~ p { color: gray; }`       |

---

## Attribute Selectors

| Selector          | Penjelasan                              | Contoh                                       |
| ----------------- | --------------------------------------- | -------------------------------------------- | ------ | ------------------------------------ |
| `[attr]`          | Elemen yang memiliki atribut tertentu   | `[disabled] { opacity: 0.5; }`               |
| `[attr="value"]`  | Atribut dengan nilai tepat              | `[type="text"] { border: 1px solid blue; }`  |
| `[attr^="value"]` | Atribut dimulai dengan nilai            | `a[href^="https"] { color: green; }`         |
| `[attr$="value"]` | Atribut diakhiri dengan nilai           | `a[href$=".pdf"]::after { content: " 📄"; }` |
| `[attr*="value"]` | Atribut mengandung nilai                | `a[href*="google"] { color: blue; }`         |
| `[attr~="value"]` | Atribut mengandung kata (dipisah spasi) | `[class~="active"] { font-weight: bold; }`   |
| `[attr            | ="value"]`                              | Atribut diawali nilai diikuti `-`            | `[lang | ="en"] { font-family: sans-serif; }` |

---

## Group Selector

| Selector  | Penjelasan                            | Contoh                               |
| --------- | ------------------------------------- | ------------------------------------ |
| `A, B, C` | Menerapkan style ke beberapa selector | `h1, h2, h3 { font-family: Arial; }` |

---

## Combining Selectors

```css
/* <a> dengan class "btn" di dalam <nav> */
nav a.btn {
  padding: 8px 16px;
}

/* <input> bertipe text yang required */
input[type="text"]:required {
  border: 2px solid orange;
}

/* <li> pertama di dalam <ul> dengan class "menu" */
ul.menu > li:first-child {
  border-top: none;
}

/* Semua <p> setelah <h2> di dalam <article> */
article h2 ~ p {
  line-height: 1.8;
}
```

---

## Specificity (Prioritas Selector)

| Selector                         | Contoh                      | Nilai |
| -------------------------------- | --------------------------- | ----- |
| Inline style                     | `style="..."`               | 1000  |
| ID                               | `#header`                   | 100   |
| Class / Attribute / Pseudo-class | `.card`, `[type]`, `:hover` | 10    |
| Element / Pseudo-element         | `div`, `p`, `::before`      | 1     |

```css
/* Specificity: 0,0,1 (element) */
p {
  color: blue;
}

/* Specificity: 0,1,0 (class) → menang */
.text {
  color: red;
}

/* Specificity: 1,0,0 (ID) → menang */
#special {
  color: green;
}

/* Specificity dihitung total: 0,1,1 */
p.text {
  color: orange;
}
```

### `!important`

| Property     | Penjelasan                                   | Contoh                         |
| ------------ | -------------------------------------------- | ------------------------------ |
| `!important` | Override specificity (gunakan sangat hemat!) | `p { color: red !important; }` |
