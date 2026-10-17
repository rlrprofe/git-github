# 16. Problemas frecuentes y diagnóstico

## 16.1. Antes de probar soluciones

Cuando Git muestra un error, **no encadenes comandos a ciegas**. Comprueba dónde estás, el estado de la rama y los remotos:

```bash
git status
git branch -vv
git remote -v
git log --oneline --graph --decorate --all -12
```

Los mensajes de error suelen indicar qué operación está bloqueada. Anota el comando que falló y la salida completa antes de modificar el repositorio.

## 16.2. `fatal: not a git repository`

Estás fuera de un repositorio o la carpeta `.git` no existe. Comprueba la ruta con `pwd` (Bash) o `Get-Location` (PowerShell). No ejecutes `git init` automáticamente: podrías crear un repositorio nuevo dentro de otro proyecto por error.

## 16.3. `nothing to commit, working tree clean`

No es un error: significa que no hay cambios pendientes en el directorio de trabajo ni en staging. Si esperabas modificaciones, comprueba si guardaste el archivo, si estás en la carpeta correcta y si está ignorado.

## 16.4. `non-fast-forward` o `fetch first`

La rama remota tiene commits que tu rama no integra. Primero:

```bash
git fetch origin
git log --oneline --graph --decorate --all
```

Después decide cómo integrar los cambios (`merge` o `rebase`) según el historial y los acuerdos del equipo. **No utilices `git push --force` como primera solución**: puede sobrescribir referencias remotas y dificultar la recuperación del trabajo ajeno.

## 16.5. `You have unmerged files`

Hay una fusión o integración sin resolver. Ejecuta `git status`, abre los archivos conflictivos, elimina marcadores tras decidir el contenido correcto y finaliza la operación. Si estabas realizando un merge y quieres cancelarlo:

```bash
git merge --abort
```

Si estabas realizando un rebase, la cancelación correspondiente es `git rebase --abort`. No intercambies ambos comandos.

## 16.6. `Authentication failed` o `Permission denied`

Revisa el método de autenticación (HTTPS o SSH), la cuenta conectada, la URL del remoto y tus permisos sobre el repositorio. `git config user.email` no autentica al usuario. Evita copiar tokens en la terminal si pueden quedar registrados en el historial.

## 16.7. Archivo ignorado que quiero versionar

```bash
git check-ignore -v ruta/al/archivo
```

Comprueba qué regla de `.gitignore` está afectando al archivo. Modifica la regla si es necesario. No fuerces la inclusión de archivos sensibles o compilados sin comprender por qué estaban ignorados.

## 16.8. Cambié de rama y desaparecieron mis modificaciones

Primero comprueba `git status`, `git branch` y `git log`. Es normal que los archivos del directorio de trabajo reflejen la rama activa. Si hiciste commits, normalmente podrás encontrarlos en su rama. Si utilizaste `stash`, consulta `git stash list`. No confundas cambiar de versión con borrar el proyecto.

## 16.9. Archivos con finales de línea cambiados

Si aparecen diferencias masivas al trabajar entre Windows y Linux, revisa `.gitattributes` y `core.autocrlf`. Evita registrar una renormalización accidental junto con cambios funcionales: dificultaría la revisión.

## 16.10. Mi web MkDocs no cambia aunque hice commit

`git commit` guarda localmente; `git push` publica fuentes en GitHub; **GitHub Pages necesita además un despliegue**. En un sitio con `mkdocs gh-deploy`, se publica la salida HTML en la rama `gh-pages`, y Pages debe estar configurado para servirla. Comprueba que la compilación termina sin errores y que la rama seleccionada en Pages es la correcta.

## Protocolo de diagnóstico para clase

1. Copia el mensaje de error exacto.
2. Anota el último comando ejecutado.
3. Ejecuta `git status`.
4. Comprueba rama y remoto si el error afecta a sincronización.
5. Identifica si hay riesgo de perder cambios antes de ejecutar `restore`, `reset`, `clean` o `force`.

??? question "Caso de autoevaluación"
    Un compañero ejecuta `git push`, recibe `non-fast-forward` y propone `git push --force`. ¿Qué le responderías?

??? success "Respuesta"
    Primero hay que descargar y examinar el historial remoto con `git fetch` y `git log --all --graph`. Solo después se decide cómo integrar las diferencias. Forzar el push sin comprender la situación puede sobrescribir el trabajo remoto.

**Siguiente:** [Guía rápida de comandos](17-comandos.md).
