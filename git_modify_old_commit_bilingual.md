
# 🧩 Cómo modificar un commit antiguo en Git / How to Modify an Old Commit in Git

## 📚 Índice / Table of Contents

- [🇪🇸 Versión en Español](#🇪🇸-versión-en-español)
- [🇬🇧 English Version](#🇬🇧-english-version)

---

## 🇪🇸 Versión en Español

### 🎯 Objetivo

Dado un historial de commits:

```
C1 — C2 — C3
```

Queremos modificar el commit `C2` (añadir cambios) sin alterar el orden general.

Resultado deseado:

```
C1 — C2' — C3'
```

---

## 🛠️ Opción 1: Usando `git rebase -i` y `commit --amend`

### 1. Inicia un rebase interactivo desde antes de `C2`

```bash
git rebase -i HEAD~3
```

Cambia `pick` por `edit` en el commit `C2`:

```
pick <hash1> C1
edit <hash2> C2
pick <hash3> C3
```

### 2. Realiza tus cambios

```bash
echo "// cambio para C2" >> archivo.js
git add archivo.js
```

### 3. Modifica el commit con `--amend`

```bash
git commit --amend
```

### 4. Continúa el rebase

```bash
git rebase --continue
```

---

## 🧠 Opción 2: Usando `git commit --fixup` y `git rebase --autosquash` (más elegante)

### 1. Obtén el hash del commit a corregir

```bash
git log --oneline
```

### 2. Haz los cambios

```bash
echo "fix para C2" >> archivo.txt
git add archivo.txt
```

### 3. Crea un commit `fixup`

```bash
git commit --fixup <hash-de-C2>
```

### 4. Rebase con autosquash

```bash
git rebase -i --autosquash HEAD^^^
```

Git ordenará automáticamente el `fixup` junto al commit `C2`.

---

## 🇬🇧 English Version
## English Version

### 🎯 Goal

Given a commit history:

```
C1 — C2 — C3
```

We want to modify commit `C2` (e.g. add changes) without altering the overall sequence.

Expected result:

```
C1 — C2' — C3'
```

---

## 🛠️ Option 1: Using `git rebase -i` and `commit --amend`

### 1. Start an interactive rebase before `C2`

```bash
git rebase -i HEAD~3
```

Change `pick` to `edit` for `C2`:

```
pick <hash1> C1
edit <hash2> C2
pick <hash3> C3
```

### 2. Make your changes

```bash
echo "// change for C2" >> file.js
git add file.js
```

### 3. Amend the commit

```bash
git commit --amend
```

### 4. Continue the rebase

```bash
git rebase --continue
```

---

## 🧠 Option 2: Using `git commit --fixup` and `git rebase --autosquash` (more elegant)

### 1. Get the hash of the commit to fix

```bash
git log --oneline
```

### 2. Make the changes

```bash
echo "fix for C2" >> file.txt
git add file.txt
```

### 3. Create a fixup commit

```bash
git commit --fixup <hash-of-C2>
```

### 4. Rebase with autosquash

```bash
git rebase -i --autosquash HEAD^^^
```

Git will automatically place the `fixup` next to the target commit.

---

✅ You now have a clean and updated history!
