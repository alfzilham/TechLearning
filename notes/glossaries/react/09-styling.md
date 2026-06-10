# Styling

## CSS Modules

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| CSS Modules | CSS file yang di-scope ke komponen | `import styles from './Comp.module.css'` |
| Auto-scoping | Class name unik otomatis | `.card` jadi `.Comp_card_1a2b3` |
| Multiple classes | Gabung class | `\`${styles.card} ${styles.active}\`` |

```css
/* Card.module.css */
.card {
  padding: 16px;
  border-radius: 8px;
  background: white;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.title {
  font-size: 18px;
  font-weight: 600;
  color: #333;
}

.active {
  border: 2px solid blue;
}
```

```jsx
import styles from './Card.module.css';

function Card({ title, children, active }) {
  return (
    <div className={`${styles.card} ${active ? styles.active : ''}`}>
      <h3 className={styles.title}>{title}</h3>
      {children}
    </div>
  );
}
```

---

## Styled Components

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `styled.element` | Buat komponen styled | `const Btn = styled.button` |
| Template literal | CSS di template literal | `styled.button\` color: red; \`` |
| Props | Akses props via `${}` | `\`color: ${p => p.color}\`` |
| Extending | Perluas styled component | `styled(Btn)\` font-size: 20px \`` |

```jsx
import styled from 'styled-components';

// Basic
const Button = styled.button`
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;

  &:hover {
    opacity: 0.8;
  }
`;

// With props
const Badge = styled.span`
  background: ${props => props.variant === 'success' ? '#2ecc71' : '#e74c3c'};
  color: white;
  padding: 4px 8px;
  border-radius: 999px;
  font-size: 12px;
`;

// Extending
const DangerButton = styled(Button)`
  background: #e74c3c;
  color: white;
`;

// Dynamic props
const Card = styled.div`
  padding: ${p => p.$padding || '16px'};
  background: ${p => p.$dark ? '#333' : '#fff'};
  color: ${p => p.$dark ? '#fff' : '#333'};
`;

function App() {
  return (
    <div>
      <Button>Click me</Button>
      <Badge variant="success">Active</Badge>
      <DangerButton>Delete</DangerButton>
      <Card $dark>Dark card</Card>
    </div>
  );
}
```

---

## Tailwind CSS Integration

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| ClassName | Utility classes langsung | `className="flex gap-4 p-4"` |
| Conditional | Gabung class dinamis | `clsx('btn', isActive && 'active')` |
| Template literal | Dynamic Tailwind classes | ``text-${size}`` (hati-hati purge) |

```jsx
import clsx from 'clsx'; // atau classnames

function Card({ title, variant = 'default', isActive }) {
  return (
    <div className={clsx(
      'rounded-lg p-4 shadow transition',
      variant === 'primary' && 'bg-blue-500 text-white',
      variant === 'default' && 'bg-white text-gray-800',
      isActive && 'ring-2 ring-blue-400'
    )}>
      <h3 className="text-lg font-semibold mb-2">{title}</h3>
    </div>
  );
}

// clsx utility — alternatif ringan
function Button({ variant, size, disabled, children }) {
  const base = 'rounded font-medium transition focus:outline-none';
  const variants = {
    primary: 'bg-blue-600 text-white hover:bg-blue-700',
    secondary: 'bg-gray-200 text-gray-800 hover:bg-gray-300',
    danger: 'bg-red-500 text-white hover:bg-red-600',
  };
  const sizes = {
    sm: 'px-3 py-1 text-sm',
    md: 'px-4 py-2 text-base',
    lg: 'px-6 py-3 text-lg',
  };

  return (
    <button
      className={clsx(base, variants[variant], sizes[size], disabled && 'opacity-50 cursor-not-allowed')}
      disabled={disabled}
    >
      {children}
    </button>
  );
}
```

---

## CSS-in-JS (Emotion)

```jsx
/** @jsxImportSource @emotion/react */
import { css } from '@emotion/react';

const cardStyle = css`
  padding: 16px;
  border-radius: 8px;
  background: white;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
`;

const titleStyle = (color) => css`
  font-size: 18px;
  font-weight: 600;
  color: ${color};
`;

function Card({ title, color = '#333' }) {
  return (
    <div css={cardStyle}>
      <h3 css={titleStyle(color)}>{title}</h3>
    </div>
  );
}
```

---

## Inline Styles

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Style object | CSS dalam object JS | `style={{ color: 'red', fontSize: 16 }}` |
| camelCase | Semua properti CSS camelCase | `backgroundColor`, `fontSize`, `borderRadius` |
| Dynamic | Style berdasarkan state/props | `style={{ color: isError ? 'red' : 'green' }}` |

```jsx
function Alert({ type, message }) {
  const styles = {
    padding: '12px 16px',
    borderRadius: '4px',
    color: 'white',
    backgroundColor: type === 'error' ? '#e74c3c' :
                     type === 'success' ? '#2ecc71' : '#3498db',
  };

  return <div style={styles}>{message}</div>;
}
```
