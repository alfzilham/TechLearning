# Custom Hooks

## Dasar Custom Hook

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useXxx` | Naming convention — harus diawali `use` | `function useFetch(url)` |
| Reusable logic | Ekstrak logic dari komponen | Bisa dipakai di banyak komponen |
| Tidak share state | Setiap panggilan punya state sendiri | `useFetch(1)` dan `useFetch(2)` independen |
| Compose hooks | Bisa panggil hook lain di dalamnya | `useEffect`, `useState` di dalam custom hook |

```jsx
import { useState, useEffect } from 'react';

// Custom hook — fetch data
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    let cancelled = false;

    const fetchData = async () => {
      try {
        setLoading(true);
        const res = await fetch(url);
        const json = await res.json();
        if (!cancelled) {
          setData(json);
          setError(null);
        }
      } catch (err) {
        if (!cancelled) setError(err.message);
      } finally {
        if (!cancelled) setLoading(false);
      }
    };

    fetchData();
    return () => { cancelled = true; };
  }, [url]);

  return { data, loading, error };
}

// Pakai di komponen
function UserList() {
  const { data: users, loading, error } = useFetch('/api/users');

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  return <div>{users.map(u => <p key={u.id}>{u.nama}</p>)}</div>;
}
```

---

## Contoh Custom Hooks

### `useLocalStorage`
```jsx
function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    try {
      const item = localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch {
      return initialValue;
    }
  });

  useEffect(() => {
    try {
      localStorage.setItem(key, JSON.stringify(value));
    } catch { /* quota exceeded */ }
  }, [key, value]);

  return [value, setValue];
}

// Penggunaan
function App() {
  const [theme, setTheme] = useLocalStorage('theme', 'light');
  const [user, setUser] = useLocalStorage('user', null);
  return <div className={theme}>...</div>;
}
```

### `useDebounce`
```jsx
import { useState, useEffect } from 'react';

function useDebounce(value, delay = 300) {
  const [debounced, setDebounced] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(timer);
  }, [value, delay]);

  return debounced;
}

// Penggunaan
function Search() {
  const [query, setQuery] = useState('');
  const debouncedQuery = useDebounce(query, 500);

  useEffect(() => {
    if (debouncedQuery) fetch(`/api/search?q=${debouncedQuery}`);
  }, [debouncedQuery]);

  return <input value={query} onChange={e => setQuery(e.target.value)} />;
}
```

### `useToggle`
```jsx
function useToggle(initial = false) {
  const [value, setValue] = useState(initial);
  const toggle = useCallback(() => setValue(v => !v), []);
  const setTrue = useCallback(() => setValue(true), []);
  const setFalse = useCallback(() => setValue(false), []);

  return [value, { toggle, setTrue, setFalse, set: setValue }];
}

// Penggunaan
function Panel() {
  const [isOpen, { toggle, setTrue, setFalse }] = useToggle(false);
  return (
    <div>
      <button onClick={toggle}>{isOpen ? 'Tutup' : 'Buka'}</button>
      {isOpen && <div>Konten panel...</div>}
    </div>
  );
}
```

### `useMediaQuery`
```jsx
function useMediaQuery(query) {
  const [matches, setMatches] = useState(false);

  useEffect(() => {
    const mql = window.matchMedia(query);
    const handler = (e) => setMatches(e.matches);
    mql.addEventListener('change', handler);
    setMatches(mql.matches);
    return () => mql.removeEventListener('change', handler);
  }, [query]);

  return matches;
}

// Penggunaan
function Header() {
  const isMobile = useMediaQuery('(max-width: 768px)');
  const isDark = useMediaQuery('(prefers-color-scheme: dark)');

  return <div>{isMobile ? <MobileNav /> : <DesktopNav />}</div>;
}
```

### `useOnClickOutside`
```jsx
function useOnClickOutside(ref, handler) {
  useEffect(() => {
    const listener = (e) => {
      if (!ref.current || ref.current.contains(e.target)) return;
      handler(e);
    };
    document.addEventListener('mousedown', listener);
    document.addEventListener('touchstart', listener);
    return () => {
      document.removeEventListener('mousedown', listener);
      document.removeEventListener('touchstart', listener);
    };
  }, [ref, handler]);
}

// Penggunaan
function Dropdown() {
  const ref = useRef(null);
  const [open, setOpen] = useState(false);
  useOnClickOutside(ref, () => setOpen(false));

  return (
    <div ref={ref}>
      <button onClick={() => setOpen(!open)}>Menu</button>
      {open && <div className="dropdown">...</div>}
    </div>
  );
}
```
