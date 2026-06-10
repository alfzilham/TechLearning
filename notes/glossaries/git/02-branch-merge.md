# Branch & Merge

## Branch

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git branch` | Lihat daftar branch (tanda `*` = branch aktif) | `git branch` |
| `git branch <name>` | Buat branch baru (tetap di branch saat ini) | `git branch feature-auth` |
| `git checkout -b <name>` | Buat branch baru + pindah ke branch itu | `git checkout -b feature-auth` |
| `git switch -c <name>` | Alternatif checkout -b (Git 2.23+) | `git switch -c feature-auth` |
| `git switch <name>` | Pindah branch (Git 2.23+) | `git switch main` |
| `git checkout <name>` | Pindah branch | `git checkout main` |
| `git branch -d <name>` | Hapus branch (jika sudah di-merge) | `git branch -d feature-auth` |
| `git branch -D <name>` | Hapus branch paksa (meski belum di-merge) | `git branch -D feature-auth` |
| `git branch -m <old> <new>` | Rename branch | `git branch -m master main` |
| `git branch -r` | Lihat remote branch | `git branch -r` |
| `git branch -a` | Lihat semua branch (lokal + remote) | `git branch -a` |

```bash
# Branch naming convention
git checkout -b feature/login         # fitur baru
git checkout -b fix/login-error       # bugfix
git checkout -b chore/update-deps     # maintenance
git checkout -b refactor/components   # refactor

# Pindah branch
git checkout main
git switch main

# Hapus branch
git branch -d feature-login  # aman (sudah di-merge)
git branch -D feature-login  # paksa (belum di-merge)

# Rename branch
git branch -m old-name new-name
```

---

## Merge

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git merge <branch>` | Gabung branch lain ke branch aktif | `git checkout main; git merge feature-auth` |
| `--no-ff` | Paksa merge commit (no fast-forward) | `git merge --no-ff feature-auth` |
| `--squash` | Gabung semua commit jadi satu | `git merge --squash feature-auth` |
| Fast-forward | Merge tanpa commit baru (jika linear) | Default jika cabang lurus |
| 3-way merge | Merge dengan commit baru (jika divergen) | Otomatis saat branch berbeda |

```bash
# Merge feature ke main
git checkout main
git merge feature-auth

# Fast-forward merge — linear, tanpa commit baru
# main → A → B → C (feature)
# Hasil: main = A → B → C

# 3-way merge — divergen, ada commit merge
# main → A → B → D (merge commit)
# feature → C
# Hasil: main = A → B → C → D

# Merge dengan --no-ff (pasti ada merge commit)
git merge --no-ff feature-auth

# Squash merge (satu commit)
git merge --squash feature-auth
git commit -m "feat: add auth system"
```

---

## Merge Conflict

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Conflict | Terjadi saat 2 branch mengubah baris yang sama | Git akan memberitahu file mana conflict |
| `<<<<<<< HEAD` | Kode di branch aktif (current) | Ada di file conflict |
| `=======` | Pemisah antara dua versi | — |
| `>>>>>>> branch` | Kode dari branch yang di-merge | — |
| Resolve | Manual edit file + hapus marker | Edit → add → commit |

```bash
# Saat conflict, git akan bilang:
# CONFLICT (content): Merge conflict in index.html

# Buka file, akan terlihat:
<<<<<<< HEAD
<h1>Home Page</h1>
=======
<h1>Home</h1>
>>>>>>> feature-navbar

# Edit — pilih salah satu atau gabung:
<h1>Home Page</h1>

# Setelah edit, stage dan commit
git add index.html
git commit -m "merge: resolve conflict navbar"

# Atau abort merge jika bingung
git merge --abort
```

---

## Rebase

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git rebase <branch>` | Pindah base branch | `git rebase main` |
| `git rebase -i HEAD~n` | Interactive rebase n commit terakhir | Squash, reword, drop, edit |
| `git rebase --continue` | Lanjutkan rebase setelah conflict | Setelah resolve conflict |
| `git rebase --abort` | Batalkan rebase | Kembali ke sebelum rebase |

```bash
# Rebase feature ke main
git checkout feature-auth
git rebase main
# History jadi linear: main → A → B, feature → A → B → C

# Interactive rebase (squash, edit commit)
git rebase -i HEAD~3
# Picker:
# pick — pakai commit
# squash — gabung dengan commit sebelumnya
# reword — ganti pesan commit
# drop — hapus commit
# edit — edit isi commit

# Jika conflict saat rebase
git status           # lihat file conflict
# resolve conflict...
git add <file>
git rebase --continue

# Batalkan
git rebase --abort
```

---

## Stash

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git stash` | Simpan sementara perubahan (belum di-commit) | `git stash` |
| `git stash pop` | Kembalikan stash terakhir + hapus dari stash list | `git stash pop` |
| `git stash save "pesan"` | Stash dengan pesan | `git stash save "WIP: form login"` |
| `git stash list` | Lihat daftar stash | `git stash list` |
| `git stash apply stash@{n}` | Kembalikan stash tertentu (tidak hapus) | `git stash apply stash@{2}` |
| `git stash drop stash@{n}` | Hapus stash tertentu | `git stash drop stash@{0}` |
| `git stash clear` | Hapus semua stash | `git stash clear` |
| `git stash branch <name>` | Buat branch baru dari stash | `git stash branch fix-bug` |

```bash
# Sedang kerja di feature tapi harus pindah branch
git stash save "WIP: login form validation"
git checkout main
# fix something...
git checkout feature-auth
git stash pop  # kembalikan work in progress

# Lihat stash
git stash list
# stash@{0}: On feature-auth: login form validation
# stash@{1}: On main: temp changes
```
