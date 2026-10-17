# 5. Seguimiento de cambios e historial

## 5.1. Leer el historial

Un historial útil permite responder: **qué cambió, cuándo, quién lo hizo y por qué**. El mensaje del commit debe aportar el motivo o propósito; Git registra además autor y fechas.

```bash
git log
git log --oneline
git log --oneline --graph --decorate --all
git log -5
```

`--graph` dibuja la estructura de los commits, `--decorate` muestra referencias de ramas y `-5` limita el resultado a cinco entradas. Pulsa `q` para salir del paginador cuando aparezca.

## 5.2. Comparar versiones con `git diff`

```bash
git diff                 # cambios en el directorio de trabajo no preparados
git diff --staged        # cambios preparados para el próximo commit
git diff HEAD            # cambios del directorio y staging frente a HEAD
git diff HEAD~1 HEAD     # diferencia entre los dos últimos commits
```

Los signos `+` y `-` representan líneas añadidas y eliminadas. El formato *unified diff* incluye contexto para comprender dónde se modificó el archivo. `HEAD~1` significa el primer antecesor de `HEAD`; requiere al menos dos commits.

## 5.3. Consultar un commit

```bash
git show HEAD
git show --stat HEAD
git show --name-only HEAD
```

`--stat` resume los archivos y el número de líneas cambiadas; `--name-only` muestra nombres. Para inspeccionar una versión antigua de un archivo **sin modificar el directorio de trabajo**:

```bash
git show HEAD~1:HolaGit.java
```

La sintaxis `REVISION:ruta` recupera el contenido del archivo tal como existía en esa revisión.

## 5.4. Historial de un archivo y autoría de líneas

```bash
git log --oneline -- HolaGit.java
git log -p -- HolaGit.java
git blame HolaGit.java
```

`--` separa las opciones de las rutas; `-p` incluye los parches. `blame` muestra el último commit que modificó cada línea, pero **no determina quién es responsable de un problema**: puede faltar contexto de cambios anteriores.

## 5.5. Escribir mensajes de commit útiles

Evita mensajes como `cambios`, `arreglo` o `final`. Prefiere descripciones específicas:

```text
Añadir validación de precio en Producto
Corregir cierre de conexión JDBC
Documentar instrucciones de ejecución
```

Un commit debería agrupar cambios relacionados. Si mezclas una corrección, un cambio visual y una actualización de dependencias, después será más difícil revisar o revertir el trabajo.

## 5.6. Corregir el último commit con `--amend`

Si acabas de crear un commit local y olvidaste un archivo:

```bash
git add README.md
git commit --amend --no-edit
```

O cambia su mensaje:

```bash
git commit --amend -m "Documentar instalación del proyecto"
```

!!! danger "Un commit enmendado cambia de identidad"
    `--amend` crea un commit nuevo que sustituye al anterior en tu rama. Evítalo si el commit ya está compartido: reescribir historial publicado puede complicar el trabajo de otras personas.

## 5.7. Ejercicio guiado

En tu repositorio `HolaGit`: crea un commit para el README, otro para un cambio de código y otro para documentación. Ejecuta `git log --oneline`, `git show --stat HEAD` y `git diff HEAD~2 HEAD`. Explica qué información aporta cada comando.

??? success "Respuesta orientativa"
    `log` enumera versiones; `show --stat` resume el último commit; `diff HEAD~2 HEAD` compara el estado actual con el de dos commits antes. La comparación es entre instantáneas, no una lista de instrucciones ejecutadas.

**Siguiente:** [GitHub y repositorios remotos](06-remotos.md).
