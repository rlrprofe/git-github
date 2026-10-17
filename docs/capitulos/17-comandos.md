# 17. Guía rápida de comandos Git

Esta página es una **referencia de consulta**, no sustituye las explicaciones y actividades de los capítulos anteriores. Ejecuta cada comando en el repositorio correcto y revisa `git status` cuando tengas dudas.

## Configuración y diagnóstico

| Comando | Para qué sirve |
|---|---|
| `git --version` | Consultar versión instalada |
| `git config --global user.name "Nombre"` | Configurar autor global |
| `git config --global user.email "correo"` | Configurar correo global |
| `git config --list` | Consultar configuración |
| `git status` | Consultar el estado del repositorio |
| `git status -sb` | Resumen de rama y cambios |

## Crear y obtener repositorios

| Comando | Para qué sirve |
|---|---|
| `git init -b main` | Crear repositorio local |
| `git clone URL` | Clonar repositorio existente |
| `git remote -v` | Consultar remotos |
| `git remote add origin URL` | Añadir remoto |
| `git remote set-url origin URL` | Cambiar URL de remoto |

## Preparar y confirmar cambios

| Comando | Para qué sirve |
|---|---|
| `git add archivo` | Preparar un archivo |
| `git add .` | Preparar cambios bajo el directorio actual |
| `git diff` | Ver cambios sin preparar |
| `git diff --staged` | Ver cambios preparados |
| `git commit -m "Mensaje"` | Crear commit |
| `git commit --amend` | Sustituir el último commit (precaución si está publicado) |

## Historial y comparación

| Comando | Para qué sirve |
|---|---|
| `git log --oneline` | Historial resumido |
| `git log --graph --oneline --all` | Historial gráfico de referencias |
| `git show HEAD` | Consultar último commit |
| `git show --stat HEAD` | Resumen de archivos del commit |
| `git diff HEAD~1 HEAD` | Comparar dos commits consecutivos |
| `git blame archivo` | Ver último cambio de cada línea |

## Ramas y fusiones

| Comando | Para qué sirve |
|---|---|
| `git branch` | Listar ramas locales |
| `git switch -c feature/nombre` | Crear y activar rama |
| `git switch main` | Cambiar a `main` |
| `git merge feature/nombre` | Integrar una rama en la actual |
| `git merge --abort` | Cancelar un merge en curso |
| `git branch -d feature/nombre` | Borrar rama local integrada |

## Sincronización con GitHub

| Comando | Para qué sirve |
|---|---|
| `git fetch origin` | Descargar referencias sin integrar |
| `git pull` | Descargar e integrar según configuración |
| `git pull --ff-only` | Integrar solo si puede avanzar sin merge |
| `git push -u origin main` | Primera publicación y seguimiento |
| `git push` | Publicar cambios en remoto configurado |
| `git push -u origin feature/nombre` | Publicar rama de trabajo |

## Recuperación y precauciones

| Comando | Para qué sirve |
|---|---|
| `git restore --staged archivo` | Sacar archivo de staging sin descartar ediciones |
| `git restore archivo` | Descartar cambios no preparados del archivo |
| `git revert HEAD` | Crear commit que revierte otro |
| `git stash push -m "Mensaje"` | Guardar temporalmente cambios seguidos |
| `git stash pop` | Recuperar cambios guardados |
| `git reflog` | Consultar movimientos locales de referencias |
| `git clean -nd` | Simular limpieza de archivos sin seguimiento |

!!! danger "Comandos que requieren especial atención"
    `git reset --hard`, `git clean -fd`, `git push --force` y `git branch -D` pueden causar pérdida de trabajo o reescribir referencias. No los utilices como recetas rápidas ante un error.

## Flujo diario recomendado

```bash
git status
git pull --ff-only           # cuando corresponda y la rama siga el remoto
# Editar archivos y ejecutar pruebas
git diff
git add ruta/al/archivo
git diff --staged
git commit -m "Describir cambio concreto"
git push
```

Si `pull --ff-only` se rechaza, examina la divergencia antes de decidir una integración. Para tareas de equipo, desarrolla en una rama y abre una PR.

## Actividad de consulta

Sin mirar los capítulos anteriores, identifica qué comando usarías para: revisar un archivo antes del commit; crear una rama; obtener novedades sin fusionarlas; deshacer un commit ya compartido; y comprobar qué cambios están preparados.

??? success "Solución"
    `git diff` / `git diff --staged`; `git switch -c`; `git fetch`; `git revert`; `git diff --staged`.

**Siguiente:** [Proyecto práctico integrador](18-proyecto.md).
