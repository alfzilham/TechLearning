# Dasar & Instalasi

## Setup Git

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git --version` | Cek versi Git | `git --version` |
| `git config --global user.name` | Set nama user global | `git config --global user.name "Rizky"` |
| `git config --global user.email` | Set email user global | `git config --global user.email "rizky@email.com"` |
| `git config --global init.defaultBranch` | Ganti default branch dari master ke main | `git config --global init.defaultBranch main` |
| `git config --list` | Lihat semua konfigurasi | `git config --list` |
| `git config --global alias` | Buat shortcut command | `git config --global alias.co checkout` |

```bash
# Setup awal
git config --global user.name "Rizky"
git config --global user.email "rizky@email.com"
git config --global init.defaultBranch main

# Alias yang berguna
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --all"
```

---

## Init Repository

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git init` | Buat repository Git baru di folder lokal | `git init` |
| `git clone <url>` | Clone repository dari remote | `git clone https://github.com/user/repo.git` |
| `git clone <url> <folder>` | Clone dengan nama folder berbeda | `git clone https://github.com/user/repo.git my-folder` |

```bash
# Init repo baru
mkdir project-ku
cd project-ku
git init
# Output: Initialized empty Git repository in ...

# Clone repo existing
git clone https://github.com/user/repo.git
git clone https://github.com/user/repo.git project-folder
```

---

## Tracking & Commit

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git status` | Cek status file (modified, staged, untracked) | `git status` |
| `git add <file>` | Stage file tertentu ke staging area | `git add index.html` |
| `git add .` | Stage semua perubahan | `git add .` |
| `git add -p` | Stage file per bagian (interaktif) | `git add -p` |
| `git commit -m "pesan"` | Commit perubahan yang sudah di-stage | `git commit -m "feat: add navbar"` |
| `git commit -am "pesan"` | Add + commit untuk file yang sudah di-track (gabungan add + commit) | `git commit -am "fix: update button"` |
| `git log` | Lihat history commit | `git log --oneline -5` |

```bash
# Siklus dasar Git
echo "# My Project" > README.md
git status               # README.md = untracked (merah)
git add README.md        # stage file
git status               # README.md = staged (hijau)
git commit -m "init: add README"  # commit

# Edit file yang sudah di-track
sed -i 's/My Project/Project Baru/' README.md
git status               # README.md = modified (merah)
git add .
git commit -m "update: ganti judul"

# Melihat log
git log                         # semua commit
git log --oneline               # ringkas
git log --oneline --graph --all # visual branch
git log --oneline -5            # 5 commit terakhir
```

---

## Gitignore

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `.gitignore` | File untuk mengabaikan file/folder agar tidak di-track | File teks biasa di root project |
| `node_modules/` | Abaikan folder node_modules | `node_modules/` |
| `.env` | Abaikan file environment | `.env` |
| `*.log` | Abaikan semua file .log | `*.log` |
| `!important.log` | Tapi tetap track file ini | `!important.log` |
| `dist/` | Abaikan folder dist | `dist/` |
| `/build` | Abaikan folder build di root saja | `/build` |

```gitignore
# .gitignore
node_modules/
.env
.env.local
dist/
build/
*.log
.DS_Store
*.swp
coverage/
.next/
.cache/

# Tapi track ini
!important.log
```
