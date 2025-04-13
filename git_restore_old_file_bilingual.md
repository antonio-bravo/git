
# 📦 Recuperar versión antigua de un archivo o carpeta con Git / Restore an Old Version of a File or Folder with Git

## 📚 Índice / Table of Contents
- 🇪🇸 [Versión en Español](#versión-en-español)
- 🇬🇧 [English Version](#english-version)

---

## 🇪🇸 Versión en Español

### 🧠 Escenario

Tienes un archivo o carpeta en tu proyecto Git y deseas:
- Ver o recuperar una versión antigua
- Posiblemente restaurar la versión actual si no te gusta el cambio

---

### ✅ Ver historial de un archivo

```bash
git log --oneline nombre_del_archivo
```

Ejemplo:

```bash
git log --oneline main.py
```

---

### ✅ Ver contenido antiguo sin cambiar nada

```bash
git show <commit>:nombre_del_archivo
```

Ejemplo:

```bash
git show 123abcd:main.py
```

---

### ✅ Recuperar archivo de un commit antiguo

```bash
git checkout <commit> -- nombre_del_archivo
```

Ejemplo:

```bash
git checkout 123abcd -- main.py
```

Esto reemplaza el archivo actual en tu working directory.

---

### 📂 Recuperar carpeta completa de un commit antiguo

```bash
git checkout <commit> -- ruta/a/la/carpeta
```

Ejemplo:

```bash
git checkout 123abcd -- src/
```

---

### 🛑 Recuperar versión actual si te arrepientes

Si **aún no hiciste commit**, simplemente:

```bash
git restore nombre_del_archivo
```

O para una carpeta:

```bash
git restore -s HEAD ruta/a/la/carpeta
```

---

### 🔁 ¿Y si ya hiciste commit y quieres deshacerlo?

```bash
git log --oneline
git revert <hash_del_commit>
```

O si estás seguro y no hiciste nada más:

```bash
git reset --hard HEAD
```

---

## 🇬🇧 English Version

### 🧠 Scenario

You have a file or folder in your Git project and you want to:
- View or restore a previous version
- Optionally return to the latest version if needed

---

### ✅ View file history

```bash
git log --oneline filename
```

Example:

```bash
git log --oneline main.py
```

---

### ✅ View old content without changing anything

```bash
git show <commit>:filename
```

Example:

```bash
git show 123abcd:main.py
```

---

### ✅ Recover an old version of a file

```bash
git checkout <commit> -- filename
```

Example:

```bash
git checkout 123abcd -- main.py
```

This replaces the file in your working directory.

---

### 📂 Recover a folder from an old commit

```bash
git checkout <commit> -- path/to/folder
```

Example:

```bash
git checkout 123abcd -- src/
```

---

### 🛑 Restore latest version if you change your mind

If you **haven’t committed yet**:

```bash
git restore filename
```

Or for a folder:

```bash
git restore -s HEAD path/to/folder
```

---

### 🔁 What if you've already committed and want to undo it?

```bash
git log --oneline
git revert <commit_hash>
```

Or, if safe to reset:

```bash
git reset --hard HEAD
```

---

✅ With Git, you can always go back in time!
