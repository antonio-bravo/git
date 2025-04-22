
# 🔄 Git Rebase: Guía Completa con Ejemplos, Diagramas y Buenas Prácticas

## 📚 Índice
- [¿Qué es `git rebase`?](#qué-es-git-rebase)
- [Tipos de `rebase`](#tipos-de-rebase)
- [🧱 Casos comunes con diagramas](#casos-comunes-con-diagramas)
- [📌 Comandos útiles](#comandos-útiles)
- [⚠️ Cuándo evitarlo](#cuándo-evitarlo)
- [🧠 Consejos avanzados](#consejos-avanzados)

---

## ¿Qué es `git rebase`?

`git rebase` es una herramienta que **reescribe el historial de Git** moviendo commits de una rama sobre otra base. A diferencia de `merge`, rebase genera un historial **más lineal y limpio**.

---

## Tipos de `rebase`

### 1. `git rebase <branch>`

Rebasa tu rama actual sobre otra:

```bash
git checkout feature
git rebase main
```

> Aplica los commits de `feature` sobre el último commit de `main`.

📈 Diagrama antes:

```
main:    A---B---C
feature:         D---E
```

📉 Después de `rebase`:

```
main:    A---B---C
                \
feature:          D'--E'
```

---

### 2. `git rebase -i` (Interactivo)

Te permite:
- Reordenar commits
- Cambiar mensajes (`reword`)
- Combinar commits (`squash`, `fixup`)
- Eliminar commits (`drop`)

```bash
git rebase -i HEAD~3
```

✏️ Abre un editor con algo como:

```
pick a1 Commit 1
reword b2 Commit 2
squash c3 Commit 3
```

---

### 3. `git rebase --onto`

Rebasa un subconjunto de commits sobre otro punto:

```bash
git rebase --onto new-base old-base feature
```

📈 Ejemplo:

```
       A---B---C (main)
      /
D---E---F---G (feature)
```

```bash
git checkout feature
git rebase --onto C E
```

📉 Resultado:

```
       A---B---C
                \
                 F'--G' (feature)
```

---

### 4. `git rebase --autosquash`

Cuando usas `--fixup` o `--squash`:

```bash
git commit --fixup <commit-hash>
git rebase -i --autosquash HEAD~3
```

Reordena automáticamente los commits para agruparlos correctamente.

---

## Casos comunes con diagramas

### ✨ Limpiar historial antes de hacer `merge`

```
main:     A---B---C
feature:           D---E---F
```

```bash
git checkout feature
git rebase main
```

Resultado:

```
main:     A---B---C
                    \
feature:              D'--E'--F'
```

### 🪓 Editar o eliminar commits antiguos

```bash
git rebase -i HEAD~4
```

---

## Comandos útiles

```bash
git rebase main                     # rebase estándar
git rebase -i HEAD~N               # interactivo
git rebase --abort                 # cancelar un rebase
git rebase --continue              # continuar tras resolver conflictos
git rebase --skip                  # saltar commit con error
git rebase --onto <new> <old> <branch>  # avanzada
git commit --fixup <hash>          # crear commit para autosquash
```

---

## ⚠️ Cuándo evitarlo

- ❌ No hagas rebase a ramas compartidas si ya hiciste `push`
- ❌ Evita rebase en `main` o `master` si más personas colaboran

---

## 🧠 Consejos avanzados

- Usa `git log --graph` para ver el efecto de los rebase
- Rebase interactivo es ideal para preparar PRs limpios
- `--autosquash` + `--fixup` = magia para código en revisión

---

📌 Recuerda: Rebase es poderoso, pero **con gran poder viene gran responsabilidad** 🕸️
