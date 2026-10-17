# 2. Instalación y configuración de Git

## 2.1. Qué necesitas antes de empezar

Para seguir la guía necesitas **Git**, una terminal y un editor. Git es independiente de GitHub: puedes trabajar localmente sin cuenta. Usaremos **PowerShell** en Windows y una terminal Bash en Linux. Los comandos de Git son prácticamente iguales; lo que cambia es la navegación por carpetas y la instalación.

!!! important "Instala Git, no solamente una extensión"
    El panel de control de versiones de VS Code necesita que Git esté instalado en el sistema. GitHub Desktop es opcional y no sustituye el aprendizaje de los comandos.

## 2.2. Instalación en Windows

1. Descarga Git desde [git-scm.com/downloads/win](https://git-scm.com/downloads/win).
2. Ejecuta el instalador. Para empezar, conserva las opciones predeterminadas; presta atención al editor predeterminado y a la integración de Git con la línea de comandos.
3. Abre **PowerShell** o **Git Bash** y comprueba:

```powershell
 git --version
```

La salida tendrá un formato parecido a `git version 2.x.y`. El número exacto depende de la versión instalada. Si PowerShell indica que no reconoce `git`, cierra y abre una terminal nueva; si continúa, revisa la instalación y el `PATH`.

## 2.3. Instalación en Linux (Ubuntu / Pop!_OS)

```bash
sudo apt update
sudo apt install git
 git --version
```

`sudo` solicita permisos de administración; `apt update` actualiza los índices de paquetes y `apt install` instala Git desde los repositorios de la distribución. En otras distribuciones cambia el gestor de paquetes.

## 2.4. Configurar la identidad de los commits

Git registra **autor** y **correo** en cada commit. No es lo mismo que iniciar sesión en GitHub.

```bash
git config --global user.name "Nombre Apellidos"
git config --global user.email "correo@example.com"
git config --global --list
```

Sustituye los valores de ejemplo por los tuyos. `--global` aplica la configuración a los repositorios de tu usuario. Si trabajas con dos identidades (personal y académica), puedes configurar una diferente **dentro de un repositorio**:

```bash
git config --local user.name "Nombre Académico"
git config --local user.email "correo-academico@example.com"
```

La configuración local tiene prioridad sobre la global. Comprueba el origen de los valores:

```bash
git config --show-origin --get user.email
```

!!! warning "Privacidad del correo"
    El correo de los commits puede ser visible al publicar el historial. GitHub ofrece direcciones `noreply` para quienes no desean exponer su correo personal. Configura esa dirección antes de crear commits si quieres utilizarla.

## 2.5. Editor y comportamiento de Git

Puedes configurar VS Code como editor para mensajes y operaciones que requieran edición:

```bash
git config --global core.editor "code --wait"
```

Esto requiere que el comando `code` esté disponible en la terminal. `--wait` hace que Git espere a que cierres el archivo editado. No es imprescindible para empezar: también puedes escribir mensajes con `git commit -m`.

Comprueba la configuración de final de línea:

```bash
git config --show-origin --get core.autocrlf
```

Windows suele utilizar CRLF y Linux LF. En proyectos compartidos conviene establecer una política mediante `.gitattributes` (lo estudiaremos en el capítulo 12), en lugar de cambiar opciones al azar.

## 2.6. Crear una carpeta de prácticas

=== "Windows (PowerShell)"

    ```powershell
    mkdir GitPracticas
    cd GitPracticas
    Get-Location
    ```

=== "Linux (Bash)"

    ```bash
    mkdir -p ~/GitPracticas
    cd ~/GitPracticas
    pwd
    ```

Los comandos `mkdir`, `cd` y `pwd`/`Get-Location` pertenecen a la terminal, **no a Git**. Comprender esta diferencia evita muchos errores de ruta.

## 2.7. Comprobaciones y problemas habituales

| Síntoma | Posible causa | Qué comprobar |
|---|---|---|
| `git` no se reconoce | Git no instalado o `PATH` sin actualizar | `git --version` en una terminal nueva |
| `Author identity unknown` | Falta nombre o correo | `git config --global --list` |
| `code` no se reconoce | VS Code no está en el `PATH` | Instalación o comando de VS Code |
| Permiso denegado | Carpeta protegida | Trabajar en una carpeta del usuario |

## Actividades

1. Comprueba la versión de Git y anótala.
2. Configura nombre y correo. Explica qué diferencia hay entre `--global` y `--local`.
3. Crea una carpeta de prácticas y abre su ubicación desde la terminal.
4. Investiga si el correo de un commit tiene que coincidir con el de acceso a GitHub.

??? success "Orientaciones de solución"
    `git --version` muestra la versión instalada. `--global` configura al usuario y `--local` solo al repositorio actual. Git no exige que el correo sea el de acceso a GitHub; para atribuir commits a tu cuenta, GitHub debe reconocer la dirección utilizada.

**Siguiente:** [Fundamentos de Git](03-fundamentos.md).
