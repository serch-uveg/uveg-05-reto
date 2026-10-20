# Git: conceptos y comandos básicos

## ¿Qué es Git?

Git es un sistema de control de versiones distribuido. Permite registrar los cambios de un proyecto a lo largo del tiempo, consultar versiones anteriores y trabajar en paralelo sin que cada persona tenga que modificar directamente la misma versión.

Al ser distribuido, cada persona que clona un repositorio obtiene una copia completa de su historial. Por eso es posible consultar y guardar cambios localmente incluso sin conexión; para compartirlos con otras personas se sincronizan con un repositorio remoto.

## ¿Cómo funciona?

Al trabajar con Git, los archivos pasan por tres áreas principales:

1. **Directorio de trabajo:** los archivos del proyecto tal como están en tu equipo. Aquí editas y creas archivos.
2. **Área de preparación (staging):** selección de cambios que formarán parte del siguiente registro. Se agregan con `git add`.
3. **Repositorio local:** historial de cambios guardados como *commits*. Se crean con `git commit`.

Un *commit* es una fotografía del estado preparado del proyecto, acompañada de un identificador, autor, fecha y mensaje. Los commits suelen enlazarse para formar el historial del proyecto.

## Conceptos principales

- **Repositorio:** proyecto cuyos cambios e historial controla Git. Puede ser local o estar alojado en un servicio remoto.
- **Commit:** registro de un conjunto de cambios. Conviene que sea pequeño y tenga un mensaje claro.
- **Rama (branch):** línea de trabajo independiente. Permite desarrollar una función o corregir un error sin alterar inmediatamente la rama principal.
- **Fusión (merge):** integración de los cambios de una rama en otra. Si Git no puede combinar cambios automáticamente, se deben resolver los conflictos manualmente.
- **Repositorio remoto:** copia del repositorio disponible en otro lugar, normalmente en un servidor, para compartir y sincronizar el trabajo.
- **Clonar:** crear una copia local de un repositorio remoto, incluido su historial.
- **`origin`:** nombre remoto convencional que Git asigna al repositorio del que se clonó el proyecto.
- **`main`:** nombre habitual de la rama principal, aunque un repositorio puede usar otro nombre.

## Git y GitHub: ¿cuál es la diferencia?

**Git** es el programa que controla las versiones y puede usarse desde la terminal o mediante aplicaciones gráficas. **GitHub** es una plataforma web que aloja repositorios Git y ofrece herramientas para colaborar, como solicitudes de cambios (*pull requests*), revisiones, seguimiento de tareas y automatización.

Git puede utilizarse sin GitHub; también se pueden alojar repositorios Git en otros servicios o en servidores propios. GitHub, por su parte, utiliza Git para administrar el historial de los repositorios.

## Comandos básicos

### Configuración inicial

Configura el nombre y correo que aparecerán en tus commits. Normalmente se hace una sola vez por equipo:

```bash
git config --global user.name "Tu nombre"
git config --global user.email "tu-correo@ejemplo.com"
```

### Crear o descargar un repositorio

```bash
git init                    # Inicia un repositorio en la carpeta actual
git clone URL_DEL_REPO      # Descarga un repositorio remoto
```

### Revisar y guardar cambios

```bash
git status                  # Muestra archivos modificados y preparados
git diff                    # Muestra cambios aún no preparados
git add README.md           # Prepara un archivo específico
git add .                   # Prepara todos los cambios de la carpeta actual
git diff --staged           # Muestra los cambios preparados
git commit -m "Describe el cambio"  # Guarda los cambios preparados
git log --oneline           # Consulta el historial resumido
```

Antes de ejecutar `git add .`, revisa `git status` para evitar preparar archivos que no quieras incluir.

### Trabajar con ramas

```bash
git branch                  # Lista las ramas locales
git switch -c nueva-funcion # Crea una rama y cambia a ella
git switch main             # Cambia a la rama main
git merge nueva-funcion     # Integra esa rama en la rama actual
```

### Sincronizar con un remoto

```bash
git remote -v               # Muestra los repositorios remotos configurados
git pull                    # Descarga e integra cambios del remoto actual
git push -u origin main     # Publica main y establece su remoto de seguimiento
git push                    # Publica los commits posteriores
```

`git pull` integra cambios remotos en la rama actual. Es buena práctica revisar la rama y el estado con `git status` antes de sincronizar.

## Ejemplo de flujo de trabajo

Este ejemplo supone que el repositorio ya fue clonado y que existe la rama `main`:

```bash
# 1. Actualiza tu rama principal
git switch main
git pull

# 2. Crea una rama para una tarea
git switch -c docs/actualizar-readme

# 3. Edita archivos y revisa los cambios
git status
git diff

# 4. Prepara y registra el trabajo
git add README.md
git diff --staged
git commit -m "docs: explicar conceptos básicos de Git"

# 5. Publica la rama en GitHub
git push -u origin docs/actualizar-readme
```

Después de publicarla, puedes abrir una *pull request* en GitHub para revisar e integrar la rama en `main`. Si el proyecto no usa *pull requests*, cambia a `main`, actualízala y ejecuta `git merge docs/actualizar-readme` para integrar los cambios localmente; luego publica `main` con `git push`.