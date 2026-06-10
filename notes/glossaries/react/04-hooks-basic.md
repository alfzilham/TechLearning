# Hooks Basic

## Rules of Hooks

| Aturan | Penjelasan | Contoh |
|--------|-----------|--------|
| Top-level | Panggil di level teratas, bukan di if/loop | ✅ `useState()` di awal |
| Only in React functions | Hanya di function component atau custom hooks | ✅ `function Comp() { useState() }` |
| Prefix `use` | Semua hook harus diawali `use` | `useState`, `useEffect`, `useRef` |

---

## useState

Lihat file `03-state-props.md` untuk detail lengkap.

```jsx
const [count, setCount] = useState(0);
const [user, setUser] = useState({ nama: '', umur: 0 });
const [items, setItems] = useState([]);
```

---

## useEffect

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useEffect(fn, deps)` | Side effect (fetch, DOM, timer) | `useEffect(() => { fetch() }, [])` |
| No deps `[]` | Jalankan sekali (mount) | `useEffect(() => { }, [])` |
| With deps `[dep]` | Jalankan saat `dep` berubah | `useEffect(() => { }, [id])` |
| No array | Jalankan setiap render | `useEffect(() => { })` |
| Cleanup | Bersihkan effect (unmount/update) | `return () => { clearTimeout(id) }` |

```jsx
import { useState, useEffect } from 'react';

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  // Mount — fetch data
  useEffect(() => {
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(data => {
        setUser(data);
        setLoading(false);
      });
  }, [userId]); // refetch jika userId berubah

  // Timer dengan cleanup
  useEffect(() => {
    const timer = setInterval(() => {
      console.log('tick');
    }, 1000);

    return () => clearInterval(timer); // cleanup saat unmount
  }, []);

  // Event listener dengan cleanup
  useEffect(() => {
    const handler = (e) => console.log(e.key);
    window.addEventListener('keydown', handler);
    return () => window.removeEventListener('keydown', handler);
  }, []);

  if (loading) return <p>Loading...</p>;
  return <div>{user?.nama}</div>;
}
```

---

## useContext

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `createContext` | Buat context object | `const Theme = createContext('light')` |
| `.Provider` | Bungkus komponen yang butuh context | `<Theme.Provider value="dark">` |
| `useContext` | Konsumsi context dalam komponen | `const theme = useContext(Theme)` |

```jsx
import { createContext, useContext } from 'react';

// 1. Buat context
const ThemeContext = createContext('light');

// 2. Provider di root
function App() {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

// 3. Konsumsi di child
function Toolbar() {
  return <ThemeButton />;
}

function ThemeButton() {
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <button
      onClick={() => setTheme(t => t === 'light' ? 'dark' : 'light')}
      className={theme}
    >
      Theme: {theme}
    </button>
  );
}
```

---

## useReducer

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useReducer(reducer, initial)` | State management dengan reducer | `const [state, dispatch] = useReducer(reducer, { count: 0 })` |
| Lazy init | Inisialisasi dari function | `useReducer(reducer, initialArg, init)` |
| Action | Object dengan `type` | `{ type: 'increment' }` |
| Dispatch | Kirim action ke reducer | `dispatch({ type: 'increment' })` |

```jsx
import { useReducer } from 'react';

// Reducer — pure function
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    case 'reset':
      return { count: action.payload };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
      <button onClick={() => dispatch({ type: 'reset', payload: 0 })}>
        Reset
      </button>
    </div>
  );
}
```
