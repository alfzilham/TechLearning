# Hooks Advanced

## useMemo

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useMemo(fn, deps)` | Memoize hasil kalkulasi | `const total = useMemo(() => sum(items), [items])` |
| Dependency array | Ulang kalkulasi jika deps berubah | `[items]` |
| Referential equality | Menjaga referensi object/array tetap sama | `useMemo(() => ({x:1}), [])` |

```jsx
import { useMemo } from 'react';

function Cart({ items }) {
  // Hanya kalkulasi ulang jika items berubah
  const total = useMemo(() => {
    return items.reduce((sum, item) => sum + item.price * item.qty, 0);
  }, [items]);

  const diskon = useMemo(() => {
    return total > 100000 ? total * 0.1 : 0;
  }, [total]);

  // Menjaga referensi object agar tidak trigger re-render
  const config = useMemo(() => ({
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
  }), []);

  return <p>Total: Rp{total - diskon}</p>;
}
```

---

## useCallback

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useCallback(fn, deps)` | Memoize function | `const handle = useCallback(() => { }, [])` |
| Stable reference | Function tetap sama antar render | Penting untuk child yang di-memo |

```jsx
import { useState, useCallback, memo } from 'react';

// Child — hanya re-render jika props berubah
const Button = memo(({ label, onClick }) => {
  console.log('render:', label);
  return <button onClick={onClick}>{label}</button>;
});

function Parent() {
  const [count, setCount] = useState(0);

  // Tanpa useCallback — function baru setiap render → child re-render
  const handleClick = useCallback(() => {
    setCount(c => c + 1);
  }, []); // kosong karena pakai updater function

  // useCallback dengan dependency
  const handleSave = useCallback(async () => {
    await fetch('/api/save', { method: 'POST', body: JSON.stringify({ count }) });
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <Button label="Tambah" onClick={handleClick} />
      <Button label="Simpan" onClick={handleSave} />
    </div>
  );
}
```

---

## useRef

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useRef(initial)` | Menyimpan nilai yang persisten antar render | `const ref = useRef(0)` |
| `.current` | Akses nilai ref | `ref.current` |
| DOM ref | Referensi ke elemen DOM | `<input ref={inputRef} />` |
| Mutable value | Tidak trigger re-render saat berubah | `ref.current = newValue` |

```jsx
import { useState, useRef, useEffect } from 'react';

function VideoPlayer() {
  const [playing, setPlaying] = useState(false);
  const videoRef = useRef(null);
  const clickCount = useRef(0); // tidak trigger re-render

  useEffect(() => {
    if (playing) {
      videoRef.current.play();
    } else {
      videoRef.current.pause();
    }
  }, [playing]);

  const handleClick = () => {
    clickCount.current += 1;
    setPlaying(!playing);
  };

  return (
    <div>
      <video ref={videoRef} src="video.mp4" width="400" />
      <button onClick={handleClick}>
        {playing ? 'Pause' : 'Play'}
      </button>
      <p>Diklik: {clickCount.current} kali</p>
    </div>
  );
}
```

---

## useImperativeHandle & forwardRef

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `forwardRef` | Oper ref ke child component | `const Comp = forwardRef((props, ref) => ...)` |
| `useImperativeHandle` | Ekspos method spesifik ke parent | `useImperativeHandle(ref, () => ({ focus }))` |

```jsx
import { forwardRef, useImperativeHandle, useRef } from 'react';

// Child — ekspos method focus() ke parent
const CustomInput = forwardRef((props, ref) => {
  const inputRef = useRef(null);

  useImperativeHandle(ref, () => ({
    focus: () => inputRef.current.focus(),
    clear: () => { inputRef.current.value = ''; },
    getValue: () => inputRef.current.value,
  }));

  return <input ref={inputRef} {...props} />;
});

function Parent() {
  const inputRef = useRef(null);

  return (
    <div>
      <CustomInput ref={inputRef} placeholder="Teks..." />
      <button onClick={() => inputRef.current.focus()}>Focus</button>
      <button onClick={() => inputRef.current.clear()}>Clear</button>
    </div>
  );
}
```

---

## useLayoutEffect

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useLayoutEffect` | Sama seperti useEffect, tapi jalan synchronous setelah DOM | `useLayoutEffect(() => { }, [])` |
| useEffect | Async — setelah paint | Untuk fetch, log |
| useLayoutEffect | Sync — sebelum paint | Untuk ukuran DOM, animasi |

```jsx
import { useState, useLayoutEffect, useRef } from 'react';

function Tooltip({ text }) {
  const ref = useRef(null);
  const [position, setPosition] = useState({ top: 0, left: 0 });

  // useLayoutEffect — ukur DOM sebelum browser paint
  useLayoutEffect(() => {
    if (ref.current) {
      const rect = ref.current.getBoundingClientRect();
      setPosition({
        top: rect.bottom + 4,
        left: rect.left,
      });
    }
  }, [text]);

  return (
    <div ref={ref} style={{ position: 'absolute', ...position }}>
      {text}
    </div>
  );
}
```
