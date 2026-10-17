# 11. Deshacer y recuperar cambios con seguridad

## 11.1. Antes de deshacer, identifica dónde está el cambio

No existe un único comando para «volver atrás». La operación correcta depende de si el cambio está **sin preparar**, **preparado**, **confirmado localmente** o **publicado**. Ejecuta primero:

```bash
git status
git log --oneline -5
```

!!! danger "No ejecutes comandos destructivos sin comprender su alcance"
    `git reset --hard`, `git clean -fd` y ciertas opciones de restauración pueden eliminar trabajo no guardado en commits. Haz una copia o un commit de seguridad cuando haya dudas.

## 11.2. Descartar cambios no preparados

```bash
git restore HolaGit.java
```

Recupera la versión del índice para ese archivo y **descarta modificaciones no preparadas**. No sirve para recuperar archivos sin seguimiento ni borra automáticamente commits anteriores.

## 11.3. Retirar cambios de staging

```bash
git restore --staged HolaGit.java
```

Saca el archivo de la zona de preparación, pero conserva las modificaciones en el directorio de trabajo. Es útil cuando ejecutaste `git add .` y preparaste un archivo por error.

## 11.4. Deshacer un commit publicado: `revert`

```bash
git revert HEAD
```

Crea un **nuevo commit** que intenta invertir los cambios introducidos por el commit indicado. Conserva el historial y suele ser la opción preferible cuando otros ya han descargado el commit. Si hay conflictos, deben resolverse antes de finalizar la operación.

## 11.5. Mover la rama: `reset`

| Comando | Efecto sobre HEAD | Staging | Directorio de trabajo |
|---|---|---|---|
| `git reset --soft HEAD~1` | Retrocede un commit | Conserva los cambios preparados | Conserva cambios |
| `git reset --mixed HEAD~1` | Retrocede un commit | Deja cambios sin preparar | Conserva cambios |
| `git reset --hard HEAD~1` | Retrocede un commit | Ajusta al commit elegido | **Descarta cambios** |

`--mixed` es el modo predeterminado. `reset` cambia la historia de la rama; si ya publicaste commits, coordina cualquier reescritura con el equipo.

## 11.6. Guardar trabajo temporalmente: `stash`

```bash
git stash push -m "Trabajo a medias del menú"
git stash list
git stash pop
```

`stash` guarda temporalmente cambios de archivos seguidos (y cambios preparados). Por defecto **no incluye archivos sin seguimiento**; para incluirlos utiliza `git stash push -u`. `pop` intenta aplicar y retirar la entrada; si aparecen conflictos, tendrás que resolverlos.

## 11.7. Recuperar referencias con `reflog`

```bash
git reflog
```

`reflog` registra movimientos locales de referencias y de `HEAD`, y puede ayudarte a localizar un commit después de un `reset` o un cambio de rama. **No es una copia de seguridad garantizada**: sus entradas caducan y no se transfieren normalmente al remoto.

## 11.8. Archivos sin seguimiento y limpieza

Antes de borrar archivos generados, inspecciona:

```bash
git clean -nd
```

`-n` simula y `-d` incluye directorios sin seguimiento. `git clean -fd` realiza el borrado real; **no lo ejecutes sin revisar cuidadosamente la simulación**.

## Casos prácticos

1. Preparaste por error `README.md` pero quieres seguir editándolo: utiliza `git restore --staged README.md`.
2. Publicaste un commit que introduce un fallo: valora `git revert <hash>`.
3. Necesitas cambiar de rama con trabajo sin terminar: crea un commit provisional o utiliza `stash`.
4. Quieres inspeccionar una versión antigua sin modificar tus archivos: utiliza `git show REVISION:ruta`.

??? success "Decisión razonada"
    Para cambios publicados, `revert` conserva un historial compartido coherente. Para archivos preparados, `restore --staged` no descarta el trabajo. Para cambios locales no confirmados, `restore` puede ser destructivo: debe utilizarse conscientemente.

**Siguiente:** [Buenas prácticas](12-buenas-practicas.md).
