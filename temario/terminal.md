# Índice: Uso de la Terminal y Gestión de Directorios/Archivos en Linux

## 1. Introducción a la terminal
- 1.1 ¿Qué es la terminal y por qué usarla?
- 1.2 Tipos de terminales y emuladores populares
- 1.3 Acceso y navegación inicial

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

# 1. Introducción a la Terminal

## 1.1 ¿Qué es la terminal y por qué usarla?

La **terminal** (o consola) es una aplicación que permite interactuar con el sistema operativo utilizando texto y comandos en lugar de ventanas y menús gráficos. Es una herramienta fundamental para usuarios avanzados, programadores y administradores de sistemas, que buscan eficiencia, automatización y acceso a opciones potentes.

**Ventajas principales de la terminal:**
- **Automatización:** Permite ejecutar scripts para automatizar tareas rutinarias y complejas.
- **Velocidad y eficiencia:** El trabajo por comandos suele ser más rápido y requiere menos recursos que hacerlo gráficamente.
- **Flexibilidad:** Da acceso a funciones que no suelen estar disponibles desde la interfaz gráfica.
- **Control total:** Los comandos ofrecen un mayor control sobre el sistema y sus configuraciones.
- **Uso profesional:** Es indispensable en servidores, desarrollo de aplicaciones y administración avanzada de sistemas.

**Ejemplo práctico:**
Si quieres copiar todos los archivos de texto (`.txt`) de una carpeta a otra, puedes escribir:

cp *.txt /home/usuario/backup/

Esto copiará todos los archivos `.txt` del directorio actual al directorio `backup` de tu usuario.

---

## 1.2 Tipos de terminales y emuladores populares

En sistemas Linux podemos encontrar dos tipos principales de terminales:

- **Terminales físicas (TTY):**
  - Son consolas virtuales del sistema que se acceden pulsando `Ctrl+Alt+F1` hasta `Ctrl+Alt+F6`.
  - Se utilizan generalmente para administración directa, recuperaciones, o cuando el entorno gráfico no está disponible.

- **Emuladores de terminal gráficos:**
  - Permiten usar la consola dentro del entorno de escritorio, combinando potencia y comodidad.
  - Algunos de los emuladores más populares:
    - GNOME Terminal (`gnome-terminal`)
    - Konsole (KDE)
    - XTerm
    - Terminator
    - Tilix
    - Alacritty

**Ejemplo práctico:**
Para abrir una terminal gráfica, busca el icono en el menú de aplicaciones o pulsa `Ctrl+Alt+T` en la mayoría de escritorios Linux.

---

## 1.3 Acceso y navegación inicial

Cuando abres la terminal, el sistema te muestra un *prompt* (habitualmente algo como `usuario@equipo:~$`) que indica que está esperando un comando. Por defecto, se inicia en la carpeta personal del usuario.

### Comandos básicos de navegación

- **Ver la ruta actual:**

    ```
    pwd
    ```
    El comando muestra la ruta completa del directorio donde estás. Ejemplo de salida:
    ```
    /home/alumno
    ```

- **Listar archivos y carpetas en tu ubicación actual:**

    ```
    ls
    ```
    Muestra todos los archivos y carpetas disponibles en ese directorio.

- **Entrar en una carpeta:**

    ```
    cd Documentos
    ```
    Te moverás a la carpeta `Documentos` (debe existir dentro de tu ubicación actual).

- **Retroceder al directorio padre:**

    ```
    cd ..
    ```
    El comando `cd ..` permite subir un nivel en la jerarquía de directorios (al directorio padre).

### Ejemplo práctico paso a paso

1. **Abre la terminal** desde el menú o con `Ctrl+Alt+T`.
2. **Escribe** `pwd` y observa la ruta que aparece.
3. **Escribe** `ls` para ver el contenido del directorio actual.
4. **Navega** a la carpeta Descargas con:
    ```
    cd Descargas
    ```
5. **Confirma dónde estás** escribiendo nuevamente `pwd`.
6. **Retrocede** al directorio padre ejecutando:
    ```
    cd ..
    ```
    Así vuelves al directorio que contiene `Descargas` (normalmente tu carpeta personal si partiste de ahí).



