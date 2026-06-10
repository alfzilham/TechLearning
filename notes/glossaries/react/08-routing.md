# Routing

## React Router v6

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `BrowserRouter` | Router untuk web (history API) | `<BrowserRouter><App/></BrowserRouter>` |
| `Routes` | Container untuk Route | `<Routes><Route .../></Routes>` |
| `Route` | Mapping URL ke komponen | `<Route path="/about" element={<About/>} />` |
| `path` | URL pattern | `/users/:id`, `/about`, `/blog/*` |
| `element` | Komponen yang dirender | `element={<Home/>}` |
| `index` | Route default di nested route | `<Route index element={<Home/>} />` |

```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Layout /> {/* Navbar, Footer, dll */}
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/users" element={<UserList />} />
        <Route path="/users/:id" element={<UserDetail />} />
        <Route path="/blog/*" element={<BlogRoutes />} />
        <Route path="*" element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## Navigation

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `Link` | Navigasi ke route (client-side) | `<Link to="/about">Tentang</Link>` |
| `NavLink` | Link dengan active class | `<NavLink to="/" className={({isActive}) => isActive ? 'active' : ''}>` |
| `useNavigate` | Navigasi programatis | `const nav = useNavigate(); nav('/home')` |
| `useHref` | Mendapatkan URL href | `const href = useHref('/about')` |

```jsx
import { Link, NavLink, useNavigate } from 'react-router-dom';

function Navbar() {
  return (
    <nav>
      <NavLink to="/" className={({ isActive }) => isActive ? 'active' : ''}>
        Home
      </NavLink>
      <NavLink to="/about">About</NavLink>
      <NavLink to="/users">Users</NavLink>
    </nav>
  );
}

function LoginPage() {
  const navigate = useNavigate();

  const handleLogin = async () => {
    await login();
    navigate('/dashboard', { replace: true }); // replace history
  };

  return (
    <div>
      <button onClick={handleLogin}>Login</button>
      <Link to="/register">Belum punya akun?</Link>
    </div>
  );
}
```

---

## Route Parameters

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `useParams` | Ambil parameter dari URL | `const { id } = useParams()` |
| Optional param | Parameter opsional | `path="/users/:id?` |
| Wildcard `*` | Match semua | `path="/blog/*` |
| Query params | String query di URL | `?page=1&search=react` |

```jsx
import { useParams, useSearchParams } from 'react-router-dom';

// Route: /users/:id
function UserDetail() {
  const { id } = useParams(); // ambil dari URL
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch(`/api/users/${id}`).then(res => res.json()).then(setUser);
  }, [id]);

  return <div>{user?.nama}</div>;
}

// Query params — /users?page=1&search=react
function UserList() {
  const [searchParams, setSearchParams] = useSearchParams();
  const page = searchParams.get('page') || '1';
  const search = searchParams.get('search') || '';

  const setPage = (newPage) => {
    setSearchParams({ page: newPage, search });
  };

  return (
    <div>
      <p>Halaman: {page}</p>
      <button onClick={() => setPage(Number(page) + 1)}>Next</button>
    </div>
  );
}
```

---

## Nested Routes & Layout

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `<Outlet />` | Render child route di layout | `<Layout><Outlet/></Layout>` |
| Layout routes | Parent route yang bungkus child | `element={<Layout/>}` dengan `<Outlet/>` |
| Index route | Default child di layout | `<Route index element={<Default/>}/>` |

```jsx
import { Outlet, Link } from 'react-router-dom';

// Layout component
function DashboardLayout() {
  return (
    <div>
      <aside>
        <Link to="profile">Profile</Link>
        <Link to="settings">Settings</Link>
      </aside>
      <main>
        <Outlet /> {/* Child route dirender di sini */}
      </main>
    </div>
  );
}

// Setup routes
<Routes>
  <Route path="/dashboard" element={<DashboardLayout />}>
    <Route index element={<DashboardHome />} />
    <Route path="profile" element={<Profile />} />
    <Route path="settings" element={<Settings />} />
  </Route>
</Routes>
```

---

## Protected Route

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Protected route | Hanya bisa diakses jika login | `element={<PrivateRoute><Dashboard/></PrivateRoute>}` |
| Redirect | Alihkan ke login jika tidak auth | `navigate('/login', { replace: true })` |

```jsx
function PrivateRoute({ children }) {
  const { user } = useAuth();
  const location = useLocation();

  if (!user) {
    // Redirect ke login, simpan halaman asal
    return <Navigate to="/login" state={{ from: location }} replace />;
  }

  return children;
}

// Setup
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="/login" element={<Login />} />
  <Route path="/dashboard" element={
    <PrivateRoute>
      <DashboardLayout />
    </PrivateRoute>
  }>
    <Route index element={<DashboardHome />} />
    <Route path="profile" element={<Profile />} />
  </Route>
</Routes>
```
