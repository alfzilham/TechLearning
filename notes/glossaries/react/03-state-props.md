# State & Props

## useState

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useState` | Hook untuk state dalam functional component | `const [count, setCount] = useState(0)` |
| Initial value | Nilai awal state | `useState(0)` | `useState([])` |
| Lazy init | Initial value dari function (hitung sekali) | `useState(() => expensive())` |
| Updater function | Set state berdasarkan nilai sebelumnya | `setCount(c => c + 1)` |
| Immutable update | Jangan langsung mutate state | `setArr([...arr, newItem])` |

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
      {/* Updater function — aman untuk multiple update */}
      <button onClick={() => {
        setCount(c => c + 1);
        setCount(c => c + 1); // hasil: +2
      }}>+2</button>
    </div>
  );
}

function Form() {
  const [user, setUser] = useState({ nama: '', umur: 0 });

  // Immutable update — spread object
  const updateNama = (e) => {
    setUser(prev => ({ ...prev, nama: e.target.value }));
  };

  return (
    <input value={user.nama} onChange={updateNama} />
  );
}
```

---

## Lifting State Up

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Lifting up | State diangkat ke parent | Parent punya state, child via props |
| Props drilling | State dioper melalui banyak level | Masalah — Context API solusinya |

```jsx
// State di parent, dioper ke children via props
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <Child count={count} />
      <Controls onIncrement={() => setCount(c => c + 1)} />
    </div>
  );
}

function Child({ count }) {
  return <p>Count: {count}</p>;
}

function Controls({ onIncrement }) {
  return <button onClick={onIncrement}>+1</button>;
}
```

---

## State Array & Object Patterns

| Pattern | Penjelasan | Contoh |
|---------|-----------|--------|
| Add to array | Tambah item | `setItems([...items, newItem])` |
| Update in array | Ubah item tertentu | `setItems(items.map(i => i.id === id ? {...i, done: true} : i))` |
| Remove from array | Hapus item | `setItems(items.filter(i => i.id !== id))` |
| Update object | Ubah properti | `setUser({...user, nama: "baru"})` |
| Nested update | Ubah properti bersarang | `setData({...data, a: {...data.a, b: val}})` |

```jsx
function TodoList() {
  const [todos, setTodos] = useState([]);

  const addTodo = (text) => {
    setTodos([...todos, { id: Date.now(), text, done: false }]);
  };

  const toggleTodo = (id) => {
    setTodos(todos.map(t =>
      t.id === id ? { ...t, done: !t.done } : t
    ));
  };

  const removeTodo = (id) => {
    setTodos(todos.filter(t => t.id !== id));
  };

  return (
    <ul>
      {todos.map(t => (
        <li key={t.id} className={t.done ? 'done' : ''}>
          {t.text}
        </li>
      ))}
    </ul>
  );
}
```
