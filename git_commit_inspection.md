# 🔍 Exploración de Commits en Git

Cuando trabajas con repositorios grandes o históricos complejos, entender qué pasó en cada commit y cómo se relacionan es clave.  
Estos comandos te ayudarán a inspeccionar cambios con gran detalle.

---

## `git show`

Muestra la información completa de un commit específico:  
- **Mensaje de commit**  
- **Autor y fecha**  
- **Diferencias introducidas (diff)**  

```bash
git show <commit_hash>
```

Opciones útiles:
- `--stat` → Muestra resumen de cambios por archivo.
- `--name-only` → Lista solo los nombres de archivos cambiados.
- `--pretty=short` → Resumen corto de metadatos sin diff.

Ejemplo:
```bash
git show abc123 --stat
```

---

## `git diff-tree`

Permite ver de forma más estructurada qué archivos cambiaron entre commits o en un commit específico.

```bash
git diff-tree <commit_hash>
```

Opciones útiles:
- `-r` → Muestra el diff de manera recursiva por carpetas.
- `--name-status` → Lista archivos con el tipo de cambio (`A`, `M`, `D`).
- `--no-commit-id` → Oculta el hash del commit al listar.

Ejemplo:
```bash
git diff-tree --no-commit-id --name-status -r abc123
```

---

## Otros comandos complementarios

### `git log --stat`
Muestra el historial con un resumen de archivos cambiados y cantidad de líneas añadidas/borradas.

```bash
git log --stat
```

---

### `git whatchanged`
Obsoleto, pero útil para combinar `git log` con lista de cambios en cada commit.

```bash
git whatchanged -p
```

---

### `git diff`
Compara el contenido entre dos commits, ramas o el working tree.

```bash
git diff <commit1> <commit2>
```

---

💡 **Tip**: Para buscar en el historial un cambio específico, combina `git log` con:
```bash
git log --grep="texto"   # Busca por mensaje de commit
git log -S "código"      # Busca commits que añaden o eliminan una cadena
```
