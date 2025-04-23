
# 🧩 Mover un commit de una rama a otra / Move commit between branches

## 📚 Índice / Table of Contents

- 🇪🇸 [Versión en Español](#versión-en-español)
- 🇬🇧 [English Version](#english-version)

---

## Versión en Español
## 🇪🇸 Versión en Español

### 🎯 Objetivo

Situacion actual:

```
master: C1 — C3 — C4
          \
login:     C2
```

Queremos mover el commit `C3` a la rama login.

Resultado deseado:

```
master: C1 — C4
          \
login:     C2 — C3
```

---
## Solución: Usar git cherry-pick + git rebase o reset

### 1. Cambia a la rama login
```bash
git checkout login
```

### 2. Añade el commit C3 con cherry-pick

Busca el hash de `C3`:

```
git log --oneline master
```
Una vez tengas el hash de C3, digamos abc123, lo añades a login:

```bash
git cherry-pick abc123
```
Ahora login tendrá: C1 — C2 — C3

### 3. Vuelve a master y elimina C3 de allí
```bash
git checkout master
```
Hay dos formas de hacerlo:

### Opción A: Reescribir historial con interactive rebase
```bash
git rebase -i HEAD~2
```
Cambia la línea de C3 de:
```bash
pick abc123 C3
```
a:
```bash
drop abc123 C3
```

### Opción B: Usar git reset
Si C4 no depende de C3 (es decir, son independientes):

```bash
git rebase -i C1
```
Y simplemente eliminas el commit C3 de la lista.

### 4. (Opcional) Forzar el push si ya habías subido
```bash
git push --force
```

Resultado final
```bash
master: C1 — C4
          \
login:     C2 — C3
```
