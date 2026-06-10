# Remote & Sync

## Remote

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git remote add origin <url>` | Tambah remote repository | `git remote add origin https://github.com/user/repo.git` |
| `git remote -v` | Lihat daftar remote | `git remote -v` |
| `git remote remove <name>` | Hapus remote | `git remote remove origin` |
| `git remote rename <old> <new>` | Rename remote | `git remote rename origin upstream` |
| `git remote show <name>` | Detail info remote | `git remote show origin` |

```bash
# Tambah remote
git remote add origin https://github.com/user/repo.git

# Multiple remote
git remote add upstream https://github.com/original/repo.git

# Lihat
git remote -v
# origin   https://github.com/user/repo.git (fetch)
# origin   https://github.com/user/repo.git (push)
```

---

## Push

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git push` | Kirim commit ke remote | `git push` |
| `git push -u origin <branch>` | Set upstream + push pertama kali | `git push -u origin feature-auth` |
| `git push origin <branch>` | Push branch tertentu | `git push origin main` |
| `git push --all` | Push semua branch | `git push --all` |
| `git push --tags` | Push semua tag | `git push --tags` |
| `git push -f` | Force push (HATI-HATI!) | `git push -f origin main` |
| `git push -d origin <branch>` | Hapus branch di remote | `git push -d origin feature-login` |

```bash
# Push pertama kali — set upstream
git push -u origin main
# Selanjutnya cukup:
git push

# Push branch baru ke remote
git checkout -b feature-auth
git add . && git commit -m "feat: add auth"
git push -u origin feature-auth

# Hapus branch remote
git push -d origin feature-auth

# Force push (setelah rebase)
git push --force-with-lease origin main
# Lebih aman dari -f: cek jika ada commit orang lain
```

---

## Pull & Fetch

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git fetch` | Ambil update dari remote (tidak merge) | `git fetch` |
| `git fetch origin` | Fetch dari remote origin | `git fetch origin` |
| `git pull` | Fetch + merge dari remote | `git pull` |
| `git pull --rebase` | Fetch + rebase (history lebih bersih) | `git pull --rebase` |
| `git pull origin main` | Pull dari branch tertentu | `git pull origin main` |

```bash
# Fetch — lihat update tanpa merge
git fetch
git log --oneline origin/main   # lihat commit baru

# Pull — fetch + merge
git pull                        # = git fetch + git merge
git pull --rebase               # = git fetch + git rebase

# Compare local vs remote
git diff main origin/main       # lihat perbedaan
git log main..origin/main       # commit di remote yang tidak ada di local

# Rekomendasi: pull --rebase
git pull --rebase origin main
# History lebih bersih karena rebase, bukan merge commit
```

---

## Tracking Branches

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Upstream | Relasi antara local branch dan remote branch | Local `main` → `origin/main` |
| `git branch -u origin/branch` | Set upstream manual | `git branch -u origin/feature-auth` |
| `git branch -vv` | Lihat tracking semua branch | `git branch -vv` |

```bash
# Lihat tracking
git branch -vv
# main           abc123 [origin/main] feat: add navbar
# feature-auth   def456 [origin/feature-auth] feat: add login

# Setelah clone — otomatis main track origin/main

# Untuk branch lokal yang belum di-push
git push -u origin feature-auth
# Atau set manual:
git branch -u origin/feature-auth

# Hapus tracking
git branch --unset-upstream
```

---

## Sync Workflow

```bash
# 1. Dapatkan update terbaru
git checkout main
git pull --rebase origin main

# 2. Buat branch fitur
git checkout -b feature/login

# ... kerja, commit ...

# 3. Jaga branch tetap up-to-date dengan main
git fetch origin
git rebase main
# atau git merge main

# 4. Push
git push -u origin feature/login

# 5. Di GitHub: buat Pull Request

# 6. Setelah PR di-merge, update local
git checkout main
git pull --rebase origin main

# 7. Hapus branch lokal yang sudah di-merge
git branch -d feature/login
```
