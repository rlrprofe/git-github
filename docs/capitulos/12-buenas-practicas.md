# 12. Buenas prácticas y organización de repositorios

## 12.1. Qué debe contener un repositorio

Un repositorio profesional incluye **código fuente, documentación, pruebas y configuración reproducible**, pero normalmente excluye resultados compilados, archivos temporales, credenciales y preferencias personales del editor.

Ejemplo Java/Maven:

```text
inventario/
├── README.md
├── .gitignore
├── .gitattributes
├── pom.xml
└── src/
    ├── main/java/
    └── test/java/
```

## 12.2. `.gitignore`: qué ignorar y por qué

Un ejemplo razonable para Java/Maven y VS Code:

```gitignore
# Salidas de compilación
/target/
*.class

# Archivos locales del sistema
.DS_Store
Thumbs.db

# Preferencias locales del editor
.vscode/
.idea/
*.iml

# Configuración privada
.env
.env.*
!.env.example
```

**Precaución:** algunos equipos sí versionan configuraciones compartidas de `.vscode/` o del IDE; acuerda la política antes de ignorarlas. `gitignore` no elimina archivos que ya estaban bajo seguimiento.

Si añadiste por error un archivo generado:

```bash
git rm --cached archivo-generado.log
```

Esto lo retira del seguimiento en el próximo commit, **sin borrar la copia de trabajo**. Si contenía un secreto, además debes revocar la credencial y valorar la limpieza del historial.

## 12.3. README útil para otro desarrollador

Un buen `README.md` responde:

1. ¿Qué hace el proyecto?
2. ¿Qué requisitos necesita (JDK, Maven, base de datos)?
3. ¿Cómo se instala y ejecuta?
4. ¿Cómo se prueban los cambios?
5. ¿Qué estructura tiene y dónde están las instrucciones adicionales?

Ejemplo de contenido recomendado:

```text
# Inventario
Aplicación Java de consola para gestionar productos.

Requisitos: JDK 21 y Maven 3.9 o compatible.
Comprobación: mvn test
Compilación: mvn package
```

En el README real utiliza encabezados Markdown y bloques de código para los comandos. Añade las instrucciones de ejecución concretas de tu aplicación.

## 12.4. Commits pequeños y coherentes

Evita registrar varias funcionalidades sin relación en un mismo commit. Mensajes recomendados:

```text
Añadir validación de stock
Corregir lectura de productos CSV
Documentar configuración de Maven
```

Antes de confirmar, revisa `git diff --staged` y asegúrate de que el proyecto compila o pasa las pruebas pertinentes.

## 12.5. Normalización de finales de línea

En equipos mixtos Windows/Linux, `.gitattributes` ayuda a evitar cambios aparentes causados por CRLF y LF:

```gitattributes
* text=auto
*.sh text eol=lf
*.bat text eol=crlf
```

Establece esta política al principio del proyecto y comunícala al equipo. Cambiarla en un repositorio existente puede requerir una renormalización controlada.

## 12.6. Versiones y etiquetas

Una etiqueta (*tag*) marca un punto relevante del historial, por ejemplo una entrega:

```bash
git tag -a v1.0.0 -m "Primera entrega estable"
git push origin v1.0.0
```

Las etiquetas son distintas de las ramas: normalmente se utilizan para identificar versiones publicadas, no para seguir desarrollando.

## 12.7. Seguridad y privacidad

Nunca subas contraseñas, tokens, claves privadas, bases de datos reales con información personal ni archivos con datos del alumnado. Usa ejemplos ficticios y variables de entorno cuando sea apropiado. **Un repositorio privado no sustituye las buenas prácticas de seguridad.**

## Actividad de auditoría

Revisa un proyecto Java propio: identifica archivos fuente, salidas de compilación, configuraciones locales, documentación y posibles secretos. Prepara `.gitignore`, mejora el README y justifica qué archivos deben versionarse.

??? success "Criterios de evaluación"
    Se espera un repositorio reproducible, sin salidas de compilación innecesarias ni secretos, con README que permita a otra persona preparar y ejecutar el proyecto.

**Siguiente:** [Git desde Visual Studio Code](13-vscode.md).
