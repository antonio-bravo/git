
# ↩️ Revertir un commit intermedio en Git / Revert a Middle Commit in Git

## 📚 Índice / Table of Contents
- 🇪🇸 [Versión en Español](#versión-en-español)
- 🇬🇧 [English Version](#english-version)

---

## 🇪🇸 Versión en Español

### 🧠 Escenario

Tienes una secuencia de commits como esta:
```bash
C1 — C2 — C3 — C4 — C5 ← HEAD
```

- Y quieres revertir C3, que está en medio del historial.

---

### ✅ Paso 1: Encontrar el hash del commit

```bash
git log --oneline
```

Ejemplo:

```bash
e5f6a7c (HEAD -> main) C5  
b3c4d5e C4  
a7b8c9d C3  ← este es el que quieres revertir  
f2e3d4c C2  
a1b2c3d C1
```

---

### ✅ Paso 2: Revertir el commit

```bash
git revert a7b8c9d
```

Esto crea un nuevo commit que revierte los cambios de C3.

Ejemplo:

```bash
C1 — C2 — C3 — C4 — C5 — C6 (revert of C3)
```

---

### 🔀 ¿Y si el commit es un merge?

```bash
git revert -m 1 <hash_merge>
```

-m 1 indica mantener el primer padre del merge (por ejemplo, main).

---

### ❗ Si hay conflictos
Resuélvelos, luego:
```bash
git add .
git commit
```

---

## 🇬🇧 English Version

### 🧠 Scenario

You have a sequence like:
```bash
C1 — C2 — C3 — C4 — C5 ← HEAD
```

- You want to revert C3, which is in the middle of the history.

---

### ✅ Step 1: Get the hash

```bash
git log --oneline
```

Example:

```bash
e5f6a7c (HEAD -> main) C5  
b3c4d5e C4  
a7b8c9d C3  ← this is the one you want to revert  
f2e3d4c C2  
a1b2c3d C1
```

---

### ✅ Step 2: Revert it

```bash
git revert a7b8c9d
```

That will create a new commit reversing C3:

Example:

```bash
C1 — C2 — C3 — C4 — C5 — C6 (revert of C3)
```

---

### 🔀 Reverting a merge commit?

```bash
git revert -m 1 <hash_merge>
```
Where -m 1 keeps the first parent (e.g., main).

---

### ❗ If conflicts happen
Fix them, then:
```bash
git add .
git commit
```

---

✅ With Git, you can always go back in time!
