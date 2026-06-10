# Components & Props

## Komponen Functional

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Function component | Fungsi yang return JSX | `function Card() { return <div/> }` |
| Arrow component | Komponen dengan arrow function | `const Card = () => <div/>` |
| Export | Named / default export | `export default Card` |
| Props | Parameter dari parent | `function Card({ title, desc })` |
| Default props | Nilai default parameter | `function Card({ title = "Judul" })` |

```jsx
// Functional component
function Card({ title, desc, children }) {
  return (
    <div className="card">
      <h2>{title}</h2>
      <p>{desc}</p>
      {children}
    </div>
  );
}

// Arrow component
const Button = ({ label, onClick, variant = "primary" }) => (
  <button className={`btn btn-${variant}`} onClick={onClick}>
    {label}
  </button>
);

// Penggunaan
function App() {
  return (
    <Card title="Judul Card" desc="Deskripsi">
      <Button label="Klik" onClick={() => alert("hi")} />
    </Card>
  );
}

export default App;
```

---

## Props

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Destructure props | Ambil langsung nama propertinya | `({ nama, umur })` |
| Rest props | Kumpulkan sisa props | `({ base, ...rest })` |
| Spread props | Oper semua properti | `<Comp {...obj} />` |
| Children | Konten di antara tag | `{children}` |

```jsx
// Props pattern
function UserCard({ nama, umur, role = "user", ...rest }) {
  return (
    <div className="card" {...rest}>
      <h3>{nama}</h3>
      <p>Umur: {umur}</p>
      <p>Role: {role}</p>
    </div>
  );
}

// Children — komposisi
function Container({ children, title }) {
  return (
    <section>
      <h2>{title}</h2>
      <div className="content">{children}</div>
    </section>
  );
}

<Container title="Profil">
  <p>Ini konten</p>
  <button>Simpan</button>
</Container>
```

---

## Komposisi (Composition Pattern)

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `children` | Slot default | `{children}` |
| Named slots | Multiple children area | `{header}{sidebar}{content}` |
| Render props | Prop yang berisi function render | `renderItem={(item) => <div/>}` |

```jsx
// Named slots pattern
function Layout({ header, sidebar, main }) {
  return (
    <div className="layout">
      <header>{header}</header>
      <aside>{sidebar}</aside>
      <main>{main}</main>
    </div>
  );
}

<Layout
  header={<Navbar />}
  sidebar={<SideMenu />}
  main={<Dashboard />}
/>

// Render props
function List({ items, renderItem }) {
  return (
    <ul>
      {items.map((item, i) => (
        <li key={i}>{renderItem(item)}</li>
      ))}
    </ul>
  );
}

<List items={users} renderItem={(u) => <span>{u.nama}</span>} />
```
