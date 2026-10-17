# 4. Primer repositorio

!!! note "Capítulo en desarrollo"
    Este archivo contiene el esquema didáctico inicial. Se ampliará con explicaciones detalladas, ejemplos de terminal, capturas, actividades y soluciones.

## Objetivos de aprendizaje

Al finalizar este capítulo, el alumnado deberá comprender y aplicar los conceptos y procedimientos indicados a continuación.

## Contenidos previstos

Crear carpeta; `git init`; `git status`; `git add`; `git commit`; `git log`; interpretar la salida de cada comando.

## Práctica inicial

Crea un repositorio con un README, realiza dos commits y consulta el historial.

## Comprobación del aprendizaje

- Explica qué has hecho y por qué.
- Conserva las evidencias relevantes de los comandos utilizados.
- Anota cualquier error encontrado y cómo lo has resuelto.

## Primer ejemplo reproducible

Abre una terminal en una carpeta nueva y ejecuta los comandos de uno en uno:

```bash
mkdir practica-git
cd practica-git
git init
git status
```

Crea un archivo `README.md` con el título de tu proyecto y continúa:

```bash
git add README.md
git commit -m "Añadir README inicial"
git log --oneline
```

!!! warning "Antes de realizar el commit"
    Comprueba que has configurado tu nombre y correo con `git config --global user.name` y `git config --global user.email`.
