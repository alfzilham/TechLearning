# 12 - Error Handling

## Try...Catch...Finally

| Statement     | Penjelasan                             | Contoh                                    |
| ------------- | -------------------------------------- | ----------------------------------------- |
| `try...catch` | Tangkap error agar program tidak crash | `try { JSON.parse("{bad}") } catch(e) {}` |
| `finally`     | Selalu dijalankan, error atau tidak    | `finally { console.log("selalu jalan") }` |

Contoh:

```js
try {
  let data = JSON.parse("{ invalid json }");
} catch (error) {
  console.log("Error parsing JSON:", error.message);
} finally {
  console.log("Blok ini selalu jalan");
}
```

## Throw

| Keyword | Penjelasan          | Contoh                           |
| ------- | ------------------- | -------------------------------- |
| `throw` | Lempar error manual | `throw new Error("Pesan error")` |

## Jenis Error

| Error            | Penjelasan              | Contoh penyebab                          |
| ---------------- | ----------------------- | ---------------------------------------- |
| `Error`          | Error umum              | `new Error("Pesan")`                     |
| `SyntaxError`    | Syntax/kode tidak valid | `eval("alert('Halo)");`                  |
| `ReferenceError` | Variable tidak ada      | `console.log(x)` (x tidak didefinisikan) |
| `TypeError`      | Operasi pada tipe salah | `null.something()`                       |
| `RangeError`     | Nilai di luar range     | `new Array(-1)`                          |
| `URIError`       | Error fungsi URI        | `decodeURI("%%%")`                       |

## Custom Error

Buat class error sendiri dengan `extends Error`:

```js
class ValidationError extends Error {
  constructor(field, message) {
    super(message);
    this.name = "ValidationError";
    this.field = field;
  }
}

try {
  throw new ValidationError("email", "Format email tidak valid");
} catch (error) {
  if (error instanceof ValidationError) {
    console.log(`${error.field}: ${error.message}`);
  }
}
```

## Error Properties

| Properti  | Penjelasan                                          |
| --------- | --------------------------------------------------- |
| `message` | Pesan error                                         |
| `name`    | Tipe error (`"TypeError"`, `"ReferenceError"`, dll) |
| `stack`   | Stack trace (lokasi error)                          |

## Try...Catch dengan Async

| Cara               | Contoh                                 |
| ------------------ | -------------------------------------- |
| `async/await`      | `try { await fetch(url) } catch(e) {}` |
| Promise `.catch()` | `fetch(url).then(fn).catch(fn)`        |

## Global Error Handler

| Environment | Cara                                                |
| ----------- | --------------------------------------------------- |
| Browser     | `window.onerror = (msg, src, line, col, err) => {}` |
| Browser     | `window.addEventListener("error", fn)`              |
| Node.js     | `process.on("uncaughtException", fn)`               |
