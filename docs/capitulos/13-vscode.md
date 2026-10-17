# 13. Git desde Visual Studio Code

## 13.1. La interfaz gráfica y los comandos realizan operaciones equivalentes

VS Code incorpora una vista de **Control de código fuente** (*Source Control*) que permite consultar cambios, prepararlos, crear commits, cambiar de rama y sincronizar con remotos. Es útil, pero conviene entender primero qué comandos representa cada acción.

## 13.2. Preparación

1. Instala Git y comprueba `git --version` en una terminal.
2. Abre VS Code y selecciona **Archivo → Abrir carpeta**.
3. Abre una carpeta que ya contenga `.git` o inicializa el repositorio desde el panel de control de versiones.
4. Si no aparecen cambios, comprueba que abriste la **carpeta raíz** del repositorio.

No es necesario instalar una extensión adicional para las funciones básicas de Git.

## 13.3. Interpretar el panel Source Control

| Elemento visual | Significado habitual |
|---|---|
| Changes | Cambios no preparados |
| Staged Changes | Cambios preparados para commit |
| `M` | Archivo modificado |
| `U` | Archivo sin seguimiento, según vista/configuración |
| `+` junto a archivo | Preparar cambios (*stage*) |
| Commit | Registrar los cambios preparados |

Los nombres e iconos exactos pueden variar entre versiones y configuraciones de VS Code. La terminal integrada permite verificar cualquier operación con `git status`.

## 13.4. Primer commit desde VS Code

1. Abre `HolaGit`.
2. Modifica `README.md` y guarda.
3. En Source Control, abre la comparación para revisar qué líneas cambiaron.
4. Prepara el archivo con el botón `+`.
5. Escribe un mensaje descriptivo y confirma el commit.
6. Abre la terminal integrada y ejecuta `git log --oneline` para comprobarlo.

!!! tip "Aprender con dos vistas"
    Después de cada operación gráfica importante, consulta su equivalente en terminal. Esto ayuda a comprender qué ha ocurrido y facilita trabajar en equipos donde no haya interfaz gráfica.

## 13.5. Ramas y conflictos

El indicador de rama permite cambiar de rama o crear una nueva. Para fusionar, utiliza los comandos de la paleta (`Ctrl+Shift+P`) o la terminal. Ante un conflicto, VS Code puede mostrar opciones para aceptar cambios actuales, entrantes o combinar; **revisa siempre el resultado final** y ejecuta pruebas.

No confundas «aceptar ambos» con resolver correctamente la lógica del programa: puede producir código duplicado o contradictorio.

## 13.6. Sincronización con GitHub

VS Code puede mostrar acciones de *Publish Branch*, *Pull*, *Push* y *Sync Changes*. Algunas requieren autenticación con GitHub. **Sync** puede implicar tanto descargar como publicar: comprueba qué hará antes de pulsar.

Para verificar el remoto:

```bash
git remote -v
git status -sb
```

## 13.7. Extensiones opcionales

Herramientas como GitLens pueden facilitar la visualización de autores e historial, pero no son imprescindibles. Instala solo extensiones autorizadas en el aula y evita depender de funciones que no estarán disponibles en todos los equipos.

## Actividades

1. Realiza un commit completo desde el panel gráfico.
2. Repite el proceso desde la terminal integrada.
3. Crea una rama desde VS Code y comprueba su nombre con `git branch --show-current`.
4. Resuelve un conflicto de práctica y documenta qué opciones elegiste y por qué.

**Siguiente:** [Git en proyectos Java y Maven](14-java-maven.md).
