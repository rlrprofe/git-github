# 3. Fundamentos de Git: archivos, estados y áreas

## 3.1. Un modelo mental antes de memorizar comandos

Git no es una carpeta de copias de seguridad. Es una herramienta para registrar **instantáneas identificables** del proyecto. Entre el archivo que editas y el commit que guardas existe una etapa intermedia: la **zona de preparación** (*staging area* o *index*).

```mermaid
flowchart LR
    A[Directorio de trabajo] -->|git add| B[Staging area]
    B -->|git commit| C[Repositorio local]
    C -->|git push| D[Repositorio remoto]
    D -->|git fetch| C
```

**Directorio de trabajo:** archivos visibles que editas. **Staging:** contenido seleccionado para el siguiente commit. **Repositorio local:** historial y referencias gestionados dentro de `.git`. **Remoto:** otro repositorio, que puede estar alojado en GitHub.

## 3.2. Estados de los archivos

- **Untracked:** Git ve el archivo, pero todavía no lo sigue.
- **Tracked, unmodified:** el archivo coincide con la versión registrada.
- **Modified:** el archivo seguido ha cambiado en el directorio de trabajo.
- **Staged:** se ha preparado una versión de sus cambios para el siguiente commit.

Un archivo puede tener **cambios preparados y otros cambios sin preparar al mismo tiempo**. Esto ocurre si ejecutas `git add`, vuelves a editar el archivo y consultas `git status`.

## 3.3. Experimento guiado: el mismo archivo en dos estados

En una carpeta nueva:

```bash
git init
```

Crea `notas.txt` con la línea `Primera idea`. Después:

```bash
git status
git add notas.txt
git status
```

Ahora modifica el archivo añadiendo `Segunda idea`, **sin ejecutar otro `git add`**. Consulta:

```bash
git status
git diff
git diff --staged
```

`git diff` muestra cambios no preparados; `git diff --staged` muestra los preparados. En el primer commit, la zona de preparación puede contener la versión con una sola línea, aunque el archivo del disco ya tenga dos.

!!! tip "Idea clave"
    `git commit` guarda lo que hay preparado, **no necesariamente todo lo que aparece en pantalla en el editor**.

## 3.4. ¿Qué contiene `.git`?

La carpeta `.git` contiene objetos del historial, referencias a ramas, configuración local e índice de preparación. No la edites manualmente ni la subas como una carpeta independiente dentro de otro repositorio. Si borras `.git`, los archivos de trabajo permanecen, pero desaparece el historial local de ese repositorio (salvo copias o remotos).

Git identifica objetos mediante hashes; el hash de un commit identifica una versión del historial, no simplemente un nombre de archivo.

## 3.5. Commits, ramas y HEAD

Un **commit** registra una instantánea del contenido preparado y metadatos como autor, fecha, mensaje y referencia a sus padres. Una **rama** es una referencia móvil a un commit. **HEAD** señala normalmente la rama activa.

```mermaid
flowchart LR
    A[Commit A] --> B[Commit B]
    B --> C[Commit C]
    C --- M[main y HEAD]
```

Al crear otro commit sobre `main`, la referencia avanza. Más adelante veremos cómo dos ramas pueden apuntar a commits distintos.

## 3.6. Git no es GitHub

Git realiza commits localmente sin Internet. GitHub aloja repositorios y añade herramientas de colaboración. Crear un repositorio local con `git init` **no lo publica**; hacer `git commit` **no lo sube**. Para intercambiar commits con un remoto se usan `fetch`, `pull` y `push`.

## 3.7. Cómo leer `git status`

```text
On branch main
Changes to be committed:
    modified: README.md
Changes not staged for commit:
    modified: App.java
Untracked files:
    notas.txt
```

Interpretación: `README.md` está preparado; `App.java` está modificado pero no preparado; `notas.txt` todavía no está bajo seguimiento. **No todos los archivos aparecerán en el próximo commit.**

## Actividades de comprensión

1. Explica con tus palabras la diferencia entre *working directory* y *staging area*.
2. ¿Qué ocurrirá si preparas un archivo, lo vuelves a editar y haces un commit sin repetir `git add`?
3. ¿Por qué `git status` es recomendable antes de cada commit?
4. Dibuja el recorrido de un cambio desde el editor hasta GitHub.

??? success "Soluciones orientativas"
    1. El directorio contiene los archivos editables; el staging contiene la versión seleccionada para el commit. 2. Se registra la versión preparada, no la última edición. 3. Permite detectar archivos olvidados o añadidos por error. 4. Editor → `git add` → staging → `git commit` → repositorio local → `git push` → remoto.

**Siguiente:** [Primer repositorio](04-primer-repositorio.md).
