# Events & Forms

## Event Handling

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `onClick` | Klik elemen | `<button onClick={handleClick}>` |
| `onChange` | Nilai input berubah | `<input onChange={e => setVal(e.target.value)}>` |
| `onSubmit` | Form di-submit | `<form onSubmit={handleSubmit}>` |
| `onKeyDown` | Tombol keyboard ditekan | `<input onKeyDown={e => e.key === 'Enter' && fn()}` |
| SyntheticEvent | React wrapper untuk native event | `e.preventDefault()`, `e.stopPropagation()` |
| Event pooling | Di React 17+ sudah dihapus (async aman) | `e.persist()` — tidak perlu lagi |

```jsx
function EventDemo() {
  const handleClick = (e) => {
    console.log('Clicked!', e.target, e.type);
  };

  const handleKeyDown = (e) => {
    if (e.key === 'Enter') console.log('Enter pressed');
    if (e.ctrlKey && e.key === 's') {
      e.preventDefault(); // cegah save browser
      save(); // custom save
    }
  };

  return (
    <div>
      <button onClick={handleClick}>Klik</button>
      <input onKeyDown={handleKeyDown} placeholder="Tekan Enter" />
      <div onClick={(e) => e.stopPropagation()}>
        {/* Mencegah event bubbling ke parent */}
      </div>
    </div>
  );
}
```

---

## Controlled Components

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Controlled | Nilai input dikontrol oleh state React | `value + onChange` |
| Text input | Input teks biasa | `<input value={val} onChange={e => setVal(e.target.value)} />` |
| Textarea | Area teks | `<textarea value={val} onChange={fn} />` |
| Select | Dropdown | `<select value={val} onChange={fn}><option/></select>` |
| Checkbox | Checkbox boolean | `<input type="checkbox" checked={val} onChange={fn} />` |
| Radio | Pilihan tunggal | `<input type="radio" checked={val === 'opt'} />` |

```jsx
import { useState } from 'react';

function RegistrationForm() {
  const [form, setForm] = useState({
    nama: '',
    email: '',
    role: 'user',
    agree: false,
    gender: '',
  });

  const updateField = (e) => {
    const { name, value, type, checked } = e.target;
    setForm(prev => ({
      ...prev,
      [name]: type === 'checkbox' ? checked : value,
    }));
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log('Form data:', form);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="nama" value={form.nama} onChange={updateField} placeholder="Nama" />
      <input name="email" type="email" value={form.email} onChange={updateField} placeholder="Email" />

      <select name="role" value={form.role} onChange={updateField}>
        <option value="user">User</option>
        <option value="admin">Admin</option>
      </select>

      <label>
        <input name="agree" type="checkbox" checked={form.agree} onChange={updateField} />
        Setuju syarat & ketentuan
      </label>

      <label><input name="gender" type="radio" value="pria" checked={form.gender === 'pria'} onChange={updateField} /> Pria</label>
      <label><input name="gender" type="radio" value="wanita" checked={form.gender === 'wanita'} onChange={updateField} /> Wanita</label>

      <button type="submit" disabled={!form.agree}>Daftar</button>
    </form>
  );
}
```

---

## Uncontrolled Components

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Uncontrolled | Nilai diakses via ref, bukan state | `const ref = useRef(null)` |
| defaultValue | Nilai awal (bukan value) | `<input defaultValue="teks" />` |
| useRef | Akses nilai saat dibutuhkan | `ref.current.value` |

```jsx
import { useRef } from 'react';

function UncontrolledForm() {
  const namaRef = useRef(null);
  const emailRef = useRef(null);

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log({
      nama: namaRef.current.value,
      email: emailRef.current.value,
    });
  };

  return (
    <form onSubmit={handleSubmit}>
      <input ref={namaRef} defaultValue="Rizky" />
      <input ref={emailRef} type="email" />
      <button type="submit">Kirim</button>
    </form>
  );
}
```

---

## Form Validation

```jsx
function ValidatedForm() {
  const [values, setValues] = useState({ email: '', password: '' });
  const [errors, setErrors] = useState({});

  const validate = () => {
    const err = {};
    if (!values.email.includes('@')) err.email = 'Email tidak valid';
    if (values.password.length < 6) err.password = 'Min 6 karakter';
    return err;
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const err = validate();
    if (Object.keys(err).length > 0) {
      setErrors(err);
      return;
    }
    console.log('Submit', values);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input value={values.email} onChange={e => setValues({...values, email: e.target.value})} />
      {errors.email && <span className="error">{errors.email}</span>}
      <input type="password" value={values.password} onChange={e => setValues({...values, password: e.target.value})} />
      {errors.password && <span className="error">{errors.password}</span>}
      <button type="submit">Login</button>
    </form>
  );
}
```
