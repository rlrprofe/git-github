# 18. Proyecto práctico integrador: Git y GitHub de principio a fin

## 18.1. Enunciado

Vas a desarrollar y documentar un pequeño **gestor de tareas de consola en Java**. El objetivo principal **no es programar una aplicación compleja**, sino demostrar que sabes utilizar Git y GitHub para registrar, revisar, publicar, integrar y recuperar cambios. Puedes trabajar en pareja para las fases colaborativas.

### Resultados de aprendizaje de la práctica

Al finalizar deberás ser capaz de inicializar un repositorio, crear commits coherentes, configurar un remoto, utilizar ramas, abrir una PR, resolver un conflicto y documentar el proceso con evidencias verificables.

## 18.2. Punto de partida

Crea esta estructura:

```text
gestor-tareas/
├── README.md
├── .gitignore
└── src/
    └── GestorTareas.java
```

Contenido inicial de `src/GestorTareas.java`:

```java
public class GestorTareas {
    public static void main(String[] args) {
        System.out.println("GESTOR DE TAREAS");
        System.out.println("1. Mostrar tareas");
        System.out.println("0. Salir");
    }
}
```

Este código es deliberadamente sencillo. Más adelante puedes ampliarlo con `Scanner`, colecciones y métodos si ya conoces esos contenidos; **la evaluación de Git no depende de desarrollar todas esas funcionalidades**.

## 18.3. Fase A: repositorio e historial

1. Inicializa Git en `gestor-tareas` y utiliza la rama `main`.
2. Crea `.gitignore` para excluir `*.class` y archivos temporales.
3. Realiza un commit inicial con la estructura del proyecto.
4. Añade un segundo commit para documentar la compilación y ejecución.
5. Añade un tercer commit para mejorar el menú.

Comprueba con:

```bash
git status
git log --oneline --graph
```

**Evidencia:** captura o transcripción del historial con al menos tres commits coherentes.

## 18.4. Fase B: GitHub y sincronización

1. Crea un repositorio vacío en GitHub, sin README inicial.
2. Configura `origin` y publica `main`.
3. Modifica el README desde GitHub (por ejemplo, añade una sección de objetivos).
4. Ejecuta `git fetch origin` y explica qué diferencia existe entre `main` y `origin/main`.
5. Integra los cambios y comprueba que aparecen localmente.

**Evidencia:** enlace al repositorio y explicación de `fetch` frente a `pull`.

## 18.5. Fase C: desarrollo en una rama

```bash
git switch -c feature/mejorar-menu
```

Añade una opción al menú, registra el cambio con un commit descriptivo y publica la rama. Abre una PR hacia `main` que incluya objetivo, cambios y cómo se ha comprobado el funcionamiento.

**Evidencia:** enlace a la PR y captura del historial de ramas.

## 18.6. Fase D: conflicto controlado

Trabaja sobre una copia o rama de práctica. Crea dos ramas desde el mismo commit, cambia en ambas la línea del título de la aplicación con textos diferentes y confirma los cambios. Integra primero una rama en `main` y después la otra. Si Git detecta un conflicto:

1. Localiza el archivo con `git status`.
2. Examina ambas alternativas.
3. Edita el archivo y deja un título correcto.
4. Compila y ejecuta el programa.
5. Finaliza la fusión y comprueba el historial.

**Evidencia:** descripción del conflicto y del criterio utilizado para resolverlo; no es necesario publicar capturas con datos personales.

## 18.7. Fase E: recuperación

Modifica una línea de `README.md` sin preparar los cambios. Consulta `git diff` y restaura conscientemente el archivo. Después, en un archivo de práctica, prepara un cambio y retíralo del staging sin perder la edición. Explica por qué ambas operaciones son diferentes.

!!! warning "No destruyas tu entrega"
    Para practicar recuperación utiliza cambios desechables. No ejecutes `reset --hard` ni `push --force` sobre la entrega principal.

## 18.8. Entregables

1. **URL del repositorio** en GitHub con el código y README.
2. **Historial** con commits descriptivos y ramas utilizadas.
3. **Pull request** con descripción y revisión (si trabajas individualmente, documenta una PR propia de práctica).
4. **Informe breve** en Markdown o PDF: operaciones realizadas, diferencias entre comandos y resolución del conflicto.
5. **Evidencias** suficientes para verificar el proceso, sin contraseñas ni datos personales.

## 18.9. Rúbrica orientativa (100 puntos)

| Criterio | Puntos |
|---|---:|
| Repositorio correctamente organizado y `.gitignore` | 15 |
| Commits coherentes e historial comprensible | 20 |
| Remoto y sincronización explicados y realizados | 20 |
| Rama y pull request correctamente utilizadas | 20 |
| Conflicto y recuperación resueltos con criterio | 15 |
| README y documentación de evidencias | 10 |

## 18.10. Autoevaluación final

- ¿Puedo explicar la diferencia entre Git y GitHub sin consultar apuntes?
- ¿Sé qué contiene staging y qué guarda un commit?
- ¿Sé consultar el historial y comparar versiones?
- ¿Puedo crear una rama, publicar cambios y abrir una PR?
- ¿Sé detenerme y diagnosticar un conflicto sin perder trabajo?
- ¿He evitado publicar archivos generados y credenciales?

??? success "Qué debe demostrar una buena entrega"
    El repositorio no necesita una aplicación compleja, pero sí un historial que permita reconstruir cómo se ha trabajado. Los commits, ramas y PR deben evidenciar el proceso y la documentación debe explicar las decisiones tomadas.

**Has terminado el recorrido.** Utiliza la [guía rápida de comandos](17-comandos.md) como referencia cuando trabajes en tus proyectos.
