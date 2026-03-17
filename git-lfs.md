# Git LFS Setup & PDF Migration Guide

This guide explains how to enable **Git Large File Storage (LFS)** for handling large assets, migrate existing history, and verify that the migration is successful.

## 📦 1. Install Git LFS

```sh
git lfs install
```

Running this command initializes Git LFS for your repository.

## 📝 2. Track Files Using LFS

Tell Git LFS to manage all `.wav` files:

```sh
git lfs track "*.wav"
```

This updates the `.gitattributes` file.  
Commit the change:

```sh
git add .gitattributes
git commit -m "Track PDFs via Git LFS"
```

> [!CAUTION]
> Git **will not** automatically migrate existing PDFs in your history into LFS. You must rewrite the repository's history for that.

## 🔄 3. Migrate Existing History (Move Old WAVs Into LFS)

To rewrite history and replace historical PDF blobs with LFS pointers:

```sh
git lfs migrate import --include="*.wav" --everything
```

### 📌 What `--everything` means

`--everything` rewrites **all branches and all tags**.  
Use it if:

- You want the entire repository history to be clean
- You want _no_ large PDFs left in any branch or tag history

You may omit it if:

- You only want to migrate specific branches
- You want to avoid rewriting tags
- You want a lighter and safer migration

**Example (rewrite only `main`):**

```sh
git lfs migrate import --include="*.pdf" --include-ref=refs/heads/main
```

## ⬆️ 4. Force‑Push Updated History

If you rewrote history, branches must be force‑pushed:

```sh
git push --force --all
```

### 📌 About `git push --force --tags`

```sh
git push --force --tags
```

Needed only if:

- You used `--everything` **or**
- You rewrote commits that tags point to

If tags were **not** modified during migration, you don’t need this.

> [!CAUTION]
> **Warning**: All collaborators must re‑clone or reset their local repos after this step.

### Safer alternative for branches

```sh
git push --force-with-lease --all
```

## 🧹 5. (Optional) Clean Local Git Objects

This helps remove obsolete blobs and reduce repo size:

```sh
git gc --aggressive --prune=now
```

## ✅ 6. Verify That Files Are Now Tracked by LFS

List all files managed by Git LFS:

```sh
git lfs ls-files
```

You should see all `.pdf` entries listed here.
