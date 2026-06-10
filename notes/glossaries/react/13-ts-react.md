# TypeScript dengan React

## Component Typing

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `React.FC<Props>` | Function component type (umum) | `const Comp: React.FC<Props> = ({ name }) => ...` |
| Props interface | Definisikan props | `interface Props { name: string }` |
| `React.ReactNode` | Tipe untuk children | `children: React.ReactNode` |
| `React.ReactElement` | JSX element | `React.ReactElement` |

```tsx
// Cara 1: inline type
function Card({ title, children }: { title: string; children: React.ReactNode }) {
  return (
    <div className="card">
      <h3>{title}</h3>
      {children}
    </div>
  );
}

// Cara 2: interface terpisah (recommended)
interface ButtonProps {
  label: string;
  variant?: 'primary' | 'secondary' | 'danger';
  size?: 'sm' | 'md' | 'lg';
  disabled?: boolean;
  onClick?: () => void;
  children?: React.ReactNode;
}

function Button({ label, variant = 'primary', disabled, onClick }: ButtonProps) {
  return (
    <button
      className={`btn btn-${variant}`}
      disabled={disabled}
      onClick={onClick}
    >
      {label}
    </button>
  );
}

// Cara 3: React.FC (lebih eksplisit)
const Badge: React.FC<{ text: string; color?: string }> = ({ text, color }) => {
  return <span style={{ color }}>{text}</span>;
};
```

---

## useState dengan TypeScript

| Pattern | Penjelasan | Contoh |
|---------|-----------|--------|
| `useState<Type>` | State dengan tipe | `useState<string>('')` |
| Union type | State bisa beberapa tipe | `useState<User \| null>(null)` |
| Type inference | TS otomatis infer dari initial value | `useState(0)` → `number` |

```tsx
interface User {
  id: number;
  nama: string;
  email: string;
}

function UserProfile() {
  // Simple state — type inference dari initial value
  const [count, setCount] = useState(0);

  // Object state dengan interface
  const [user, setUser] = useState<User | null>(null);

  // Array state
  const [users, setUsers] = useState<User[]>([]);

  // Union type
  const [status, setStatus] = useState<'loading' | 'success' | 'error'>('loading');

  // Complex state dengan interface
  const [form, setForm] = useState<{ email: string; password: string }>({
    email: '',
    password: '',
  });

  return (
    <div>
      <p>{status}</p>
      <p>{user?.nama}</p>
    </div>
  );
}
```

---

## Event Types

| Event | Tipe | Contoh |
|-------|------|--------|
| Click | `React.MouseEvent<HTMLButtonElement>` | `(e: React.MouseEvent<HTMLButtonElement>) => void` |
| Change (input) | `React.ChangeEvent<HTMLInputElement>` | `e.target.value` |
| Form submit | `React.FormEvent<HTMLFormElement>` | `e.preventDefault()` |
| Keyboard | `React.KeyboardEvent<HTMLInputElement>` | `e.key` |
| Focus | `React.FocusEvent<HTMLInputElement>` | `e.target.value` |

```tsx
function Form() {
  const [email, setEmail] = useState('');

  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    setEmail(e.target.value);
  };

  const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    console.log('submit', email);
  };

  const handleKeyDown = (e: React.KeyboardEvent<HTMLInputElement>) => {
    if (e.key === 'Enter') console.log('enter');
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="email"
        value={email}
        onChange={handleChange}
        onKeyDown={handleKeyDown}
      />
      <button type="submit">Kirim</button>
    </form>
  );
}
```

---

## useRef dengan TypeScript

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| DOM ref | `useRef<HTMLDivElement>(null)` | `const ref = useRef<HTMLDivElement>(null)` |
| Mutable ref | `useRef<number>(0)` | Untuk counter/value tanpa re-render |
| `null!` assertion | Yakin ref tidak null saat digunakan | `ref.current!.focus()` |

```tsx
function VideoPlayer() {
  // DOM element ref
  const videoRef = useRef<HTMLVideoElement>(null);
  const inputRef = useRef<HTMLInputElement>(null);

  // Mutable value (tidak trigger re-render)
  const clickCount = useRef<number>(0);

  const play = () => {
    videoRef.current?.play(); // optional chaining
  };

  const focusInput = () => {
    inputRef.current?.focus();
  };

  return (
    <div>
      <video ref={videoRef} src="video.mp4" />
      <input ref={inputRef} />
      <button onClick={play}>Play</button>
    </div>
  );
}
```

---

## Generic Components

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `<T>` | Type parameter untuk komponen | `interface Props<T> { items: T[]; render: (item: T) => React.ReactNode }` |

```tsx
interface ListProps<T> {
  items: T[];
  renderItem: (item: T) => React.ReactNode;
  onSelect?: (item: T) => void;
}

function List<T>({ items, renderItem, onSelect }: ListProps<T>) {
  return (
    <ul>
      {items.map((item, i) => (
        <li key={i} onClick={() => onSelect?.(item)}>
          {renderItem(item)}
        </li>
      ))}
    </ul>
  );
}

// Penggunaan — TS auto infer type
interface Product { id: number; nama: string; harga: number; }

function ProductList({ products }: { products: Product[] }) {
  return (
    <List
      items={products}
      renderItem={(product) => <span>{product.nama} — Rp{product.harga}</span>}
      onSelect={(product) => console.log(product.id)}
    />
  );
}
```

---

## Utility Patterns

```tsx
// ComponentProps — ambil tipe props dari komponen
import { ComponentProps } from 'react';

type ButtonProps = ComponentProps<typeof Button>;

// Omit & Pick untuk memodifikasi props
interface BaseInputProps {
  label: string;
  error?: string;
  name: string;
}

type CustomInputProps = BaseInputProps & Omit<ComponentProps<'input'>, 'name'>;

// React.HTMLAttributes untuk HTML elements
interface CardProps extends React.HTMLAttributes<HTMLDivElement> {
  variant?: 'outlined' | 'elevated';
}

// ForwardRef dengan generic
const FancyInput = forwardRef<HTMLInputElement, { label: string }>(
  ({ label }, ref) => (
    <div>
      <label>{label}</label>
      <input ref={ref} />
    </div>
  )
);
```

