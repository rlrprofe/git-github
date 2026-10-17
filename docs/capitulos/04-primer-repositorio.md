# 4. Crear y utilizar el primer repositorio

## 4.1. Objetivo y punto de partida

Vamos a controlar las versiones de un pequeño programa Java. No necesitas conocer programación orientada a objetos: basta con un archivo `HolaGit.java`. Trabaja en una carpeta nueva para no mezclar este ejercicio con otros repositorios.

=== "PowerShell"

    ```powershell
    mkdir HolaGit
    cd HolaGit
    ```

=== "Bash"

    ```bash
    mkdir -p HolaGit
    cd HolaGit
    ```

## 4.2. Inicializar Git

```bash
git init -b main
git status
```

`git init` crea `.git` y `-b main` establece el nombre de la rama inicial. Si tu versión no admite `-b`, usa `git init` y después `git branch -M main`. `git status` debe indicar que todavía no hay commits.

## 4.3. Crear un archivo Java

Guarda este contenido en `HolaGit.java`:

```java
public class HolaGit {
    public static void main(String[] args) {
        System.out.println("Hola, Git");
    }
}
```

Comprueba el estado:

```bash
git status
```

Aparecerá como *untracked*. Esto no significa que el archivo esté mal: significa que todavía no lo hemos incluido en el seguimiento de Git.

## 4.4. Preparar y registrar la primera versión

```bash
git add HolaGit.java
git diff --staged
git commit -m "Crear programa inicial HolaGit"
git status
```

**Por qué se hace así:** `add` selecciona el contenido, `diff --staged` permite revisarlo, `commit` registra la versión y `status` comprueba que no quedan cambios pendientes. Un mensaje de commit útil describe **qué cambia**.

Si Git indica `Author identity unknown`, vuelve al capítulo 2 y configura nombre y correo.

## 4.5. Segunda versión: modificar y comparar

Cambia el mensaje a `Hola, control de versiones` y ejecuta:

```bash
git diff
git add HolaGit.java
git commit -m "Actualizar mensaje de bienvenida"
git log --oneline
```

Verás dos commits. El primero sigue existiendo: Git no ha sobrescrito el historial anterior. Para inspeccionar los cambios de un commit utiliza `git show <hash>` (sustituye `<hash>` por el identificador real).

## 4.6. Seleccionar archivos individualmente o todos

`git add HolaGit.java` prepara un archivo concreto. `git add .` prepara los cambios bajo el directorio actual, respetando `.gitignore`. Para proyectos reales es recomendable revisar `git status` y `git diff --staged` antes de confirmar; así evitas incorporar archivos temporales o información sensible.

!!! warning "No confundas `git add` con publicar"
    Ni `git add` ni `git commit` envían información a GitHub. Ambos trabajan sobre tu repositorio local.

## 4.7. Errores frecuentes

| Mensaje | Causa habitual | Solución |
|---|---|---|
| `not a git repository` | Estás fuera de la carpeta inicializada | Comprueba `pwd` o `Get-Location` |
| `nothing to commit` | No hay cambios preparados | Comprueba `git status` |
| `pathspec ... did not match` | Nombre o ruta incorrectos | Revisa la ruta y las mayúsculas |
| `Author identity unknown` | Falta configuración de autor | Configura `user.name` y `user.email` |

## Actividades

1. Crea un segundo archivo `README.md` explicando para qué sirve el programa y regístralo en un commit independiente.
2. Modifica `HolaGit.java` para imprimir dos líneas; comprueba los cambios antes del commit.
3. Anota los hashes abreviados de tus tres primeros commits.
4. Explica qué diferencia hay entre `git add .` y `git add HolaGit.java`.

??? success "Criterios de comprobación"
    El historial debe contener commits separados y descriptivos; `git status` debe terminar limpio; el alumno debe ser capaz de identificar qué archivos formaron parte de cada commit.

**Siguiente:** [Seguimiento de cambios e historial](05-seguimiento.md).
