# 11 - Animation & Transition

## Transition

| Property/Fungsi              | Penjelasan                               | Contoh                                     |
| ---------------------------- | ---------------------------------------- | ------------------------------------------ |
| `transition-property`        | Properti yang akan ditransisikan         | `transition-property: transform, opacity;` |
| `transition-duration`        | Lama transisi                            | `transition-duration: 0.3s;`               |
| `transition-timing-function` | Kecepatan / percepatan transisi          | `transition-timing-function: ease;`        |
| `transition-delay`           | Tunda sebelum transisi mulai             | `transition-delay: 0.1s;`                  |
| `transition` (Shorthand)     | Semua properti transisi dalam satu baris | `transition: all 0.3s ease;`               |

```css
.ease {
  transition-timing-function: ease;
}
.linear {
  transition-timing-function: linear;
}
.ease-in {
  transition-timing-function: ease-in;
}
.ease-out {
  transition-timing-function: ease-out;
}
.custom {
  transition-timing-function: cubic-bezier(0.42, 0, 0.58, 1);
}
.steps {
  transition-timing-function: steps(4, end);
}

.multi {
  transition:
    transform 0.3s ease,
    opacity 0.2s ease 0.1s;
}

button {
  background: blue;
  color: white;
  transition: all 0.3s ease;
}
button:hover {
  background: darkblue;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}
```

### Properti yang bisa di-transition:

`opacity`, `transform`, `color`, `background`, `width`, `height`, `margin`, `padding`, `border`, `box-shadow`, `filter`, `top`, `left`, dll.

### Properti yang TIDAK bisa di-transition:

`display`, `font-family`, `position`, `float`, `clear`, `overflow`, dll.

---

## Transform

| Property/Fungsi    | Penjelasan               | Contoh                              |
| ------------------ | ------------------------ | ----------------------------------- |
| `translate(x, y)`  | Menggeser elemen         | `transform: translate(10px, 20px);` |
| `scale(n)`         | Memperbesar/memperkecil  | `transform: scale(1.1);`            |
| `rotate(deg)`      | Memutar elemen           | `transform: rotate(45deg);`         |
| `skew(deg)`        | Memiringkan elemen       | `transform: skew(10deg);`           |
| `transform-origin` | Titik pusat transformasi | `transform-origin: center;`         |

```css
.box:hover {
  transform: translateX(10px) scale(1.1) rotate(5deg);
}
.box:active {
  transform: scale(0.95);
}
.box {
  transform: scale(1.5, 0.5);
}
.box {
  transform: rotate(-90deg);
}
.box {
  transform: rotate(1turn);
}
.box {
  transform: skew(10deg, 5deg);
}

/* 3D Transforms */
.container {
  perspective: 1000px;
}
.card {
  transform: rotateY(45deg);
}
.card:hover {
  transform: rotateY(180deg);
  transition: transform 0.5s;
}
```

---

## Animation & Keyframes

| Property/Fungsi             | Penjelasan                              | Contoh                                                          |
| --------------------------- | --------------------------------------- | --------------------------------------------------------------- |
| `@keyframes`                | Mendefinisikan animasi                  | `@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }` |
| `animation-name`            | Nama keyframes yang digunakan           | `animation-name: fadeIn;`                                       |
| `animation-duration`        | Lama animasi sekali putaran             | `animation-duration: 1s;`                                       |
| `animation-timing-function` | Kecepatan animasi                       | `animation-timing-function: ease;`                              |
| `animation-delay`           | Tunda sebelum animasi mulai             | `animation-delay: 0.5s;`                                        |
| `animation-iteration-count` | Berapa kali animasi diulang             | `animation-iteration-count: infinite;`                          |
| `animation-direction`       | Arah animasi                            | `animation-direction: alternate;`                               |
| `animation-fill-mode`       | Style sebelum/setelah animasi           | `animation-fill-mode: forwards;`                                |
| `animation-play-state`      | Jeda / lanjutkan animasi                | `animation-play-state: paused;`                                 |
| `animation` (Shorthand)     | Semua properti animasi dalam satu baris | `animation: fadeIn 1s ease 0.5s 1 normal forwards;`             |

```css
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@keyframes slideIn {
  0% {
    transform: translateX(-100%);
    opacity: 0;
  }
  100% {
    transform: translateX(0);
    opacity: 1;
  }
}
@keyframes bounce {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

.box {
  animation: fadeIn 1s ease 0.5s 1 normal forwards;
}
.spinner {
  animation: spin 1s linear infinite;
}
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.multi {
  animation:
    fadeIn 0.5s ease,
    slideIn 0.5s ease 0.2s;
}

.card:hover {
  animation-play-state: paused;
}
```

---

## Common Animations

```css
/* Fade In */
.fade-in {
  animation: fadeIn 0.5s ease forwards;
}
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Slide In */
.slide-in {
  animation: slideIn 0.3s ease forwards;
}
@keyframes slideIn {
  from {
    transform: translateY(20px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

/* Pulse */
.pulse {
  animation: pulse 2s infinite;
}
@keyframes pulse {
  0%,
  100% {
    opacity: 1;
  }
  50% {
    opacity: 0.5;
  }
}

/* Shake */
.shake {
  animation: shake 0.3s ease;
}
@keyframes shake {
  0%,
  100% {
    transform: translateX(0);
  }
  25% {
    transform: translateX(-5px);
  }
  75% {
    transform: translateX(5px);
  }
}

/* Loading Spinner */
.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid #e0e0e0;
  border-top-color: #0066ff;
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}
@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}
```
