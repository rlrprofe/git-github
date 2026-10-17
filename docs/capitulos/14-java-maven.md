# 14. Git aplicado a proyectos Java y Maven

## 14.1. Qué aporta Git a un proyecto Java

En un proyecto Java no basta con guardar `.java`: también necesitamos registrar cómo compilar, ejecutar y probar el código. Maven facilita la estructura y la gestión de dependencias; Git registra la evolución de **fuentes y configuración**, no de los resultados compilados.

## 14.2. Estructura típica de Maven

```text
inventario/
├── pom.xml
├── README.md
├── .gitignore
├── src/
│   ├── main/java/es/ejemplo/App.java
│   └── test/java/es/ejemplo/AppTest.java
└── target/                # generado: no versionar
```

`pom.xml` describe el proyecto y sus dependencias; `src/main/java` contiene código de aplicación; `src/test/java`, pruebas; `target/` se genera al compilar y debe ignorarse normalmente.

## 14.3. Configurar `.gitignore`

```gitignore
/target/
*.class
*.log
.idea/
*.iml
.vscode/
.env
```

Adapta el archivo a las herramientas del equipo. Comprueba que `target/` no aparece entre los archivos preparados:

```bash
git status --short
git check-ignore -v target/ejemplo.class
```

`git check-ignore` permite identificar qué regla ignora una ruta. Si el archivo ya estaba versionado, una nueva regla no lo retira automáticamente del seguimiento.

## 14.4. Primer ciclo de trabajo

```bash
git init -b main
git add pom.xml src README.md .gitignore
git diff --staged
git commit -m "Crear proyecto Maven inicial"
```

Antes de registrar una funcionalidad, comprueba que el proyecto funciona:

```bash
mvn test
mvn package
```

Estos comandos requieren Maven y un JDK compatible instalados. No registres `target/` después de compilar.

## 14.5. Trabajar por funcionalidades

Supón que vas a añadir validación de stock:

```bash
git switch -c feature/validar-stock
# Edita el código y las pruebas
mvn test
git add src
git commit -m "Validar stock no negativo"
```

Cuando termines, publica la rama y abre una PR si el equipo utiliza revisión. Un cambio pequeño y acompañado de pruebas es más fácil de revisar que una modificación extensa y sin comprobaciones.

## 14.6. Dependencias y reproducibilidad

En general se versiona `pom.xml` porque permite declarar dependencias y plugins. No se versiona el repositorio local de dependencias (`~/.m2/repository`). Si el proyecto incluye **Maven Wrapper**, suele versionarse su configuración y los archivos necesarios para ejecutar la versión indicada, revisando su procedencia.

No incluyas credenciales de repositorios privados en `pom.xml`; utiliza mecanismos de configuración local o secretos gestionados de forma segura.

## 14.7. README para una entrega académica

Incluye el objetivo, requisitos (por ejemplo JDK 21), comandos de compilación, instrucciones de ejecución, estructura del proyecto, pruebas y, si procede, capturas y limitaciones conocidas. Un profesor o compañero debería poder reproducir el proyecto sin tener que preguntarte cómo arrancarlo.

## Actividad integradora

Crea o reutiliza un proyecto Maven pequeño. Registra la estructura inicial, añade una funcionalidad en una rama, ejecuta pruebas, documenta la ejecución y prepara una PR. Entrega el enlace al repositorio y al historial de commits.

??? success "Comprobación"
    Debe poder clonarse y compilarse desde fuentes. `target/` no debe formar parte del historial ordinario. Los commits deben reflejar avances comprensibles.

**Siguiente:** [Flujos de trabajo profesionales](15-flujos.md).
