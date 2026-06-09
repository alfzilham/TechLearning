# 11 tsconfig

## Compiler Options

| Opsi                  | Penjelasan                         | Contoh Nilai                           |
| --------------------- | ---------------------------------- | -------------------------------------- |
| `target`              | Versi ECMAScript output            | `"ES2020"`, `"ESNext"`                 |
| `module`              | Module system output               | `"commonjs"`, `"ESNext"`, `"NodeNext"` |
| `strict`              | Aktifkan semua strict checks       | `true`                                 |
| `outDir`              | Direktori output JS                | `"./dist"`                             |
| `rootDir`             | Direktori input TS                 | `"./src"`                              |
| `paths`               | Path aliases untuk import          | `{ "@/*": ["./src/*"] }`               |
| `include` / `exclude` | Pola file yang diproses            | `["src/**/*"]`, `["node_modules"]`     |
| `jsx`                 | Mode kompilasi JSX                 | `"react-jsx"`, `"preserve"`            |
| `resolveJsonModule`   | Izinkan import `.json`             | `true`                                 |
| `esModuleInterop`     | Interop seamless CJS/ESM           | `true`                                 |
| `baseUrl`             | Base directory untuk relative path | `"."`                                  |

## Compiler Strict Family

| Opsi Strict                    | Penjelasan                                           |
| ------------------------------ | ---------------------------------------------------- |
| `strict: true`                 | Mengaktifkan SEMUA di bawah ini                      |
| `noImplicitAny`                | Error jika tipe inferred jadi `any`                  |
| `strictNullChecks`             | `null`/`undefined` tidak bisa dipakai sembarangan    |
| `strictFunctionTypes`          | Strict variance pada function                        |
| `strictBindCallApply`          | Strict checking untuk `.bind()`/`.call()`/`.apply()` |
| `strictPropertyInitialization` | Properti class harus diinisialisasi                  |
| `noUnusedLocals`               | Error untuk variabel lokal tidak terpakai            |
| `noUnusedParameters`           | Error untuk parameter tidak terpakai                 |

```jsonc
{
  "compilerOptions": {
    // Target & Module
    "target": "ES2022",
    "module": "ESNext",
    "moduleResolution": "bundler",
    "lib": ["ES2022", "DOM", "DOM.Iterable"],

    // Output
    "outDir": "./dist",
    "rootDir": "./src",
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true,

    // Strict
    "strict": true,
    // setara dengan mengaktifkan semua di bawah:
    // "noImplicitAny": true,
    // "strictNullChecks": true,
    // "strictFunctionTypes": true,
    // "strictBindCallApply": true,
    // "strictPropertyInitialization": true,
    // "noImplicitThis": true,
    // "alwaysStrict": true

    // Module resolution
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"],
      "@components/*": ["./src/components/*"],
    },
    "esModuleInterop": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "verbatimModuleSyntax": true,

    // JSX
    "jsx": "react-jsx",
    "jsxImportSource": "react",

    // Additional
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
  },
  "include": ["src/**/*.ts", "src/**/*.tsx"],
  "exclude": ["node_modules", "dist", "**/*.test.ts"],
}
```
