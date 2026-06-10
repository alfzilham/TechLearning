# Performance

## React.memo

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `memo(Comp)` | Mencegah re-render jika props tidak berubah | `const Memo = memo(Expensive)` |
| Shallow compare | Membandingkan props secara dangkal | Object baru → dianggap berubah |
| Custom comparator | `memo(Comp, (prev, next) => prev.id === next.id)` | Untuk kontrol lebih |

```jsx
import { memo, useState } from 'react';

// Hanya re-render jika props berubah
const ExpensiveList = memo(function ExpensiveList({ items }) {
  console.log('render list');
  return (
    <ul>
      {items.map(item => <li key={item.id}>{item.nama}</li>)}
    </ul>
  );
});

function App() {
  const [count, setCount] = useState(0);
  const [items, setItems] = useState([...]);

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(c => c + 1)}>+1</button>
      {/* ExpensiveList tidak re-render saat count berubah */}
      <ExpensiveList items={items} />
    </div>
  );
}
```

---

## useMemo

Sudah di file `05-hooks-advanced.md`. Fokus: memoize hasil kalkulasi.

```jsx
function CartSummary({ items }) {
  const total = useMemo(() => {
    return items.reduce((sum, item) => sum + item.price * item.qty, 0);
  }, [items]);

  return <p>Total: Rp{total.toLocaleString()}</p>;
}
```

---

## useCallback

Sudah di `05-hooks-advanced.md`. Fokus: menjaga referensi function.

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount(c => c + 1);
  }, []);

  return <Child onClick={increment} />;
}
```

---

## lazy & Suspense

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `React.lazy()` | Code splitting — load komponen saat dibutuhkan | `const Lazy = lazy(() => import('./Comp'))` |
| `<Suspense>` | Fallback selama loading | `<Suspense fallback={<Loading/>}>` |
| Route-based splitting | lazy per route | Paling umum dan efektif |

```jsx
import { lazy, Suspense } from 'react';
import { Routes, Route } from 'react-router-dom';

// Code splitting per route — load saat user navigasi
const Home = lazy(() => import('./pages/Home'));
const About = lazy(() => import('./pages/About'));
const Dashboard = lazy(() => import('./pages/Dashboard'));

function App() {
  return (
    <Suspense fallback={<div className="loading">Loading...</div>}>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/dashboard" element={<Dashboard />} />
      </Routes>
    </Suspense>
  );
}

// lazy untuk komponen berat (chart, editor, dll)
const Chart = lazy(() => import('./Chart'));
const MDEditor = lazy(() => import('./MDEditor'));
```

---

## Profiler & React DevTools

| Tools | Penjelasan |
|-------|-----------|
| React DevTools | Inspect komponen, props, state |
| Profiler | Rekam & analisis re-render |
| `why-did-you-render` | Library untuk deteksi re-render tidak perlu |

```jsx
import { Profiler } from 'react';

function onRender(id, phase, actualDuration) {
  console.log(`${id} (${phase}): ${actualDuration}ms`);
}

function App() {
  return (
    <Profiler id="App" onRender={onRender}>
      <Dashboard />
    </Profiler>
  );
}
```

---

## Window & Virtualization

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| react-window | Render hanya item yang terlihat | `import { FixedSizeList } from 'react-window'` |
| FixedSizeList | Semua item tinggi sama | `height={400} itemCount={1000} itemSize={50}` |
| VariableSizeList | Item tinggi berbeda | `import { VariableSizeList } from 'react-window'` |

```jsx
import { FixedSizeList } from 'react-window';

function VirtualList({ items }) {
  const Row = ({ index, style }) => (
    <div style={style} className="item">
      {items[index].nama}
    </div>
  );

  return (
    <FixedSizeList
      height={400}
      itemCount={items.length}
      itemSize={50}
      width="100%"
    >
      {Row}
    </FixedSizeList>
  );
}

// Hanya render ~10 elemen meskipun items 10000!
```
