# JSX

## JSX Syntax

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| JSX expression | HTML-like syntax di JavaScript | `const el = <h1>Halo</h1>` |
| `{ }` embed | Menyisipkan ekspresi JS di JSX | `<p>{nama}</p>` |
| JSX adalah expression | Bisa dipakai di if, for, return | `return <div>{items}</div>` |
| Fragment `<> </>` | Bungkus elemen tanpa DOM tambahan | `return <><h1/><p/></>` |

```jsx
// JSX = JavaScript XML
const nama = "Rizky";
const element = <h1>Halo, {nama}!</h1>;

// Expression bisa berupa function, math, ternary
function salam(waktu) {
  return <p>Selamat {waktu}</p>;
}

const user = { nama: "Budi", umur: 25 };
const profile = (
  <div>
    <h2>{user.nama}</h2>
    <p>Umur: {user.umur}</p>
  </div>
);

// Fragment — tanpa elemen pembungkus
function Daftar() {
  return (
    <>
      <h1>Judul</h1>
      <p>Paragraf</p>
    </>
  );
}
```

---

## Atribut JSX

| Atribut HTML | JSX | Contoh |
|-------------|-----|--------|
| `class` | `className` | `<div className="card">` |
| `for` | `htmlFor` | `<label htmlFor="email">` |
| `style="color: red"` | `style={{color:'red'}}` | `style={{ fontSize: 16 }}` |
| `onclick` | `onClick` | `<button onClick={handleClick}>` |
| `tabindex` | `tabIndex` | `<div tabIndex={0}>` |

```jsx
// className
<div className="container active">
  <label htmlFor="email">Email</label>
  <input id="email" type="email" />
</div>

// Inline style — harus object dengan camelCase
const styles = {
  color: 'blue',
  fontSize: 16,
  backgroundColor: '#f0f0f0',
};
<div style={styles}>Teks biru</div>

// Template string untuk dynamic class
<div className={`card ${isActive ? 'active' : ''}`}>
```

---

## Conditional Rendering

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Ternary `? :` | If-else dalam JSX | `{isLogin ? <Profile/> : <Login/>}` |
| `&&` | Render jika true (tanpa else) | `{isLoading && <Spinner/>}` |
| `||` | Fallback jika falsy | `{nama || "Tamu"}` |
| Guard clause | Return early | `if (!user) return null;` |

```jsx
function Greeting({ isLogin, user }) {
  // Guard clause
  if (!user) return <p>Loading...</p>;

  return (
    <div>
      {/* Ternary */}
      {isLogin ? (
        <p>Selamat datang, {user.nama}!</p>
      ) : (
        <button onClick={login}>Login</button>
      )}

      {/* AND — render jika true */}
      {user.isAdmin && <AdminPanel />}

      {/* OR — fallback */}
      <p>{user.bio || "Belum ada bio"}</p>
    </div>
  );
}
```

---

## List & Keys

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `.map()` | Render array ke JSX | `{items.map(i => <Item key={i.id}/>)}` |
| `key` | Identitas unik elemen di list | `key={item.id}` |
| `key` index | Hanya jika data statis/tidak berurut | `key={index}` |

```jsx
function ItemList({ items }) {
  return (
    <ul>
      {items.map((item) => (
        <li key={item.id}>
          {item.nama} — Rp{item.harga}
        </li>
      ))}
    </ul>
  );
}

// Spread props
const user = { nama: "Rizky", umur: 25 };
<UserProfile {...user} />
// Sama dengan: <UserProfile nama="Rizky" umur={25} />
```
