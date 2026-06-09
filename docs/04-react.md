# Phase 4: React

**Durasi:** 21 hari (Minggu 5-7)
**Tujuan:** Membangun Single Page Application dengan komponen reusable

---

## Kenapa React?

React adalah library untuk membangun user interface. Dengan React, Anda membuat **komponen** (potongan UI independen) lalu merangkainya jadi halaman utuh. React mengelola DOM secara efisien — Anda cukup bilang **"seperti apa UI-nya"**, React yang urus **"gimana cara update-nya"**.

---

## Minggu 5: React Dasar

### Hari 1: Setup & JSX

**Konsep:**
- `npm create vite@latest` — setup project React dengan Vite
- Struktur folder project React
- `main.tsx` → entry point, `App.tsx` → root component
- JSX: JavaScript XML — HTML-like syntax di dalam JS
- Aturan JSX:
  - Harus 1 parent element (atau `<> </>` Fragment)
  - `class` → `className`
  - Inline style: `style={{ color: 'red' }}` (object, bukan string)
  - Expression dalam `{}`
- Komponen pertama: function yang return JSX

**Tugas:**
```tsx
// Buat komponen Header, MainContent, Footer
// Render di App.tsx
// Setiap komponen di file terpisah
// Gunakan Props: <Header title="My App" />
```

---

### Hari 2: Props & Children

**Konsep:**
- Props adalah parameter yang dikirim ke komponen
- Type props dengan interface
- Destructuring props
- `children` prop — komponen yang dibungkus
- Default props
- `key` prop (kenapa penting di list)

**Tugas:**
```tsx
// 1. Buat komponen Card dengan props: title, description, imageUrl, variant ('primary' | 'secondary')
// 2. Buat komponen CardList yang menerima array CardData sebagai props
// 3. Buat komponen Layout dengan children prop
```

---

### Hari 3: Conditional Rendering & List

**Konsep:**
- Ternary: `{isLoggedIn ? <Dashboard /> : <Login />}`
- `&&` short-circuit: `{isAdmin && <AdminPanel />}`
- `||` fallback
- Render list dengan `.map()` + `key`
- Fragment `<> </>` untuk grouping tanpa DOM node

**Tugas:**
```tsx
// 1. Tampilkan daftar user dari array
// 2. Kalo array kosong, tampilkan "Tidak ada user"
// 3. Ada tombol filter: tampilkan hanya user aktif
```

---

### Hari 4: useState — State Management Dasar

**Konsep:**
- `const [count, setCount] = useState(0)`
- State itu immutable — jangan di-mutate langsung
- Cara update yang benar: `setCount(prev => prev + 1)`
- State di komponen itu **privat** dan **independen**
- `useState` dengan object atau array

**Tugas:**
```tsx
// 1. Counter (+1, -1, reset)
// 2. Form controlled component: input.text → value + onChange
// 3. Daftar item: tambah, hapus, toggle
// 4. State object: { name, email, age } dengan form terpisah
```

**PENTING:**
```tsx
// SALAH:
const [user, setUser] = useState({ name: '', age: 0 });
user.name = 'John'; // ❌ Mutating directly!

// BENAR:
setUser({ ...user, name: 'John' }); // ✅ Spread + override
```

---

### Hari 5: useEffect — Side Effects

**Konsep:**
- `useEffect(() => {}, [])` — jalan sekali setelah render (mount)
- `useEffect(() => {}, [count])` — jalan setiap `count` berubah
- `useEffect(() => { return () => {} }, [])` — cleanup function (unmount)
- Dependency array kosong `[]` ≠ tanpa dependency array
- Common use cases:
  - Fetch data saat mount
  - Subscribe/unsubscribe event
  - Update document.title
  - Timer (setTimeout/setInterval + cleanup)

**Tugas:**
```tsx
// 1. Fetch users dari JSONPlaceholder saat mount, simpan di state
// 2. Update document.title setiap count berubah
// 3. Timer: detik berjalan, ada tombol start/stop
// 4. Window resize listener (dengan cleanup)
```

---

### Hari 6: Forms & Controlled Components

**Konsep:**
- Controlled vs Uncontrolled
- Input: `value` + `onChange`
- Select, checkbox, radio, textarea
- Form submission: `onSubmit` + `event.preventDefault()`
- Validasi: inline error message
- `useRef` untuk uncontrolled (fokus input)

**Tugas:**
```tsx
// 1. Form registrasi: name, email, password, confirmPassword, role (select), agree (checkbox)
// 2. Validasi: email format, password >= 6 char, confirmPassword harus sama
// 3. Tampilkan error message per field
// 4. Submit → simpan ke array users (state lokal)
```

---

### Hari 7: Mini Project Week 1 — Product Catalog

Buat aplikasi katalog produk dengan:

1. **Header** — judul + navigasi
2. **Product List** — grid produk dari data statis array
3. **Search Bar** — filter produk berdasarkan nama (controlled input + state)
4. **Category Filter** — dropdown filter kategori
5. **Product Card** — gambar, nama, harga, stok
6. **Loading state** — simulasi delay (setTimeout di useEffect)
7. **Error state** — kalo data kosong

**Data:**
```ts
interface Product {
  id: number;
  name: string;
  price: number;
  category: string;
  image: string;
  stock: number;
}
```

---

## Minggu 6: React Intermediate

### Hari 8: useRef & Custom Hooks

**Konsep:**
- `useRef`: menyimpan nilai yang tidak trigger re-render
  - Referensi DOM: `inputRef.current.focus()`
  - Menyimpan nilai sebelumnya (previous value)
  - Timer ID
- Custom hooks: function yang pakai hooks React
  - Nama harus `useXxx`
  - Bisa pakai hooks lain di dalamnya

**Tugas:**
```tsx
// Custom hooks:
// 1. useLocalStorage<T>(key, initialValue) — baca/tulis localStorage
// 2. useDebounce<T>(value, delay) — debounce value
// 3. useFetch<T>(url) — return { data, loading, error }
// 4. Gunakan semua di komponen
```

---

### Hari 9: useMemo & useCallback

**Konsep:**
- `useMemo(() => expensiveCalculation(data), [data])` — memoize value
- `useCallback(() => handler, [deps])` — memoize function
- Kenapa perlu? — performance optimization, referensi stabil buat useEffect
- **JANGAN** dipake di semua tempat — hanya untuk kalkulasi mahal
- React DevTools untuk profiling

**Tugas:**
```tsx
// 1. Daftar 10000 item dengan search filter
// 2. Tanpa useMemo: search jadi lambat
// 3. Dengan useMemo: filter di-cache sampai search term berubah
// 4. Bandingkan performa
```

---

### Hari 10: Context API

**Konsep:**
- `createContext`, `Provider`, `useContext`
- Props drilling → solusi dengan context
- Kapan pake context? — theme, auth, language preference
- Kapan TIDAK pake context? — data yang sering berubah (bisa trigger banyak re-render)

**Tugas:**
```tsx
// 1. Buat ThemeContext: 'light' | 'dark'
// 2. ThemeProvider di root
// 3. Tombol toggle theme di header
// 4. Semua komponen menyesuaikan warna berdasarkan theme
// 5. Simpan preferensi theme di localStorage
```

---

### Hari 11: useReducer — Complex State Logic

**Konsep:**
- `useReducer(reducer, initialState)` — alternatif useState untuk state kompleks
- `reducer(state, action) => newState`
- Action: `{ type: 'ACTION_NAME', payload? }`
- Kapan pakai useReducer vs useState:
  - useState: state sederhana (string, number, boolean)
  - useReducer: state dengan banyak field & banyak cara update

**Tugas:**
```tsx
// Implementasi Todo List dengan useReducer:
interface TodoState {
  todos: Todo[];
  filter: 'all' | 'active' | 'completed';
}

type TodoAction =
  | { type: 'ADD'; payload: string }
  | { type: 'TOGGLE'; payload: number }
  | { type: 'DELETE'; payload: number }
  | { type: 'SET_FILTER'; payload: TodoState['filter'] };

// Reducer function + komponen
```

---

### Hari 12: React Router — Multi Page

**Konsep:**
- `npm install react-router-dom`
- `createBrowserRouter` + `RouterProvider`
- `<Route path="/" element={<Home />} />`
- Nested routes: `layout.tsx` dengan `<Outlet />`
- Dynamic routes: `/products/:id`
- `useParams()`, `useNavigate()`, `useLocation()`
- `Link` vs `NavLink`
- `loader` & `action` (data loading sebelum render)

**Tugas:**
```tsx
// Routes: /, /products, /products/:id, /about
// Layout component dengan navbar + Outlet
// Product detail page dari params
// NavLink dengan active styling
```

---

### Hari 13: Error Boundaries & Suspense

**Konsep:**
- Error Boundary: menangkap error di komponen child
- React 18+ — belum ada hook langsung, tapi bisa komponen class atau library
- `Suspense`: fallback untuk komponen yang belum siap
- `lazy()`: lazy loading komponen
- `use(Promise)` — React 19+

**Tugas:**
```tsx
// 1. Buat komponen ErrorBoundary (class component)
// 2. Bungkus komponen yang mungkin error
// 3. Route-based lazy loading: const Products = lazy(() => import('./Products'))
// 4. Suspense fallback: loading spinner
```

---

### Hari 14: Review & Refactor

Refactor semua project sebelumnya:
- Pisahkan logic ke custom hooks
- Tambah loading/error/empty states
- Pastikan TypeScript strict mode tidak error
- Refactor styling ke CSS Modules atau inline style yang rapi

---

## Minggu 7: React Final Project

### Hari 15-17: Final Project — Notes App Full CRUD

**Spesifikasi:**

Buat Notes App dengan fitur:

1. **Authentication** (simulasi — cukup login dengan nama, tanpa password)
   - Halaman login: input nama
   - Setelah login, nama tersimpan di localStorage
   - Tombol logout

2. **Notes List**
   - Grid notes card
   - Setiap card: judul, konten (preview), tanggal, kategori, warna
   - Search by title
   - Filter by category

3. **Create Note**
   - Form modal atau halaman terpisah
   - Fields: judul, konten (textarea), kategori, warna (color picker / pilihan)
   - Validasi: judul wajib

4. **Edit Note**
   - Klik card → edit mode
   - Pre-populated form

5. **Delete Note**
   - Konfirmasi sebelum hapus

6. **Persistensi**
   - localStorage (nanti di Next.js phase pake database)

**Routing:**
- `/` → Home (daftar notes)
- `/notes/new` → Create
- `/notes/:id` → Detail/Edit

**Teknis:**
- React + TypeScript + Vite
- react-router-dom
- Custom hooks (useLocalStorage, useNotes, etc.)
- useReducer untuk state notes
- Context untuk auth state
- Responsive CSS

---

### Hari 18-19: Self-Review & Bug Fixing

- Temukan dan fix minimal 5 bug di project Notes App
- Refactor kode yang berantakan
- Tambah error handling yang hilang
- Pastikan semua TypeScript strict

### Hari 20-21: Presentasi & Code Review

Kirim kode Notes App ke saya untuk di-review.

---

## Referensi

- [React.dev](https://react.dev/) — dokumentasi resmi (baca Learn section)
- [React TypeScript Cheatsheet](https://react-typescript-cheatsheet.netlify.app/)
- [reactrouter.com](https://reactrouter.com/)

## Checklist Penguasaan

Sebelum lanjut ke Next.js, pastikan bisa:
- [ ] Membuat komponen dengan props & children
- [ ] Mengelola state dengan useState & useReducer
- [ ] Side effects dengan useEffect
- [ ] Custom hooks (useLocalStorage, useFetch, useDebounce)
- [ ] Context API untuk global state
- [ ] React Router untuk multi-page
- [ ] Error handling dengan ErrorBoundary
- [ ] Membuat aplikasi CRUD dari 0
