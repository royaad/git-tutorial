# Git Filter Repo

**Permanently remove files (e.g., large/binary artifacts) from your entire Git history** so they disappear from every past commit.

## 📦 1. Install `git filter-repo`

On Linux & Windows:

```sh
pip install git-filter-repo
```

## 🧹 2. Remove files from the entire history

### Examples

#### 🎯 Remove file types

```sh
git filter-repo --invert-paths --path '*.zip' --path '*.mp4'
```

#### 📁 Remove a folder or specific file everywhere

```sh
git filter-repo --invert-paths --path 'build/'
git filter-repo --invert-paths --path 'secrets.env'
```

#### 🚫 Remove large files > 50MB

```sh
git filter-repo --strip-blobs-bigger-than 50M
```

## 🔍 3. Verify the cleanup

Check for large Git objects:

```sh
git verify-pack -v .git/objects/pack/*.idx | sort -k3 -n | tail
```

Confirm deleted files are gone:

```sh
git log --all -- '**/*.zip'
```

## 🚀 4. Force‑push the rewritten history

⚠️ _This rewrites public history._

```sh
git push origin --force-with-lease --all
git push origin --force-with-lease --tags
```

## 🔃 5. Ask collaborators to re‑clone

Simplest:

```sh
git clone <repo-url>
```

Or force‑sync:

```sh
git fetch
git reset --hard origin/main
```

## 🛡️ 6. Prevent future accidental commits (optional)

### Add to `.gitignore`

```plaintext
*.zip
*.env
build/
```

### Pre‑commit hook to block large files

**Installation:**

```sh
pip install pre-commit
pre-commit install
```

**`.pre-commit-config.yaml`:**

```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: check-added-large-files
        args: ["--maxkb=5000"]

      - id: forbid-files
        args:
          - --pattern
          - '(^|/)\.env($|\.|/)'
          - --pattern
          - '(^|/)\.env\..*'
        exclude: ''

  - repo: https://github.com/Yelp/detect-secrets
    rev: v1.5.0
    hooks:
      - id: detect-secrets
        args: ["--baseline", ".secrets.baseline"]
```

## 📌 7. Full example workflow (copy/paste)

```sh
pip install git-filter-repo
git filter-repo --invert-paths --path '*.zip'
git log --all -- '**/*.zip'
git push origin --force --all
git push origin --force --tags
```
