
# 🔄 Recuperar commits o ramas eliminadas con Git Reflog / Recover Deleted Commits or Branches with Git Reflog

## 📚 Índice / Table of Contents
- 🇪🇸 [Versión en Español](#versión-en-español)
- 🇬🇧 [English Version](#english-version)

---

## Versión en Español
## 🇪🇸 Versión en Español

### 🧠 Escenario 1: Recuperar commits eliminados tras `git reset --hard`

Supón que tenías estos commits:

```
C1 — C2 — C3 — C4
```

Y ejecutaste:

```bash
git reset --hard HEAD~2
```

Ahora solo tienes `C1 — C2`, pero **quieres recuperar `C3` y `C4`**.

#### ✅ Solución: Usar `git reflog`

```bash
git reflog
```

Verás una lista como:

```
abc1234 HEAD@{0}: reset: moving to HEAD~2
def5678 HEAD@{1}: commit: C4
789abcd HEAD@{2}: commit: C3
```

Para recuperar esos commits:

```bash
git checkout -b recuperacion HEAD@{1}
```

O puedes hacer:

```bash
git reset --hard HEAD@{1}
```
#### 💡 Tip pro

Después de un `reset --hard`, nunca hagas un `gc` (garbage collect) hasta haber revisado `reflog`, ya que Git podría borrar esos objetos si los considera inalcanzables.

---

### 🧠 Escenario 2: Recuperar una rama borrada

Si borraste una rama, por ejemplo:

```bash
git branch -D feature/login
```

Y quieres recuperarla:

1. Encuentra el commit más reciente:

```bash
git reflog
```

Busca una línea similar a:

```
bca4321 HEAD@{3}: checkout: moving from feature/login to master
```

2. Recrea la rama:

```bash
git branch feature/login bca4321
```

¡Y tu rama está de vuelta!

---

## English Version
## 🇬🇧 English Version

### 🧠 Scenario 1: Recover deleted commits after `git reset --hard`

Suppose you had these commits:

```
C1 — C2 — C3 — C4
```

Then you ran:

```bash
git reset --hard HEAD~2
```

Now you only see `C1 — C2`, but you want to **get back `C3` and `C4`**.

#### ✅ Solution: Use `git reflog`

```bash
git reflog
```

You'll see something like:

```
abc1234 HEAD@{0}: reset: moving to HEAD~2
def5678 HEAD@{1}: commit: C4
789abcd HEAD@{2}: commit: C3
```

To recover the commits:

```bash
git checkout -b recovery HEAD@{1}
```

Or simply:

```bash
git reset --hard HEAD@{1}
```

---

### 🧠 Scenario 2: Recover a deleted branch

If you deleted a branch like this:

```bash
git branch -D feature/login
```

And want to recover it:

1. Find the last commit:

```bash
git reflog
```

Look for something like:

```
bca4321 HEAD@{3}: checkout: moving from feature/login to master
```

2. Recreate the branch:

```bash
git branch feature/login bca4321
```

And your branch is back!

---

✅ With `git reflog`, nothing is ever truly lost (until Git garbage collects it)!
