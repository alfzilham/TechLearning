# Advanced React Concepts

## Portals

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `createPortal(child, domNode)` | Render komponen di luar DOM parent | `createPortal(<Modal/>, document.body)` |
| Event bubbling | Event tetap naik ke parent React meski DOM beda | Klik di portal tetap terdeteksi parent |

```jsx
import { createPortal } from 'react-dom';

function Modal({ isOpen, onClose, children }) {
  if (!isOpen) return null;

  return createPortal(
    <div className="modal-backdrop" onClick={onClose}>
      <div className="modal-content" onClick={e => e.stopPropagation()}>
        <button onClick={onClose}>X</button>
        {children}
      </div>
    </div>,
    document.body // render di luar root app
  );
}

function App() {
  const [open, setOpen] = useState(false);
  return (
    <div>
      <button onClick={() => setOpen(true)}>Buka Modal</button>
      <Modal isOpen={open} onClose={() => setOpen(false)}>
        <h2>Judul Modal</h2>
        <p>Konten modal — DOM-nya di body, bukan di sini</p>
      </Modal>
    </div>
  );
}
```

---

## Error Boundaries

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `componentDidCatch` | Tangkap error di child component | Error boundary |
| `getDerivedStateFromError` | Update state setelah error | Return `{ hasError: true }` |
| Class component | Error boundary HARUS class component | Belum ada hook version |

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true, error };
  }

  componentDidCatch(error, errorInfo) {
    console.error('Error caught:', error, errorInfo);
    // Kirim ke error tracking service (Sentry, etc)
  }

  render() {
    if (this.state.hasError) {
      return (
        <div className="error-boundary">
          <h2>Terjadi kesalahan</h2>
          <p>{this.state.error?.message}</p>
          <button onClick={() => this.setState({ hasError: false })}>
            Coba lagi
          </button>
        </div>
      );
    }
    return this.props.children;
  }
}

// Penggunaan
function App() {
  return (
    <ErrorBoundary>
      <Dashboard />
    </ErrorBoundary>
  );
}
```

---

## Fragments

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `<> </>` | Fragment singkat (tidak bisa key) | `return <><h1/><p/></>` |
| `<Fragment>` | Fragment dengan key | `<Fragment key={id}><td/></Fragment>` |

```jsx
// Tanpa fragment — harus ada div wrapper = DOM berlebih
function TableRow({ item }) {
  return (
    <tr>
      <td>{item.id}</td>
      <td>{item.nama}</td>
    </tr>
  );
}

// Fragment — tanpa DOM tambahan
function Columns({ items }) {
  return items.map(item => (
    <React.Fragment key={item.id}>
      <td>{item.nama}</td>
      <td>{item.umur}</td>
    </React.Fragment>
  ));
}
```

---

## forwardRef

Lihat juga di `05-hooks-advanced.md`.

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `forwardRef(renderFn)` | Oper ref dari parent ke child | `const Input = forwardRef((props, ref) => <input ref={ref}/>)` |

```jsx
const FancyInput = forwardRef(function FancyInput(props, ref) {
  return <input ref={ref} className="fancy-input" {...props} />;
});

function Parent() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus(); // Auto focus
  }, []);

  return <FancyInput ref={inputRef} placeholder="Auto focus" />;
}
```

---

## React Server Components (RSC)

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Server Component | Rendered di server, bundle lebih kecil | Default di Next.js App Router |
| Client Component | Butuh interaktivitas, `"use client"` | State, effects, event handlers |
| "use client" | Batas antara server dan client | `"use client"; export default function Comp(){}` |

```jsx
// Server Component (default di Next.js App Router)
// — bisa async, akses DB langsung, tidak bisa pakai hooks
async function ProductList() {
  const products = await db.products.findMany();
  return (
    <ul>
      {products.map(p => <li key={p.id}>{p.nama}</li>)}
    </ul>
  );
}

// Client Component — butuh interaktivitas
// file: AddToCart.tsx
"use client";
import { useState } from 'react';

export default function AddToCart({ productId }) {
  const [added, setAdded] = useState(false);
  return (
    <button onClick={() => setAdded(true)}>
      {added ? '✓ Ditambahkan' : 'Tambah ke Keranjang'}
    </button>
  );
}
```

---

## StrictMode

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `<StrictMode>` | Detect potensi masalah di development | Hanya jalan di dev |
| Double render | Render 2x untuk deteksi side effect | `useEffect` cleanup test |
| Deprecation warning | Peringatan untuk API usang | |

```jsx
import { StrictMode } from 'react';

const root = createRoot(document.getElementById('root'));
root.render(
  <StrictMode>
    <App />
  </StrictMode>
);
```
