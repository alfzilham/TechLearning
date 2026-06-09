# 05 - Display & Position

## Display

| Properti                | Penjelasan                                              | Contoh                   |
| ----------------------- | ------------------------------------------------------- | ------------------------ |
| `display: block`        | Menempati seluruh lebar, mulai dari baris baru          | `display: block;`        |
| `display: inline`       | Hanya selebar konten, tidak bisa diberi width/height    | `display: inline;`       |
| `display: inline-block` | Inline tapi bisa diberi width/height dan padding/margin | `display: inline-block;` |
| `display: none`         | Menyembunyikan elemen (tidak memakan ruang)             | `display: none;`         |
| `display: flex`         | Flexbox — lihat file 06                                 | `display: flex;`         |
| `display: grid`         | Grid — lihat file 07                                    | `display: grid;`         |

Contoh lengkap:

```css
.block {
  display: block;
  width: 200px;
  height: 100px;
}
.inline {
  display: inline;
}
.btn {
  display: inline-block;
  width: 120px;
  height: 40px;
  padding: 8px 16px;
}
.hidden {
  display: none;
}
```

---

## Position

| Properti             | Penjelasan                                             | Contoh                                       |
| -------------------- | ------------------------------------------------------ | -------------------------------------------- |
| `position: static`   | Default — mengikuti alur normal dokumen                | `position: static;`                          |
| `position: relative` | Relatif terhadap posisi normalnya                      | `position: relative; top: 10px; left: 20px;` |
| `position: absolute` | Relatif terhadap parent terdekat yang `relative`       | `position: absolute; top: 0; right: 0;`      |
| `position: fixed`    | Relatif terhadap viewport — tetap saat scroll          | `position: fixed; top: 0; left: 0;`          |
| `position: sticky`   | Relative + fixed — menempel saat scroll mencapai batas | `position: sticky; top: 0;`                  |

Contoh lengkap:

```css
.parent {
  position: relative;
}
.child-absolute {
  position: absolute;
  top: 0;
  right: 0;
}

.fixed-header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
}
.fixed-whatsapp {
  position: fixed;
  bottom: 20px;
  right: 20px;
}
.sticky-nav {
  position: sticky;
  top: 0;
}
.sticky-sidebar {
  position: sticky;
  top: 20px;
}
```

---

## Z-Index

| Properti  | Penjelasan                                        | Contoh           |
| --------- | ------------------------------------------------- | ---------------- |
| `z-index` | Tumpukan elemen (semakin besar, semakin di depan) | `z-index: 1000;` |

```css
.modal {
  position: fixed;
  z-index: 1000;
}
.backdrop {
  position: fixed;
  z-index: 999;
}
.content {
  z-index: 1;
}
/* z-index hanya bekerja pada element yang position-nya bukan static */
```

---

## Float

| Properti | Penjelasan                        | Contoh         |
| -------- | --------------------------------- | -------------- |
| `float`  | Mengapungkan elemen ke kiri/kanan | `float: left;` |
| `clear`  | Menghentikan efek float           | `clear: both;` |

Contoh lengkap:

```css
.float-left {
  float: left;
  margin-right: 16px;
}
.float-right {
  float: right;
  margin-left: 16px;
}
.clear-left {
  clear: left;
}
.clear-both {
  clear: both;
}

/* Clearfix hack */
.clearfix::after {
  content: "";
  display: table;
  clear: both;
}
```

---

## Visibility

| Properti              | Penjelasan                                     | Contoh                 |
| --------------------- | ---------------------------------------------- | ---------------------- |
| `visibility: hidden`  | Menyembunyikan elemen tapi tetap memakan ruang | `visibility: hidden;`  |
| `visibility: visible` | Menampilkan elemen                             | `visibility: visible;` |

Perbedaan `display: none` vs `visibility: hidden`:

```css
.hidden1 {
  display: none;
} /* hilang total, tidak ada ruang */
.hidden2 {
  visibility: hidden;
} /* tidak terlihat, ruang tetap */
```

---

## Contoh Lengkap

```css
/* Header tetap di atas */
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 60px;
  background: white;
  z-index: 100;
}

/* Sidebar sticky */
.sidebar {
  position: sticky;
  top: 80px;
}

/* Badge absolute di pojok card */
.card {
  position: relative;
}
.badge {
  position: absolute;
  top: -10px;
  right: -10px;
  background: red;
  color: white;
  border-radius: 50%;
  width: 24px;
  height: 24px;
}

/* Clearfix */
.container::after {
  content: "";
  display: block;
  clear: both;
}
```
