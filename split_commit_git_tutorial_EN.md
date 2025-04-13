
# ✂️ How to Split an Old Commit in Git

### 🎯 Goal

Given a commit history like:

```
C1 — C2 — C3
```

We want to split commit `C2` into two separate commits (`C2'` and `C2''`), resulting in:

```
C1 — C2' — C2'' — C3
```

---

## 🧰 Requirements

- Git installed.
- A clean working directory (no unstaged or uncommitted changes).
- You should be on a branch where rewriting history is safe (don’t do this on production `main`).

---

## 🛠️ Step-by-Step

### 1. Start an **interactive rebase** from three commits back (adjust as needed):

```bash
git rebase -i HEAD~3
```

You'll see something like this in your editor:

```text
pick <hash1> C1
pick <hash2> C2
pick <hash3> C3
```

---

### 2. Change `pick` to `edit` for the commit you want to split (`C2`):

```text
pick <hash1> C1
edit <hash2> C2
pick <hash3> C3
```

Save and close the editor.

---

### 3. Perform a soft reset to undo the commit but keep the changes staged:

```bash
git reset HEAD^ --soft
```

This undoes `C2` but preserves all changes in the staging area.

---

### 4. Split the changes into two commits:

You can use `git add -p` to interactively choose which changes to stage:

```bash
git add -p
git commit -m "C2' - first part of the original commit"

git add .
git commit -m "C2'' - second part of the original commit"
```

Or use `git restore --staged <file>` to manage by file.

---

### 5. Continue the rebase:

```bash
git rebase --continue
```

Git will apply `C3` on top of your new `C2'` and `C2''`.

---

## ✅ Final Result

Your history will now look like:

```
C1 — C2' — C2'' — C3
```

And that's it! You've successfully split a previous commit 🧙‍♂️✨
