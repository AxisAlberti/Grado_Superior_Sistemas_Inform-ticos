# Índice: Uso de la Terminal y Gestión de Directorios/Archivos en Linux

## 1. Introducción a la terminal
- 1.1 ¿Qué es la terminal y por qué usarla?
- 1.2 Tipos de terminales y emuladores populares
- 1.3 Acceso y navegación inicial
- 1.4 Opciones avanzadas de comandos básicos  
- 1.5 Manipulación de archivos y directorios  
- 1.6 Redirecciones y canalizaciones

## 2. Estructura del sistema de archivos en Linux
- 2.1 Jerarquía y directorios principales
- 2.2 El sistema de archivos: rutas absolutas y relativas
- 2.3 Comando `ls` y visualización de directorios

## 3. Navegación entre directorios
- 3.1 Uso de `pwd` para conocer la ruta actual
- 3.2 Cambio de directorio con `cd`
- 3.3 Atajos para navegar (directorios padre, inicio, etc.)

## 4. Creación y gestión de archivos y carpetas
- 4.1 Crear archivos: `touch`
- 4.2 Crear directorios: `mkdir`
- 4.3 Copiar archivos y carpetas: `cp`
- 4.4 Mover y renombrar: `mv`
- 4.5 Eliminar archivos y carpetas: `rm`, `rmdir`
- 4.6 Uso de comodines y globbing (`*`, `?`, etc.)

## 5. Visualización y edición básica de archivos
- 5.1 Comandos para mostrar contenido (`cat`, `less`, `more`)
- 5.2 Edición rápida con `nano` y consulta con `head`/`tail`
- 5.3 Visualización de archivos ocultos

## 6. Permisos y propietarios
- 6.1 Permisos básicos: lectura, escritura, ejecución
- 6.2 Cambiar permisos: `chmod`
- 6.3 Cambiar propietario y grupo: `chown`, `chgrp`
- 6.4 Comando `stat` para detalles avanzados

## 7. Búsqueda y gestión avanzada
- 7.1 Buscar archivos y carpetas: `find`, `locate`
- 7.2 Buscar contenido de archivos: `grep`
- 7.3 Compresión y descompresión: `tar`, `gzip`, `zip`, `unzip`

## 8. Buenas prácticas y seguridad en la gestión de archivos
- 8.1 Prevención del borrado y backups básicos
- 8.2 Comandos peligrosos y cómo evitar errores graves

## 9. Gestión de software y repositorios
- 9.1 ¿Qué son los repositorios de software?
- 9.2 Añadir, listar y actualizar repositorios (`apt`, `dnf`, `yum`, `zypper`)
- 9.3 Instalación y desinstalación de paquetes (`apt install`, `apt remove`, `dnf install`, `yum install`, `zypper install`)
- 9.4 Actualización de paquetes y del sistema (`apt update`, `apt upgrade`, `dnf upgrade`)
- 9.5 Búsqueda de paquetes disponibles (`apt search`, `dnf search`, `yum search`)
- 9.6 Comandos para consultar información de paquetes (`apt show`, `dnf info`, `yum info`)

---

*Actualizado octubre 2025*

## 1.1 ¿Qué es la terminal y por qué usarla?

La **terminal**, también llamada **consola** o **línea de comandos**, es una herramienta que permite al usuario comunicarse directamente con el sistema operativo escribiendo comandos en texto.  
A diferencia de las interfaces gráficas, la terminal ofrece **mayor control, velocidad y automatización**.

En los entornos de desarrollo profesional, dominar la terminal es fundamental. La mayoría de los frameworks, herramientas de despliegue, sistemas de control de versiones (como Git) y entornos virtuales dependen de ella.

### Ventajas principales

- **Eficiencia:** las tareas se ejecutan más rápido que mediante interfaces gráficas.  
- **Automatización:** permite crear scripts que realizan operaciones complejas sin intervención manual.  
- **Control total:** el usuario puede acceder a configuraciones del sistema y ejecutar herramientas no disponibles desde el entorno gráfico.  
- **Trabajo remoto:** es el medio estándar para administrar servidores o proyectos alojados en la nube mediante SSH.  
- **Integración con herramientas de desarrollo:** la mayoría de los entornos de trabajo para DAW (Node.js, Laravel, Git, Docker, etc.) requieren uso frecuente de la terminal.

### Ejemplo práctico

Para crear un proyecto Node.js desde la terminal:

```bash
mkdir mi_proyecto
cd mi_proyecto
npm init -y
```

Este conjunto de comandos crea un directorio, accede a él y genera el archivo `package.json` del proyecto.

---

## 1.2 Tipos de terminales y emuladores populares

En sistemas Linux existen distintos tipos de terminales y emuladores que proporcionan acceso al shell.

### Terminales de texto (TTY)

Son las **consolas virtuales** del sistema, accesibles normalmente con las combinaciones de teclas `Ctrl + Alt + F1` a `Ctrl + Alt + F6`.  
Funcionan incluso sin entorno gráfico, por lo que son esenciales en tareas de mantenimiento o recuperación del sistema.

Para volver al entorno gráfico, suele usarse `Ctrl + Alt + F7` o `Ctrl + Alt + F1`, según la distribución.

### Emuladores de terminal

Son aplicaciones gráficas que simulan una terminal de texto dentro del entorno de escritorio.  
Permiten ejecutar el shell de manera integrada en la interfaz visual del sistema.

**Ejemplos de emuladores comunes:**
- GNOME Terminal (`gnome-terminal`)
- Konsole (KDE)
- XTerm
- Tilix
- Alacritty
- Terminator

Cada emulador puede configurarse con distintos temas, fuentes, colores y comportamientos de pestañas o paneles divididos.

### Terminales en otros sistemas operativos

- **Windows:** PowerShell y Windows Terminal permiten acceder tanto al shell de Windows como a Bash a través del Subsistema de Linux (WSL).  
- **macOS:** incluye la aplicación Terminal y, en versiones recientes, también permite usar `zsh` como intérprete por defecto.

---

## 1.3 Acceso y navegación inicial

Cuando abrimos una terminal, aparece un texto similar a:

```
usuario@equipo:~$
```

Este es el **prompt**, el indicador de que el sistema está esperando un comando.

Significado de sus partes:
- `usuario`: nombre del usuario actual.
- `equipo`: nombre del host o máquina.
- `~`: representa el directorio personal del usuario (`/home/usuario`).
- `$`: símbolo que indica que no se está en modo administrador (root). Si aparece `#`, significa que el usuario tiene privilegios de superusuario.

### Comandos básicos de navegación

| Comando | Descripción | Ejemplo |
|----------|--------------|---------|
| `pwd` | Muestra la ruta completa del directorio actual | `pwd` → `/home/alumno` |
| `ls` | Lista archivos y carpetas del directorio actual | `ls -lha` |
| `cd` | Cambia de directorio | `cd Documentos` |
| `cd ..` | Retrocede al directorio padre |  |
| `cd -` | Vuelve al directorio anterior |  |
| `clear` | Limpia el contenido de la pantalla |  |

### Opciones avanzadas del comando `ls`

El comando `ls` dispone de múltiples opciones que amplían su utilidad. Algunas de las más usadas son:

| Opción | Descripción | Ejemplo |
|---------|--------------|---------|
| `-a` | Muestra **todos los archivos**, incluidos los ocultos (comienzan por punto `.`). | `ls -a` |
| `-l` | Muestra los archivos en **formato largo**, incluyendo permisos, propietario, tamaño y fecha. | `ls -l` |
| `-h` | Muestra tamaños en formato **legible por humanos** (K, M, G). | `ls -lh` |
| `-R` | Lista los archivos y subdirectorios de forma **recursiva**. Muestra toda la estructura de carpetas. | `ls -R` |
| `-t` | Ordena los resultados por **fecha de modificación**. | `ls -lt` |
| `-S` | Ordena los archivos por **tamaño**, del mayor al menor. | `ls -lS` |
| `--color` | Colorea los archivos según su tipo (opción activada por defecto en la mayoría de sistemas). | `ls --color=auto` |

#### Ejemplo de uso combinado

```bash
ls -lhaR /etc
```

Este comando:
- muestra todos los archivos (`-a`),
- en formato detallado (`-l`),
- con tamaños legibles (`-h`),
- y recorre recursivamente todas las subcarpetas (`-R`).

El resultado será una vista completa y detallada del contenido del directorio `/etc` y todos sus subdirectorios.

### Otros comandos de navegación útiles

| Comando | Función | Ejemplo |
|----------|----------|---------|
| `tree` | Muestra una vista jerárquica del sistema de archivos. | `tree /home/alumno` |
| `du -sh` | Muestra el tamaño total de un directorio. | `du -sh /var/www` |
| `df -h` | Muestra el uso del espacio en disco. | `df -h` |

### Ejemplo práctico de sesión inicial

```bash
pwd
# Resultado: /home/alumno

ls -lha
# Muestra el contenido completo, incluidos archivos ocultos

cd Descargas
pwd
# Resultado: /home/alumno/Descargas

ls -R
# Lista el contenido de Descargas y todas sus subcarpetas

cd ..
pwd
# Resultado: /home/alumno
```

