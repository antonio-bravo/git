
# 🔄 Git Rebase: Guía Paso a Paso con Entradas, Salidas y Resultados Visuales

Esta guía incluye ejemplos detallados con los mensajes que verás en la consola y cómo lucirá el historial de Git **antes y después** de cada operación. Ideal para dominar `git rebase` con confianza.

---

## 🧭 1. `git rebase <branch>` - Rebase básico

### 🎯 Objetivo:
Reescribir los commits de una rama (`feature`) para que se apliquen encima de la base de otra (`main`).

### 📍 Estado inicial

```
git log --oneline --graph --all

* e5f6 (feature) Commit E
* d4c3 Commit D
| * c3b2 (main) Commit C
| * b2a1 Commit B
| * a1a1 Commit A
|/
```

### ⚙️ Comando

```bash
git checkout feature
git rebase main
```

### 🖥️ En pantalla

```
First, rewinding head to replay your work on top of it...
Applying: Commit D
Applying: Commit E
```

### ✅ Resultado final

```
*  f9f8 (feature) Commit E'
*  e7e6 Commit D'
*  c3b2 (main) Commit C
*  b2a1 Commit B
*  a1a1 Commit A
```

---

## ✏️ 2. `git rebase -i` - Rebase interactivo

### 🎯 Objetivo:
Editar, reordenar, unir o eliminar commits recientes.

### 📍 Estado inicial

```
* e5f6 Commit E
* d4c3 Commit D
* c3b2 Commit C
* b2a1 Commit B
* a1a1 Commit A
```

### ⚙️ Comando

```bash
git rebase -i HEAD~3
```

### 🖥️ En pantalla

Se abre tu editor con:

```
pick c3b2 Commit C
reword d4c3 Commit D
squash e5f6 Commit E
```

Tú cambias a:

```
pick c3b2 Commit C
reword d4c3 Mejorar texto en D
squash e5f6 Unir E en D
```

Luego se te pedirá que edites el mensaje del commit combinado.

### ✅ Resultado final

```
* z9z8 Commit C
* y8y7 Mejorar texto en D + Unir E
* b2a1 Commit B
* a1a1 Commit A
```

---

## 🔀 3. `git rebase --onto` - Rebase avanzado

### 🎯 Objetivo:
Mover parte del historial de una rama a otro punto base.

### 📍 Estado inicial

```
       A---B---C (main)
      /
D---E---F---G (feature)
```

Queremos aplicar `F` y `G` sobre `C`, ignorando `D` y `E`.

### ⚙️ Comando

```bash
git checkout feature
git rebase --onto C E
```

### 🖥️ En pantalla

```
First, rewinding head to replay your work on top of it...
Applying: Commit F
Applying: Commit G
```

### ✅ Resultado final

```
main:    A---B---C
                  \
feature:            F'--G'
```

---

## 🪄 4. `git rebase --autosquash` + `--fixup`

### 🎯 Objetivo:
Agregar un pequeño cambio como corrección de un commit anterior, y agruparlo automáticamente.

### 📍 Estado inicial

```
* e5f6 Fix typo
* d4c3 Initial login
* c3b2 Setup project
```

Quieres que `Fix typo` se una a `Initial login`.

### ⚙️ Comandos

```bash
git commit --fixup d4c3
git rebase -i --autosquash HEAD~3
```

### 🖥️ En pantalla

Se abre tu editor con:

```
pick c3b2 Setup project
pick d4c3 Initial login
fixup e5f6 fixup! Initial login
```

### ✅ Resultado final

```
* z9z8 Initial login + Fix typo
* c3b2 Setup project
```

---

## 🧯 5. Rebase con conflicto

### 📍 Estado inicial

Ambas ramas modifican el mismo archivo.

```bash
git rebase main
```

### 🖥️ En pantalla

```
CONFLICT (content): Merge conflict in index.js
```

### ⚙️ Resolver

```bash
# Editar el archivo para resolver
git add index.js
git rebase --continue
```

---

¿Quieres que lo prepare como `.md` para que puedas descargarlo y subirlo a tu GitHub?
