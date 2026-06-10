# Advanced Git

## Bisect

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git bisect start` | Mulai binary search untuk find commit yang introduce bug | `git bisect start` |
| `git bisect bad` | Tandai commit saat ini sebagai bad (ada bug) | `git bisect bad` |
| `git bisect good <commit>` | Tandai commit yang tidak ada bug | `git bisect good v1.0.0` |
| `git bisect reset` | Selesai bisect, kembali ke branch semula | `git bisect reset` |

```bash
# Cari commit yang introduce bug
git bisect start
git bisect bad              # commit sekarang ada bug
git bisect good v1.0.0      # v1.0.0 tidak ada bug
# Git akan checkout commit di tengah
# Test... jika masih ada bug:
git bisect bad
# Jika tidak ada bug:
git bisect good
# Ulangi sampai ketemu commit pertama yang bermasalah
# Output: abc123 is the first bad commit

git bisect reset  # selesai, balik ke branch semula

# Bisect otomatis — jalankan script
git bisect start HEAD v1.0.0
git bisect run npm test       # jalanin test setiap commit
git bisect reset
```

---

## Worktree

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git worktree add <path> <branch>` | Checkout branch di folder terpisah | `git worktree add ../feature-auth feature-auth` |
| `git worktree list` | Lihat semua worktree | `git worktree list` |
| `git worktree remove <path>` | Hapus worktree | `git worktree remove ../feature-auth` |

```bash
# Kerja di 2 branch tanpa stash/commit
git worktree add ../project-feature feature-auth
cd ../project-feature
# kerja di sini sementara branch main tetap clean

git worktree list
# /project   (main)
# /project-feature (feature-auth)

# Selesai, hapus
git worktree remove ../project-feature
```

---

## Submodule

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git submodule add <url>` | Tambah repo lain sebagai submodule | `git submodule add https://github.com/user/lib.git` |
| `git clone --recurse-submodules <url>` | Clone termasuk submodule | `git clone --recurse-submodules <url>` |
| `git submodule update --init --recursive` | Update submodule di repo yang sudah di-clone | `git submodule update --init --recursive` |

```bash
# Tambah library sebagai submodule
git submodule add https://github.com/user/shared-lib.git lib/
git commit -m "chore: add shared-lib as submodule"

# Clone dengan submodule
git clone --recurse-submodules https://github.com/user/repo.git

# Update submodule
git submodule update --init --recursive --remote
```

---

## Diff

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git diff` | Perubahan yang belum di-stage | `git diff` |
| `git diff --staged` | Perubahan yang sudah di-stage | `git diff --staged` |
| `git diff <branchA> <branchB>` | Bandingkan 2 branch | `git diff main feature-auth` |
| `git diff <commit> <commit>` | Bandingkan 2 commit | `git diff abc123 def456` |
| `git diff HEAD~2..HEAD` | Perubahan dalam 2 commit terakhir | `git diff HEAD~2..HEAD` |
| `git diff --stat` | Statistik perubahan (jumlah file & baris) | `git diff --stat` |
| `git diff --name-only` | Hanya nama file yang berubah | `git diff --name-only` |

```bash
# Melihat perubahan
git diff                    # working vs staging
git diff --staged           # staging vs commit
git diff HEAD               # working vs commit terakhir

# Branch diff
git diff main feature-auth  # semua perbedaan
git diff main..feature-auth # sama
git diff main...feature-auth # perubahan di feature saja (common ancestor)

# Commit diff
git diff abc123..def456
git diff HEAD~3 HEAD        # 3 commit terakhir
```

---

## Log Advanced

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `--oneline` | Ringkas satu baris per commit | `git log --oneline` |
| `--graph` | Tampilkan branch graph secara visual | `git log --oneline --graph --all` |
| `--author="nama"` | Filter by author | `git log --author="Rizky"` |
| `--since="2 weeks ago"` | Filter by waktu | `git log --since="2024-01-01"` |
| `--grep="keyword"` | Cari di pesan commit | `git log --grep="fix"` |
| `-S "function"` | Cari perubahan yang mengandung string tertentu | `git log -S "useState"` |
| `-p` | Tampilkan diff setiap commit | `git log -p -3` |
| `--format` | Kustom format output | `git log --format="%h %s"` |

```bash
# Visual graph
git log --oneline --graph --all --decorate

# Search
git log --author="Rizky" --since="2024-01-01" --until="2024-06-01"
git log --grep="feat:" --oneline
git log -S "console.log" --oneline  # cari string di kode

# Format kustom
git log --format="%h - %an: %s (%ar)" --graph
# %h = short hash, %an = author, %s = subject, %ar = relative date

# Statistics
git log --stat --oneline -5
git shortlog -sn                # kontribusi per author
```

---

## Blame

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git blame <file>` | Lihat siapa yang mengubah setiap baris file | `git blame index.js` |
| `git blame -L 10,20 <file>` | Lihat range baris tertentu | `git blame -L 10,20 index.js` |

```bash
git blame index.js
# abc123 (Rizky) 2024-01-15 1) const x = 10;
# def456 (Budi)  2024-02-01 2) const y = 20;
```

---

## Archive & Describe

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git archive` | Buat archive zip/tar dari commit/branch tertentu | `git archive --format=zip HEAD > project.zip` |
| `git describe` | Dapatkan nama tag terdekat + jumlah commit | `git describe --tags` → `v1.0.0-3-gabc123` |

```bash
# Archive
git archive --format=zip --output=project.zip main
git archive --format=tar HEAD | gzip > project.tar.gz

# Describe (berguna untuk versioning)
git describe --tags
# v1.0.0-3-gabc123
# Artinya: 3 commit setelah tag v1.0.0, hash abc123
```

---

## Checklist Advanced

| Situasi | Command |
|---------|---------|
| Cari commit yang introduce bug | `git bisect start` → `bad` → `good` |
| Checkout branch di folder terpisah | `git worktree add ../folder branch` |
| Tambah repo lain di project | `git submodule add <url>` |
| Cari perubahan string di history | `git log -S "string"` |
| Siapa yang nulis baris ini? | `git blame <file>` |
| Lihat graph semua branch | `git log --oneline --graph --all --decorate` |
| Statistik kontributor | `git shortlog -sn` |
| Buat archive source code | `git archive --format=zip HEAD > project.zip` |
| Dapatkan versi dari tag | `git describe --tags` |
| Cari commit dengan keyword | `git log --grep="keyword" --oneline` |
