# 10. Trabajo colaborativo con GitHub

## 10.1. Colaborar no es compartir una carpeta

Cuando varias personas desarrollan una aplicación, cada una puede tener su copia del repositorio, trabajar en ramas y proponer cambios. GitHub añade herramientas para discutir, revisar y aprobar esas propuestas antes de integrarlas.

## 10.2. Dos modelos de colaboración

**Repositorio compartido:** las personas colaboradoras tienen permisos para crear ramas en el mismo repositorio. **Fork:** una persona crea una copia del repositorio en su cuenta y propone cambios al proyecto original. En proyectos de clase con equipos pequeños suele ser más sencillo comenzar con un repositorio compartido.

| Concepto | Utilidad |
|---|---|
| Colaborador | Cuenta con permisos sobre el repositorio |
| Rama de funcionalidad | Aísla un cambio concreto |
| Pull request (PR) | Propone integrar una rama en otra |
| Revisión | Permite comentar y solicitar cambios |
| Issue | Registra tareas, defectos o propuestas |

## 10.3. Flujo de trabajo con pull request

1. Actualiza tu rama principal: `git switch main` y `git pull --ff-only` si la configuración permite avanzar sin fusionar.
2. Crea una rama: `git switch -c feature/validar-precio`.
3. Realiza cambios pequeños, comprueba su funcionamiento y crea commits.
4. Publica la rama: `git push -u origin feature/validar-precio`.
5. Abre una PR en GitHub de `feature/validar-precio` hacia `main`.
6. Explica qué cambia, cómo se ha probado y si hay limitaciones.
7. Atiende los comentarios y, cuando esté aprobada, integra la PR según las reglas del proyecto.

!!! tip "Una PR no es solo un botón"
    Es un espacio para explicar la intención del cambio, revisar el código y registrar decisiones. Una buena PR suele ser pequeña, coherente y fácil de comprobar.

## 10.4. Ejemplo de descripción de PR

```markdown
## Objetivo
Evitar que se registren productos con precio negativo.

## Cambios
- Validación en ProductoService.
- Mensaje de error en la consola.
- Prueba para precio negativo.

## Comprobación
- Ejecutadas las pruebas con `mvn test`.
- Verificada la opción de alta manualmente.
```

## 10.5. Issues y organización del trabajo

Un *issue* puede incluir un título, descripción, criterios de aceptación, etiquetas y una persona asignada. Ejemplo:

```text
Título: Validar que el stock no sea negativo
Criterios de aceptación:
- Rechazar cantidades menores que cero.
- Mostrar un mensaje comprensible.
- Incorporar una prueba del caso inválido.
```

Los issues permiten distribuir trabajo sin perder de vista el objetivo del equipo.

## 10.6. Revisiones y conflictos

Una revisión debe centrarse en el código y en criterios verificables, no en la persona. Si la rama principal cambia mientras trabajas, tendrás que actualizar tu rama y resolver los conflictos antes de integrar. No hagas `push --force` sobre ramas compartidas sin coordinarlo con el equipo.

## 10.7. Protección de ramas

GitHub permite establecer reglas sobre determinadas ramas, según las funciones disponibles en el repositorio y plan: exigir PR, revisiones o comprobaciones antes de integrar. Para un proyecto académico es útil acordar que nadie modifica `main` directamente sin revisión, incluso si no se activa una regla técnica.

## Actividad en parejas

Una persona crea un repositorio con `README.md` y concede acceso a otra. Cada estudiante crea una rama para modificar una sección distinta. Publican ramas, abren PR, revisan los cambios del compañero e integran ambas. Entregad los enlaces a las PR y una breve reflexión sobre la revisión.

??? success "Rúbrica orientativa"
    Se comprueba la existencia de ramas descriptivas, commits comprensibles, PR con explicación y evidencias de revisión. No basta con que el código final funcione: debe observarse el proceso colaborativo.

**Siguiente:** [Deshacer y recuperar cambios](11-recuperacion.md).
