
# ↩️ Cambiar el mensaje del último commit / Change message in last commit

## 📚 Índice / Table of Contents
- 🇪🇸 [Versión en Español](#versión-en-español)
- 🇬🇧 [English Version](#english-version)

---

## 🇪🇸 Versión en Español

### 🧠 Escenario

Supongamos que hiciste esto:
```bash
git commit -m "Arr bug"
```

- Y luego te das cuentas de que quieres arreglarlo.

---

### ✅ Opción 1: Sin afectar nada más (no has hecho push todavía)

```bash
git commit --amend -m "Nuevo mensaje del commit"
```
Esto reescribe solo el *mensaje del último commit*, manteniendo los cambios intactos.

---

### ✅ Opción 2: Ya hiciste push (¡cuidado!)
Si *ya hiciste `git push` al repositorio remoto*, tendrás que forzar el push porque estás reescribiendo el historial:

```bash
git commit --amend -m "Nuevo mensaje corregido"
git push --force
```

⚠️ Cuidado: Solo deberías hacer esto si trabajas solo en la rama, o si sabes que los demás están de acuerdo en que se reescriba el historial.

---

## 🇬🇧 English Version

### 🧠 Scenario

You did something like this:
```bash
git commit -m "Bad message"
```

- And then you realize you want to fix it.

---

### ✅ Option 1: Without affecting anything else (you haven't pushed yet)

```bash
git commit --amend -m "New message"
```
This rewrites only the *New message*, keeping the changes intact.

---

### ✅ Option 2: You already pushed (be careful!)
If you *already did `git push` to the remote repository*, you'll have to force the push because you're rewriting history:

```bash
git commit --amend -m "New fixed message"
git push --force
```

⚠️ Caution: You should only do this if you are working alone on the branch, or if you know that everyone else agrees to rewriting the history.

---

✅ With Git, you can always go back in time!
