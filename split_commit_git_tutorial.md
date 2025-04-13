
# ✂️ Cómo dividir (split) un commit anterior en Git

### 🎯 Objetivo

Dado un historial de commits:

```
C1 — C2 — C3
```

Queremos dividir el commit `C2` en dos commits separados (`C2'` y `C2''`) para que el resultado sea:

```
C1 — C2' — C2'' — C3
```

---

## 🧰 Requisitos

- Git instalado.
- Un historial limpio (sin cambios sin commitear o sin guardar).
- Estar en una rama donde puedas reescribir el historial (no hacer esto en `main` de producción sin cuidado).

---

## 🛠️ Paso a paso

### 1. Inicia un **rebase interactivo** desde tres commits atrás (ajusta según tu caso):

```bash
git rebase -i HEAD~3
```

Verás algo como esto en tu editor:

```text
pick <hash1> C1
pick <hash2> C2
pick <hash3> C3
```

---

### 2. Cambia `pick` por `edit` en el commit que deseas dividir (`C2`):

```text
pick <hash1> C1
edit <hash2> C2
pick <hash3> C3
```

Guarda y cierra el editor.

---

### 3. Haz un reset suave para deshacer el commit pero mantener los cambios staged:

```bash
git reset HEAD^ --soft
```

Esto deshace `C2` pero conserva todos sus cambios en el área de preparación (staging area).

---

### 4. Divide los cambios en dos commits:

Puedes usar `git add -p` para dividir los cambios por partes:

```bash
git add -p
git commit -m "C2' - primera parte del commit original"

git add .
git commit -m "C2'' - segunda parte del commit original"
```

O usar `git restore --staged <archivo>` si quieres manejar archivos enteros.

---

### 5. Continúa el rebase:

```bash
git rebase --continue
```

Git aplicará `C3` encima de los nuevos `C2'` y `C2''`.

---

## ✅ Resultado final

Tu historial se verá así:

```
C1 — C2' — C2'' — C3
```

¡Y listo! Has dividido un commit anterior con éxito 🧙‍♂️✨
