
# 🔄 Git Rebase: Guía Paso a Paso / Step-by-Step Guide (Bilingüe)

Esta guía incluye ejemplos detallados con los mensajes que verás en la consola y cómo lucirá el historial de Git **antes y después** de cada operación.  
This guide includes detailed examples showing what you’ll see in your terminal and how Git history looks **before and after** each operation.

---

## 📚 Índice / Table of Contents

- [1. Rebase básico / Basic rebase](#1-rebase-básico--basic-rebase)
- [2. Rebase interactivo / Interactive rebase](#2-rebase-interactivo--interactive-rebase)
- [3. Rebase avanzado con --onto](#3-rebase-avanzado-con---onto)
- [4. Autosquash y fixup](#4-autosquash-y-fixup)
- [5. Rebase con conflictos / Rebase with conflicts](#5-rebase-con-conflictos--rebase-with-conflicts)
- [6. Combinar commit 2 y 4 / Squash commit 2 and 4](#6-combinar-commit-2-y-4--squash-commit-2-and-4)

---

## 6. 🧩 Combinar commit 2 y 4 / Squash commit 2 and 4

### 🎯 Objetivo / Goal
Combinar el segundo y el cuarto commit en uno solo.  
Squash the second and fourth commits into one.

### 📍 Estado inicial / Initial state

```
git log --oneline --reverse

a1a1 Commit 1
b2b2 Commit 2  <-- queremos combinar este
c3c3 Commit 3
d4d4 Commit 4  <-- con este
e5e5 Commit 5
```

```
Historial visual:

    Commit 5 (e5e5)
    Commit 4 (d4d4) *
    Commit 3 (c3c3)
    Commit 2 (b2b2) *
    Commit 1 (a1a1)
```

---

### ⚙️ Método 1: Rebase interactivo / Interactive method

```bash
git rebase -i HEAD~5
```

En tu editor:

```
pick a1a1 Commit 1
pick b2b2 Commit 2
pick c3c3 Commit 3
pick d4d4 Commit 4
pick e5e5 Commit 5
```

➡️ Cambia a:

```
pick a1a1 Commit 1
pick c3c3 Commit 3
pick e5e5 Commit 5
pick b2b2 Commit 2
squash d4d4 Commit 4
```

Este reordena los commits y luego fusiona (squash) el 4 en el 2.

### ✅ Resultado final / Final result

```
a1a1 Commit 1
c3c3 Commit 3
e5e5 Commit 5
z9z9 Commit 2 + 4 (squashed)
```

---

### ⚙️ Método 2: No interactivo con autosquash / Non-interactive autosquash

1. Crea un commit de fixup respecto a `b2b2`

```bash
git checkout b2b2
# haz algún cambio aquí si es necesario
git commit --fixup b2b2
```

2. Ejecuta rebase con autosquash

```bash
git rebase -i --autosquash HEAD~5
```

El editor mostrará algo como:

```
pick a1a1 Commit 1
pick b2b2 Commit 2
fixup <hash> fixup! Commit 2
pick c3c3 Commit 3
pick d4d4 Commit 4
pick e5e5 Commit 5
```

Pero para squash entre commits no consecutivos, se recomienda **el método interactivo** ya que autosquash está diseñado para squash de cambios derivados, no commits no relacionados.

---

¿Quieres que también te lo convierta a HTML o agregar más ejemplos visuales como conflicto múltiple o rebase con ramas remotas?
