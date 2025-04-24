
# 🧠 Git Rebase explicado como si tuvieras 5 años (o como si fueras nuevo en Git)

> Una guía visual, paso a paso, y muy fácil de entender sobre `git rebase -i` y `git rebase --onto`.

---

## ✨ ¿Qué es un rebase?

Imagina que tienes una torre de bloques. Cada bloque es un cambio (commit).  
Con `git rebase`, puedes **reordenar**, **editar**, o **mover** esos bloques como si estuvieras construyendo una torre nueva, sin destruir la anterior.

---

## 🎭 Parte 1: `git rebase -i` (interactivo)

### ¿Qué hace?

Te deja abrir un menú y decirle a Git:

- ¿Qué commits quieres cambiar?
- ¿Cuál quieres borrar, cambiar, combinar o reordenar?

---

### 🎯 Ejemplo:

#### 🔶 Tienes esta torre de commits:

```
A - B - C - D - E (HEAD)
```

Cada letra representa un commit.

Y los mensajes de commit podrían ser:

```
A: Primer commit
B: Agrega login
C: Corrige login
D: Agrega logout
E: Ajustes finales
```

---

### 👨‍💻 Usas:

```bash
git rebase -i HEAD~4
```

> Esto abre los últimos 4 commits (`B`, `C`, `D`, `E`) para editarlos.

---

### 📜 Git te muestra esto:

```
pick B Agrega login
pick C Corrige login
pick D Agrega logout
pick E Ajustes finales
```

---

### ✍️ Tú lo cambias a:

```
pick B Agrega login
squash C Corrige login   # Une C dentro de B
reword D Agrega logout   # Cambia el mensaje de D
pick E Ajustes finales
```

---

### 🧠 ¿Qué pasará?

- `B` y `C` serán 1 solo commit (squash)
- El mensaje de `D` podrá cambiar
- `E` queda igual

---

### 📦 Resultado:

```
A - B' - D' - E
```

✅ Mucho más limpio, como si nunca hubieras cometido errores 😎

---

## 🎭 Parte 2: `git rebase --onto`

### ¿Qué hace?

Permite **mover** una secuencia de commits a otra base, como si tomaras una rama y la pegaras en otro sitio.

---

### 📦 Imagina esto:

```
main:     A - B - C
feature:           \ 
                    D - E - F
```

Quieres mover los commits `D - E - F` para que estén después de `B` en lugar de `C`.

---

### 🛠️ Comando:

```bash
git rebase --onto B C feature
```

- `B`: el nuevo lugar donde pegarás los commits
- `C`: el último commit que NO quieres mover
- `feature`: la rama que estás modificando

---

### 🧩 Resultado:

```
main:     A - B - C
feature:        \ 
                 D' - E' - F'   (basados en B, no en C)
```

---

## ✅ Cuándo usar cada uno:

| Situación                         | Usa `-i`         | Usa `--onto`      |
|----------------------------------|------------------|-------------------|
| Limpiar historial                | ✅               |                   |
| Editar un commit viejo           | ✅               |                   |
| Mover commits entre ramas        |                  | ✅                |
| Eliminar commits intermedios     | ✅               |                   |
| Rebase desde punto intermedio    |                  | ✅                |

---

## 🧯 Consejo final

Antes de hacer rebase, guarda una copia:

```bash
git branch respaldo-antes-del-rebase
```

Y si algo sale mal:

```bash
git rebase --abort
```

¿Quieres un PDF con ilustraciones de esto? 😄
