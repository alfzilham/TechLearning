# Testing

## Setup

| Tools | Penjelasan | Contoh |
|-------|-----------|--------|
| Vitest / Jest | Test runner | `npm i -D vitest @testing-library/react` |
| React Testing Library | Render & query komponen | `import { render, screen } from '@testing-library/react'` |
| jest-dom | Custom matchers | `import '@testing-library/jest-dom'` |
| user-event | Simulasi interaksi user | `import userEvent from '@testing-library/user-event'` |

```jsx
// setup — tambahkan di setup file atau global
import '@testing-library/jest-dom';
```

---

## Render & Query

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `render(<Comp />)` | Render komponen untuk test | `render(<Button label="Klik" />)` |
| `screen.getByText()` | Cari elemen berdasarkan teks | `screen.getByText('Klik')` |
| `screen.getByRole()` | Cari berdasarkan ARIA role (prioritas!) | `screen.getByRole('button')` |
| `screen.getByLabelText()` | Cari form input via label | `screen.getByLabelText('Email')` |
| `screen.getByTestId()` | Cari via `data-testid` | `screen.getByTestId('submit-btn')` |
| `screen.queryBy*` | Return null jika tidak ada (untuk assert "tidak ada") | `expect(screen.queryByText('Error')).toBeNull()` |
| `screen.findBy*` | Async — tunggu elemen muncul | `await screen.findByText('Loaded')` |

```jsx
import { render, screen } from '@testing-library/react';

function Button({ label, variant }) {
  return (
    <button className={`btn btn-${variant}`} data-testid="submit-btn">
      {label}
    </button>
  );
}

test('render button with label', () => {
  render(<Button label="Simpan" variant="primary" />);

  // Query priority: ByRole > ByLabelText > ByPlaceholderText > ByText > ByTestId
  expect(screen.getByRole('button')).toHaveTextContent('Simpan');
  expect(screen.getByText('Simpan')).toBeInTheDocument();
  expect(screen.getByTestId('submit-btn')).toBeInTheDocument();
});

test('button disabled', () => {
  render(<Button label="Simpan" disabled />);
  expect(screen.getByRole('button')).toBeDisabled();
});
```

---

## Events & User Interaction

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `userEvent.click(el)` | Klik elemen | `await user.click(screen.getByRole('button'))` |
| `userEvent.type(el, text)` | Ketik teks | `await user.type(screen.getByRole('textbox'), 'Halo')` |
| `userEvent.clear(el)` | Kosongkan input | `await user.clear(input)` |
| `userEvent.selectOptions(el, ['opt'])` | Pilih option | `await user.selectOptions(select, 'opt1')` |

```jsx
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';

function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(c => c + 1)}>Tambah</button>
    </div>
  );
}

test('counter increments on click', async () => {
  const user = userEvent.setup();
  render(<Counter />);

  const button = screen.getByRole('button', { name: 'Tambah' });
  await user.click(button);
  await user.click(button);

  expect(screen.getByText('Count: 2')).toBeInTheDocument();
});

test('form input', async () => {
  const user = userEvent.setup();
  const handleSubmit = jest.fn();
  render(<Form onSubmit={handleSubmit} />);

  await user.type(screen.getByLabelText('Email'), 'user@test.com');
  await user.click(screen.getByRole('button', { name: 'Kirim' }));

  expect(handleSubmit).toHaveBeenCalledWith({ email: 'user@test.com' });
});
```

---

## Async Testing

```jsx
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  useEffect(() => {
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(setUser);
  }, [userId]);

  if (!user) return <p>Loading...</p>;
  return <h1>{user.nama}</h1>;
}

test('loads user data', async () => {
  render(<UserProfile userId={1} />);

  // Loading state
  expect(screen.getByText('Loading...')).toBeInTheDocument();

  // Tunggu data muncul
  const name = await screen.findByText('John Doe');
  expect(name).toBeInTheDocument();
});

test('waitFor example', async () => {
  render(<AsyncComponent />);

  await waitFor(() => {
    expect(screen.getByText('Data loaded')).toBeInTheDocument();
  });
});
```

---

## Mocking API

```jsx
// Mock fetch
global.fetch = vi.fn();

test('fetch user data', async () => {
  fetch.mockResolvedValueOnce({
    ok: true,
    json: async () => ({ id: 1, nama: 'John' }),
  });

  render(<UserProfile userId={1} />);

  expect(await screen.findByText('John')).toBeInTheDocument();
  expect(fetch).toHaveBeenCalledWith('/api/users/1');
});
```
