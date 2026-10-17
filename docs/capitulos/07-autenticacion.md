# 7. Autenticación y seguridad con GitHub

## 7.1. Identidad de autor y autenticación son cosas distintas

`user.name` y `user.email` identifican el autor de un commit; **no conceden acceso a GitHub**. Para leer repositorios públicos normalmente no necesitas autenticarte; para publicar cambios en repositorios protegidos debes demostrar tu identidad y tener permisos.

## 7.2. HTTPS y gestores de credenciales

La URL HTTPS de un remoto tiene este formato:

```text
https://github.com/USUARIO/REPOSITORIO.git
```

En Windows, Git suele integrarse con **Git Credential Manager** para abrir un proceso de autenticación en el navegador y guardar credenciales de forma segura. Comprueba qué ayudante tienes configurado:

```bash
git config --show-origin --get credential.helper
```

No introduzcas la contraseña de tu cuenta como si fuera la contraseña del repositorio: GitHub no admite contraseñas de cuenta para autenticar operaciones Git por HTTPS. El método disponible depende de la configuración del equipo y la cuenta.

## 7.3. Tokens de acceso personal (PAT)

Un token es una credencial con permisos específicos. Si tu flujo requiere uno, créalo desde la configuración de GitHub y concede **solo los permisos y el alcance necesarios**. Establece caducidad cuando corresponda y revócalo si sospechas exposición.

!!! danger "Nunca publiques credenciales"
    No escribas tokens en archivos `.java`, `.env` versionados, capturas de pantalla, mensajes de foro ni comandos que puedan quedar guardados en el historial de terminal. No incluyas tokens en la URL remota.

## 7.4. Autenticación mediante SSH

SSH utiliza un par de claves: **privada**, que permanece en tu equipo, y **pública**, que registras en GitHub.

```bash
ssh-keygen -t ed25519 -C "correo@example.com"
```

Sigue las indicaciones de la terminal y protege la clave privada con una frase de paso. La ruta habitual es `~/.ssh/id_ed25519` (en Windows se encuentra bajo el directorio personal). Para mostrar la **clave pública**:

=== "PowerShell"

    ```powershell
    Get-Content "$HOME/.ssh/id_ed25519.pub"
    ```

=== "Bash"

    ```bash
    cat ~/.ssh/id_ed25519.pub
    ```

Añade ese contenido en GitHub, en **Settings → SSH and GPG keys**. Nunca copies el archivo sin extensión `.pub` a un servicio web: es la clave privada.

Comprueba la conexión:

```bash
ssh -T git@github.com
```

Es normal que GitHub indique que no proporciona acceso a una shell. Para usar SSH en un repositorio:

```bash
git remote set-url origin git@github.com:USUARIO/REPOSITORIO.git
```

## 7.5. Permisos y seguridad en equipos compartidos

En ordenadores de aula, evita guardar credenciales de forma persistente si no controlas el perfil de usuario. Cierra las sesiones al terminar y revisa qué cuentas están conectadas en el navegador y VS Code. No compartas una cuenta de GitHub entre varios estudiantes.

## 7.6. Errores habituales

| Mensaje | Qué revisar |
|---|---|
| `Authentication failed` | Método de autenticación y credenciales guardadas |
| `Permission denied (publickey)` | Clave SSH, agente, cuenta y URL remota |
| `Repository not found` | URL, visibilidad y permisos de la cuenta |
| `403` | Permisos insuficientes, restricciones de organización o credencial incorrecta |

## Actividades

1. Explica por qué configurar `user.email` no significa haber iniciado sesión en GitHub.
2. Compara HTTPS y SSH: ventajas, inconvenientes y uso en equipos compartidos.
3. Localiza en la documentación oficial cómo revocar un token comprometido.
4. Comprueba la URL de tu remoto con `git remote -v` sin mostrar credenciales.

**Documentación:** [Autenticación de GitHub](https://docs.github.com/es/authentication) · [Conexión mediante SSH](https://docs.github.com/es/authentication/connecting-to-github-with-ssh).

**Siguiente:** [Ramas](08-ramas.md).
