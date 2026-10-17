# Git y GitHub · Guía práctica de control de versiones

Sitio educativo independiente creado con MkDocs Material.

## Puesta en marcha

```powershell
python -m pip install -r requirements.txt
python -m mkdocs serve
```

Visita `http://127.0.0.1:8000/`.

## Publicación

1. Crea en GitHub el repositorio público `git-github` en la cuenta `rlrprofe`.
2. Abre una terminal en esta carpeta y ejecuta:

```powershell
git init
git add .
git commit -m "Crear estructura inicial de la guía Git y GitHub"
git branch -M main
git remote add origin https://github.com/rlrprofe/git-github.git
git push -u origin main
python -m mkdocs gh-deploy
```

3. En GitHub, revisa **Settings → Pages** y comprueba que se publica desde la rama `gh-pages` (raíz `/`).
4. Web prevista: https://rlrprofe.github.io/git-github/

El repositorio debe crearse primero; la dirección no estará activa hasta completar el despliegue.

## Estado del contenido

La estructura y la navegación están preparadas. Los capítulos contienen un guion editorial y puntos de partida; **no constituyen todavía la guía didáctica completa**.
