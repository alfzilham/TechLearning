# Undo & Reset

## Working Directory & Staging

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git restore <file>` | Discard perubahan file yang belum di-stage | `git restore index.html` |
| `git restore --staged <file>` | Unstage file (kembali ke modified) | `git restore --staged index.html` |
| `git checkout -- <file>` | Cara lama discard perubahan (sama seperti restore) | `git checkout -- index.html` |
| `git clean -fd` | Hapus file untracked (f = file, d = directory) | `git clean -fd` |
| `git clean -n` | Dry run — lihat apa yang akan dihapus | `git clean -n` |

```bash
# Hapus perubahan file yang belum di-stage
git restore index.html          # modern (Git 2.23+)
git checkout -- index.html      # legacy

# Unstage file (balik ke modified)
git add index.html              # staging
git restore --staged index.html # unstage — file tetap modified

# Hapus semua untracked files/folders
git clean -fd
git clean -n                    # dry run (cek dulu)
```

---

## Commit

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git commit --amend` | Ubah pesan commit terakhir | `git commit --amend -m "pesan baru"` |
| `git commit --amend --no-edit` | Tambah perubahan ke commit terakhir tanpa ubah pesan | `git add . && git commit --amend --no-edit` |
| `git revert <commit>` | Buat commit baru yang membalikkan perubahan | `git revert abc123` |
| `git revert HEAD` | Revert commit terakhir | `git revert HEAD` |
| `git revert HEAD~3..HEAD` | Revert range commit | `git revert HEAD~3..HEAD --no-edit` |

```bash
# Ganti pesan commit terakhir
git commit -m "feat: add login"
git commit --amend -m "feat: add login with validation"

# Tambah perubahan ke commit terakhir (lupa add 1 file)
git add forgotten-file.js
git commit --amend --no-edit

# Revert (buat commit baru yang kebalikan)
git revert HEAD                     # revert 1 commit terakhir
git revert abc123                   # revert commit spesifik
git revert HEAD~3..HEAD             # revert 3 commit terakhir

# Revert vs Reset:
# revert = aman untuk remote (buat commit baru)
# reset = berbahaya untuk remote (hapus history)
```

---

## Reset

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git reset --soft HEAD~1` | Hapus commit, perubahan tetap di stage | `git reset --soft HEAD~1` |
| `git reset --mixed HEAD~1` | Hapus commit, perubahan tetap di working (default) | `git reset HEAD~1` |
| `git reset --hard HEAD~1` | Hapus commit + perubahan (permanen!) | `git reset --hard HEAD~1` |
| `git reset <file>` | Unstage file (sama seperti restore --staged) | `git reset index.html` |

```bash
# Level reset (dari paling berbahaya ke paling aman):

# --soft: commit hilang, perubahan tetap di stage
git reset --soft HEAD~1     # kembali 1 commit, file siap di-commit ulang

# --mixed (default): commit hilang, perubahan di working directory
git reset HEAD~1            # kembali 1 commit, file modified
git reset HEAD~3            # kembali 3 commit

# --hard: commit hilang + perubahan hilang (TIDAK BISA DIKEMBALIKAN!)
git reset --hard HEAD~1     # HATI-HATI! Perubahan permanent hilang

# Unstage file
git reset index.html        # sama dengan git restore --staged index.html
```

---

## Reflog (Safety Net)

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git reflog` | Catatan semua pergerakan HEAD | `git reflog` |
| `git reset --hard HEAD@{n}` | Kembali ke state tertentu via reflog | `git reset --hard HEAD@{2}` |

```bash
# Reflog — penyelamat!
git reflog
# abc123 HEAD@{0}: reset: moving to HEAD~1
# def456 HEAD@{1}: commit: feat: add login
# ghi789 HEAD@{2}: commit: fix: button

# Oops, salah reset --hard!
git reset --hard HEAD@{1}   # kembali ke sebelum reset
# Semua perubahan kembali! ✅

# Reflog hanya menyimpan 30-90 hari (gc)
```

---

## Restore Specific File

```bash
# Kembalikan file ke versi commit tertentu
git restore --source abc123 index.html

# Kembalikan file ke versi 2 commit sebelumnya
git restore --source HEAD~2 index.html

# Atau cara lama
git checkout abc123 -- index.html
```

---

## Cheatsheet Undo

| Situasi | Command |
|---------|---------|
| Ubah file, belum di-stage, mau balik | `git restore <file>` |
| Udah di-stage, mau unstage | `git restore --staged <file>` |
| Udah di-commit, mau ganti pesan | `git commit --amend` |
| Udah di-commit, mau hapus commit (lokal) | `git reset --soft HEAD~1` |
| Udah di-commit, mau hapus + perubahan (lokal) | `git reset --hard HEAD~1` |
| Udah di-push, mau balik | `git revert <commit>` |
| Reset --hard kebanyakan | `git reflog` → `git reset --hard HEAD@{n}` |
