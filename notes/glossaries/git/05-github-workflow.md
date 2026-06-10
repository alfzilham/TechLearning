# GitHub Workflow

## Pull Request

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| PR (Pull Request) | Minta perubahan kamu di-merge ke branch lain | GitHub.com → New Pull Request |
| Base branch | Target merge (biasanya `main`) | base: `main` |
| Compare branch | Branch yang berisi perubahan kamu | compare: `feature-auth` |
| Draft PR | PR yang belum siap di-review | Create Draft PR |
| Code review | Review PR sebelum merge | Comment, Approve, Request Changes |
| Assignee | Orang yang bertanggung jawab | Assign reviewer |
| Labels | Tag untuk PR (bug, enhancement) | `bug`, `feature` |

```bash
# Workflow PR:
# 1. Buat branch fitur
git checkout -b feature/login

# 2. Kerja & commit
git add . && git commit -m "feat: add login form"

# 3. Push ke remote
git push -u origin feature/login

# 4. Di GitHub: Create Pull Request
# 5. Reviewer approve → Merge
```

---

## Fork & Clone

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Fork | Copy repo orang lain ke akunmu | GitHub.com → Fork |
| Clone | Download repo lokal | `git clone <url>` |
| Upstream remote | Remote ke repo original | `git remote add upstream <url>` |
| Sync fork | Update fork dengan repo original | `git pull upstream main` |

```bash
# Fork repo orang lain → lalu clone punyamu
git clone https://github.com/user/repo.git
cd repo

# Tambah remote original sebagai "upstream"
git remote add upstream https://github.com/original/repo.git

# Sync fork dengan upstream
git checkout main
git pull upstream main       # ambil dari original
git push origin main         # update fork-mu
```

---

## Tag & Release

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git tag <nama>` | Buat tag (lightweight) | `git tag v1.0.0` |
| `git tag -a <nama> -m "pesan"` | Buat annotated tag (dengan metadata) | `git tag -a v1.0.0 -m "Release v1.0.0"` |
| `git tag` | Lihat daftar tag | `git tag` |
| `git push --tags` | Push semua tag ke remote | `git push --tags` |
| `git push origin <tag>` | Push tag tertentu | `git push origin v1.0.0` |
| `git tag -d <nama>` | Hapus tag lokal | `git tag -d v1.0.0` |
| GitHub Release | Buat release dari tag via UI | Releases → Draft new release |

```bash
# Buat tag versi
git tag -a v1.0.0 -m "First stable release"
git tag v1.1.0-beta           # lightweight

# Push tag
git push origin v1.0.0
git push --tags               # push semua tag

# Delete tag local & remote
git tag -d v1.0.0
git push origin --delete v1.0.0
git push origin :v1.0.0       # cara lama
```

---

## GitHub Issues

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| Issue | Melacak bug, fitur, tugas | New Issue |
| Labels | Kategori issue | `bug`, `enhancement`, `good first issue` |
| Milestone | Kelompok issue untuk rilis | `v1.0`, `sprint-1` |
| Assignee | Orang yang mengerjakan | Assign yourself |
| Close issue | Tutup dengan commit message | `git commit -m "fixes #12"` |

```bash
# Auto-close issue dengan commit
git commit -m "fix: resolve login bug

Closes #12"
# Saat di-merge ke main, issue #12 auto close

# Keywords: closes, fixes, resolve
git commit -m "feat: add profile page

Closes #15, #16"  # multiple issues
```

---

## GitHub CLI (`gh`)

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `gh auth login` | Login GitHub CLI | `gh auth login` |
| `gh repo create` | Buat repo baru dari CLI | `gh repo create my-repo --public --push` |
| `gh pr create` | Buat PR dari CLI | `gh pr create --base main --title "feat: ..."` |
| `gh pr checkout <number>` | Checkout PR number untuk review | `gh pr checkout 12` |
| `gh pr list` | Lihat daftar PR | `gh pr list --state open` |
| `gh pr review` | Review PR dari CLI | `gh pr review 12 --approve` |
| `gh issue list` | Lihat issues | `gh issue list --label bug` |
| `gh release create` | Buat release | `gh release create v1.0.0 --title "v1.0.0"` |

```bash
# Setup repo baru & push
gh repo create my-repo --public --source=. --push

# Buat PR
gh pr create \
  --base main \
  --head feature-auth \
  --title "feat: add authentication" \
  --body "Added login and register" \
  --assignee @me \
  --label enhancement

# Review PR
gh pr checkout 12         # checkout PR untuk test lokal
gh pr review 12 --approve  # approve

# Lihat PR
gh pr list
gh pr status

# Buat release
gh release create v1.0.0 --title "v1.0.0" --notes "First release"
```

---

## Advanced Rebase & Squash

| Konsep | Penjelasan | Contoh |
|--------|-----------|--------|
| `git rebase -i HEAD~n` | Interactive rebase | Squash, reword, drop |
| `git log --author="nama"` | Filter commit by author | `git log --oneline --author="Rizky"` |

```bash
# Squash 3 commit terakhir jadi 1
git rebase -i HEAD~3
# Picker:
# pick abc123 feat: add form
# squash def456 fix: form validation
# squash ghi789 style: form styling
# → hasil: 1 commit "feat: add form with validation & styling"

# Cherry-pick — ambil commit dari branch lain
git checkout main
git cherry-pick abc123       # ambil commit abc123 ke main
git cherry-pick abc123..def456  # range commit
```
