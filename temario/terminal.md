
- 


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

## 1.4 Opciones avanzadas de comandos básicos

En Linux, la mayoría de los comandos admiten **opciones** que modifican su comportamiento.  
Estas opciones se escriben precedidas por un guion (`-`) o dos (`--`) si son palabras completas.

A continuación, se presentan algunas de las más utilizadas en comandos esenciales.

### Comando `ls` – listar contenido de directorios

| Opción | Descripción | Ejemplo |
|---------|--------------|---------|
| `-a` | Muestra todos los archivos, incluidos los ocultos. | `ls -a` |
| `-l` | Formato largo: muestra permisos, propietario, tamaño y fecha. | `ls -l` |
| `-h` | Tamaños legibles (K, M, G). | `ls -lh` |
| `-R` | Listado recursivo de subdirectorios. | `ls -R` |
| `-t` | Ordena por fecha de modificación. | `ls -lt` |
| `-S` | Ordena por tamaño de archivo. | `ls -lS` |
| `--color=auto` | Muestra los archivos con colores según su tipo. | `ls --color=auto` |

Ejemplo combinado:

```bash
ls -lhaR /etc
```

Muestra todos los archivos (incluidos ocultos), en formato largo, con tamaños legibles y de forma recursiva.

---

### Comando `cd` – cambiar de directorio

| Opción | Descripción | Ejemplo |
|---------|--------------|---------|
| `cd` | Sin argumentos, lleva al directorio personal del usuario. | `cd` |
| `cd -` | Regresa al directorio anterior. | `cd -` |
| `cd ..` | Sube al directorio padre. | `cd ..` |

> **Consejo:** puedes usar rutas absolutas (`/var/www`) o relativas (`../imagenes`), dependiendo del contexto actual.

---

### Comando `cat` – mostrar contenido de archivos

| Opción | Descripción | Ejemplo |
|---------|--------------|---------|
| `-n` | Numera las líneas. | `cat -n texto.txt` |
| `-b` | Numera solo las líneas no vacías. | `cat -b texto.txt` |
| `-s` | Suprime líneas vacías repetidas. | `cat -s log.txt` |

---

### Comando `grep` – buscar texto dentro de archivos

| Opción | Descripción | Ejemplo |
|---------|--------------|---------|
| `-i` | Ignora mayúsculas y minúsculas. | `grep -i error log.txt` |
| `-r` | Búsqueda recursiva en subdirectorios. | `grep -r "function" src/` |
| `-n` | Muestra el número de línea donde se encontró la coincidencia. | `grep -n palabra texto.txt` |
| `--color=auto` | Resalta las coincidencias en color. | `grep --color=auto html index.html` |

---

### Comando `man` – manual de ayuda

| Opción | Descripción | Ejemplo |
|---------|--------------|---------|
| `man -k palabra` | Busca comandos relacionados con una palabra clave. | `man -k copy` |
| `man comando` | Muestra el manual completo del comando. | `man ls` |

---

## 1.5 Manipulación de archivos y directorios

Linux proporciona comandos muy potentes para crear, copiar, mover y eliminar archivos y carpetas.

### Creación de archivos y carpetas

| Comando | Descripción | Ejemplo |
|----------|--------------|---------|
| `touch` | Crea un archivo vacío o actualiza su fecha de modificación. | `touch index.html` |
| `mkdir` | Crea un directorio. | `mkdir proyecto` |
| `mkdir -p` | Crea directorios anidados. | `mkdir -p web/assets/css` |

---

### Copiar archivos o directorios

| Opción | Descripción | Ejemplo |
|---------|--------------|---------|
| `cp archivo destino` | Copia un archivo. | `cp index.html backup/` |
| `-r` o `-R` | Copia recursiva: incluye subdirectorios. | `cp -r img/ copia_img/` |
| `-i` | Solicita confirmación antes de sobrescribir. | `cp -i datos.txt backup/` |
| `-v` | Muestra los archivos mientras se copian (modo verbose). | `cp -v *.html /var/www/html/` |

---

### Mover o renombrar archivos

| Opción | Descripción | Ejemplo |
|---------|--------------|---------|
| `mv origen destino` | Mueve o renombra un archivo o carpeta. | `mv app.js js/app.js` |
| `-i` | Confirma antes de sobrescribir. | `mv -i index.html public/` |
| `-v` | Muestra los archivos movidos. | `mv -v *.txt backup/` |

---

### Eliminar archivos y carpetas

| Opción | Descripción | Ejemplo |
|---------|--------------|---------|
| `rm archivo` | Elimina un archivo. | `rm log.txt` |
| `rm -r directorio` | Elimina directorios y su contenido recursivamente. | `rm -r cache/` |
| `rm -f` | Fuerza la eliminación sin confirmación. | `rm -f temporal.log` |
| `rm -rf` | Elimina sin confirmación y de forma recursiva. | `rm -rf /tmp/test` |

> **Precaución:** `rm -rf` es irreversible; úsalo solo cuando estés seguro.

---

### Ver y combinar archivos

| Comando | Descripción | Ejemplo |
|----------|--------------|---------|
| `cat` | Muestra el contenido de un archivo. | `cat index.html` |
| `less` | Visualiza el contenido con paginación. | `less texto.txt` |
| `head` | Muestra las primeras líneas. | `head -n 5 log.txt` |
| `tail` | Muestra las últimas líneas. | `tail -n 10 log.txt` |
| `tail -f` | Muestra en tiempo real la actualización de un archivo (útil para logs). | `tail -f /var/log/syslog` |

---

## 1.6 Redirecciones y canalizaciones

Una de las características más poderosas del shell es la posibilidad de **redirigir la salida o la entrada** de los comandos, y de **encadenarlos** mediante canalizaciones (*pipes*).

### Redirección de salida estándar (stdout)

Por defecto, los comandos muestran la salida en pantalla. Puede redirigirse a un archivo:

| Operador | Descripción | Ejemplo |
|-----------|--------------|---------|
| `>` | Redirige la salida, **sobrescribiendo** el archivo. | `ls -l > listado.txt` |
| `>>` | Redirige la salida **añadiendo** al final del archivo. | `ls -lh >> listado.txt` |

---

### Redirección de errores (stderr)

| Operador | Descripción | Ejemplo |
|-----------|--------------|---------|
| `2>` | Redirige solo los errores. | `ls /carpeta_inexistente 2> errores.log` |
| `2>>` | Añade errores al final del archivo. | `ls /root 2>> errores.log` |

---

### Combinación de salida y errores

| Operador | Descripción | Ejemplo |
|-----------|--------------|---------|
| `> archivo 2>&1` | Redirige salida y errores al mismo archivo. | `comando > salida.log 2>&1` |

---

### Redirección de entrada (stdin)

Permite que un comando lea datos de un archivo.

```bash
sort < nombres.txt
```

El comando `sort` leerá el contenido de `nombres.txt` como si lo hubiésemos escrito manualmente.

---

### Canalizaciones (pipes)

El operador `|` conecta la salida de un comando con la entrada de otro.  
Permite construir cadenas de procesamiento muy potentes.

#### Ejemplos prácticos

Mostrar solo las líneas que contienen “html” en un directorio:
```bash
ls -l | grep html
```

Contar cuántas líneas contienen una palabra:
```bash
grep -i "error" log.txt | wc -l
```

Ver los 10 procesos más consumidores de memoria:
```bash
ps aux | sort -nrk 4 | head -n 10
```

Buscar archivos por nombre y mostrarlos con detalles:
```bash
find /var/www -name "*.php" | xargs ls -lh
```

---

# Tema 2: Estructura del sistema de archivos en Linux

## 2.1 Jerarquía y directorios principales

Linux organiza los archivos en una **jerarquía única** con la raíz en `/`. La mayor parte de las distribuciones siguen el estándar **FHS (Filesystem Hierarchy Standard)**. A continuación, un resumen de los directorios más relevantes y su propósito:

| Directorio | Propósito / Contenido típico |
|-----------|-------------------------------|
| `/` | Raíz del sistema de archivos. Punto de partida de toda la jerarquía. |
| `/bin` | Binarios esenciales para todos los usuarios (p. ej., `ls`, `cp`, `mv`, `cat`). En sistemas modernos suele ser enlace a `/usr/bin`. |
| `/sbin` | Binarios esenciales de administración (p. ej., `mount`, `fsck`, `ip`). A menudo enlace a `/usr/sbin`. |
| `/usr` | Software de solo lectura para los usuarios (binarios, bibliotecas, documentación). |
| `/usr/bin` | Programas de usuario no esenciales para el arranque (la mayoría de comandos). |
| `/usr/sbin` | Herramientas de administración no esenciales para el arranque. |
| `/usr/lib`, `/usr/lib64` | Bibliotecas compartidas. |
| `/usr/local` | Software instalado localmente por el administrador (no gestionado por el sistema de paquetes). |
| `/var` | Datos variables: logs, colas de impresión, cachés, bases de datos, correo. |
| `/var/log` | Registros del sistema y servicios. |
| `/etc` | Configuración del sistema (archivos de texto). |
| `/home` | Directorios personales de los usuarios. |
| `/root` | Directorio personal del superusuario `root`. |
| `/opt` | Paquetes adicionales/propietarios instalados de forma opcional. |
| `/srv` | Datos de servicios (por ejemplo, contenido de sitios web). |
| `/media` | Puntos de montaje para dispositivos extraíbles (USB, DVDs). |
| `/mnt` | Punto de montaje temporal para administradores. |
| `/run` | Datos de ejecución en tiempo real (tmpfs), sockets y PIDs. |
| `/tmp` | Archivos temporales (se limpia periódicamente). |
| `/dev` | Dispositivos (bloque/caracter), pseudo-dispositivos (p. ej., `/dev/null`). |
| `/proc` | Sistema de archivos virtual con información del kernel y procesos. |
| `/sys` | Información del kernel y dispositivos (sysfs). |
| `/boot` | Archivos necesarios para el arranque (kernel, initramfs, cargador). |
| `/lib`, `/lib64` | Bibliotecas esenciales para el arranque (a veces enlaces a `/usr/lib*`). |

### Tipos de archivos en Linux
- **Archivo regular** (`-`): datos, texto, binarios.
- **Directorio** (`d`).
- **Enlace simbólico** (`l`) y **enlace duro**.
- **Dispositivo de bloque** (`b`) y **de carácter** (`c`) en `/dev`.
- **Socket** (`s`) y **FIFO/tubería con nombre** (`p`).

Puede consultarse con:
```bash
ls -l            # Tipo en la primera columna (d, -, l, b, c, s, p)
file <ruta>      # Intenta adivinar el tipo de contenido
stat <ruta>      # Metadatos detallados (inode, permisos, tiempos, etc.)
```

### Puntos de montaje y dispositivos
Los sistemas de archivos (ext4, xfs, vfat, ntfs…) se **montan** en directorios vacíos llamados **puntos de montaje**.
```bash
mount            # Muestra sistemas montados
lsblk            # Dispositivos y particiones
blkid            # UUID y tipos de sistema de archivos
```

Nombres de dispositivos habituales:
- Discos SATA/SCSI: `/dev/sda`, `/dev/sdb`… (particiones: `/dev/sda1`, `/dev/sda2`…)
- NVMe: `/dev/nvme0n1`, partición 1 → `/dev/nvme0n1p1`
- MMC/SD: `/dev/mmcblk0p1`

Montaje manual:
```bash
sudo mount /dev/sdb1 /mnt
sudo umount /mnt
```
Montaje persistente en `/etc/fstab` (recomendado usar **UUID**):
```
UUID=xxxx-xxxx  /datos  ext4  defaults  0  2
```

---

## 2.2 El sistema de archivos: rutas absolutas y relativas

Una **ruta absoluta** comienza en `/` y define la ubicación exacta de un archivo independientemente del directorio actual:
```bash
cd /var/www/html
```

Una **ruta relativa** parte del **directorio actual**:
```bash
cd proyectos/web1      # relativo al directorio actual
```

Atajos y símbolos:
- `.`  → directorio actual
- `..` → directorio padre
- `~`  → directorio personal del usuario (equivale a `$HOME`)

Ejemplos:
```bash
pwd                   # muestra la ruta actual
cd ..                 # sube un nivel
cd ~/Descargas        # entra en el directorio Descargas del usuario
```

Espacios y caracteres especiales:
```bash
cd "Mi Carpeta"       # comillas para rutas con espacios
cd Mi\ Carpeta        # escape con barra invertida
```

### Globbing (comodines) y expansiones útiles
- `*`  → cero o más caracteres: `ls *.png`
- `?`  → un único carácter: `ls foto?.jpg`
- `[abc]` → conjunto de caracteres: `ls imagen[12].png`
- `{dev,prod}` → expansión de llaves: `mkdir -p logs/{dev,prod}`

Resolver enlaces y rutas físicas:
```bash
readlink -f archivo   # ruta canónica
pwd -P                # directorio real (sin enlaces simbólicos)
```

### Enlaces duros y simbólicos
- **Enlace duro**: otro nombre para el mismo *inode* (solo dentro del mismo sistema de archivos).
- **Enlace simbólico** (recomendado): un puntero a otro archivo o directorio.
```bash
ln archivo.txt copia_dura.txt     # enlace duro
ln -s /opt/app/config ./config    # symlink
```

---

## 2.3 Usuario, grupos y permisos

La seguridad y el control de acceso en Linux se basan en **usuarios**, **grupos** y **permisos**. Cada archivo/directorio tiene un **propietario** (usuario) y un **grupo** asociados.

### 2.3.1 Cuentas y ficheros de sistema
- `/etc/passwd`  → información básica de cuentas (nombre, UID, GID, shell, home).
- `/etc/shadow`  → contraseñas cifradas y políticas (solo legible por root).
- `/etc/group`   → definición de grupos y sus miembros.

Consultar identidad y pertenencia:
```bash
whoami             # usuario actual
id                 # UID, GID y grupos
groups usuario     # grupos de un usuario
getent passwd user # consulta a la base de cuentas (incluye NSS, LDAP, etc.)
```

### 2.3.2 Gestión de usuarios
Los comandos pueden variar (Debian/Ubuntu dispone de `adduser` interactivo). En general:

Crear usuario con directorio personal y shell:
```bash
sudo useradd -m -s /bin/bash dev1
sudo passwd dev1
```
Opciones comunes de `useradd`:
- `-m` crea el home a partir de `/etc/skel`.
- `-s` establece el shell de login.
- `-u` fija el **UID**; `-g` el **GID** principal; `-G` grupos secundarios.
- `-d` define una ruta de home personalizada.

Modificar atributos de un usuario:
```bash
sudo usermod -aG docker dev1     # añade a grupo 'docker' (sin -a sobreescribe)
sudo usermod -s /bin/zsh dev1    # cambia el shell
sudo usermod -d /srv/dev1 -m dev1 # mueve y renombra su home
```

Eliminar usuario (con o sin su home):
```bash
sudo userdel dev1
sudo userdel -r dev1  # elimina también el directorio personal
```

Política de contraseñas y caducidad:
```bash
sudo passwd dev1          # cambia/establece contraseña
sudo chage -l dev1        # consulta caducidad
sudo chage -M 90 dev1     # obliga cambio cada 90 días
sudo chage -E 2025-12-31 dev1  # fecha de expiración de la cuenta
```

Cambios de datos informativos (gecos), shell:
```bash
chfn dev1                 # nombre completo, etc.
chsh -s /bin/bash dev1    # cambia el shell
```

### 2.3.3 Gestión de grupos
Crear, modificar y eliminar grupos:
```bash
sudo groupadd webdev
sudo groupmod -n frontend webdev   # renombra grupo
sudo groupdel frontend
```
Añadir/quitar usuarios a grupos secundarios:
```bash
sudo usermod -aG webdev dev1
sudo gpasswd -d dev1 webdev
```
Cambiar de grupo efectivo en una sesión:
```bash
newgrp webdev
```

### 2.3.4 Elevación de privilegios: `su`, `sudo` y `visudo`
- `su -` inicia una sesión como otro usuario (por defecto, root) pidiendo su contraseña.
- `sudo <comando>` ejecuta un comando como root (o como otro usuario con `-u`) pidiendo la contraseña del **propio** usuario.

Configuración segura de sudoers (siempre con `visudo`):
```bash
sudo visudo   # edita /etc/sudoers con comprobación de sintaxis
```
Ejemplo mínimo para permitir a un grupo:
```
%sudo ALL=(ALL:ALL) ALL
```
Para un usuario concreto sin pedir contraseña para un comando específico:
```
dev1 ALL=(root) NOPASSWD: /usr/bin/systemctl restart nginx
```

### 2.3.5 Propietarios y permisos de archivos
Visualización y significado de permisos (modo simbólico):
```
-rwxr-x--- 1 dev1 webdev  1202 oct  8 12:01 deploy.sh
```
- `r` lectura, `w` escritura, `x` ejecución.
- Tres tríos de permisos: **usuario** (u), **grupo** (g), **otros** (o).
- Propietario: `dev1`, grupo: `webdev`.

Cambiar propietario y grupo:
```bash
sudo chown dev1:webdev deploy.sh
sudo chgrp webdev src/ -R
```
Cambio recursivo (útil pero peligroso si no se delimita bien):
```bash
sudo chown -R www-data:www-data /var/www/miweb
```

Modificar permisos con `chmod` (simbólico y numérico):
```bash
chmod u+x script.sh      # añade ejecución al usuario
chmod g-w fichero.txt    # quita escritura al grupo
chmod o-rwx privado/     # retira todo a otros
chmod 640 config.yaml    # rw- r-- ---
chmod 755 run.sh         # rwx r-x r-x
```

### 2.3.6 Máscara de creación (umask)
La **umask** define qué permisos se **restan** al crear archivos/directorios.
- Umask habitual para colaborativo: `002` (archivos 664, directorios 775).
- Entornos más restrictivos: `022` (archivos 644, directorios 755).

Consultar y fijar temporalmente:
```bash
umask           # muestra valor actual
umask 002       # nueva máscara para la sesión actual
```

### 2.3.7 Bits especiales: SUID, SGID y Sticky
- **SUID (4xxx)** en binarios: ejecuta con UID del propietario. Ej.: `chmod u+s /usr/bin/passwd` (ya lo tiene por defecto).
- **SGID (2xxx)** en binarios o directorios: hereda el GID del directorio. Muy útil para directorios de trabajo compartido.
- **Sticky bit (1xxx)** en directorios: solo el propietario puede borrar su propio archivo incluso si el directorio es escribible por todos (ej.: `/tmp`).

Ejemplos:
```bash
chmod g+s /srv/proyectos/web      # herencia de grupo en subdirectorios
chmod +t /srv/proyectos/web       # sticky bit
# numéricos equivalentes (directorio 2775: rwxrwsr-x)
chmod 2775 /srv/proyectos/web
```

### 2.3.8 ACLs (Listas de Control de Acceso)
Permiten permisos más granulares por usuario/grupo, además del trío u/g/o. Requieren soporte del sistema de archivos (ext4/xfs lo soportan por defecto).

Asignar ACL y consultar:
```bash
setfacl -m u:dev2:rwx /srv/proyectos/web
setfacl -m g:qa:r-x  /srv/proyectos/web
getfacl /srv/proyectos/web
```
ACL por defecto para nuevos archivos en un directorio:
```bash
setfacl -m d:u:dev2:rwx /srv/proyectos/web
```

### 2.3.9 Atributos extendidos (chattr/lsattr)
A nivel de sistema de archivos (ext*), permiten restricciones adicionales.
```bash
sudo chattr +i config.yaml   # inmutable: no se puede modificar ni borrar
lsattr config.yaml
sudo chattr -i config.yaml
```

### 2.3.10 Patrones prácticos (escenarios DAW)

**Directorio de proyecto web colaborativo:**
```bash
sudo groupadd webteam
sudo usermod -aG webteam dev1
sudo usermod -aG webteam dev2

sudo mkdir -p /srv/www/miweb
sudo chown -R dev1:webteam /srv/www/miweb
sudo chmod 2775 /srv/www/miweb            # sgid para heredar grupo
umask 002                                  # sesión colaborativa
# Con ACLs finas (opcional)
sudo setfacl -m g:webteam:rwx /srv/www/miweb
sudo setfacl -m d:g:webteam:rwx /srv/www/miweb
```

**Servicio web servido por `www-data` y editable por desarrolladores:**
```bash
sudo chown -R www-data:webteam /var/www/miapp
sudo chmod -R 2775 /var/www/miapp
sudo usermod -aG webteam dev1
sudo usermod -aG webteam dev2
```

**Añadir un usuario al grupo `docker` para usar Docker sin sudo:**
```bash
sudo usermod -aG docker dev1
# Cerrar sesión y volver a entrar para refrescar grupos
```

**Restringir borrado en un directorio compartido:**
```bash
sudo chmod +t /srv/compartido   # sticky bit
```

---

## 4. Entorno de desarrollo y configuración práctica en Linux

### 4.1 Introducción al entorno del desarrollador

En Linux, el entorno de desarrollo se construye sobre el **shell**, que actúa como interfaz entre el usuario y el sistema operativo.  
Desde el shell se pueden ejecutar comandos, configurar variables de entorno, instalar software y automatizar tareas de compilación o despliegue.

El shell más común es **Bash**, aunque también se utilizan **Zsh** o **Fish**.  
Cuando se abre una terminal, el sistema carga configuraciones iniciales definidas en archivos como:

- `~/.bashrc` → configuración personal que se ejecuta en cada sesión interactiva.  
- `~/.profile` o `~/.bash_profile` → configuración general del usuario.  
- `/etc/profile` → configuración global del sistema.

Para aplicar cambios sin cerrar la sesión actual:
```bash
source ~/.bashrc
```

---

### 4.2 Variables de entorno y rutas del sistema

Las **variables de entorno** almacenan información que utilizan tanto el sistema como los programas.  
Son fundamentales para controlar la forma en que se ejecutan los procesos y localizar herramientas o librerías.

| Variable | Función |
|-----------|----------|
| `$PATH` | Define los directorios donde se buscan los comandos ejecutables. |
| `$HOME` | Indica el directorio personal del usuario. |
| `$USER` | Muestra el nombre del usuario actual. |
| `$PWD` | Indica el directorio actual. |
| `$SHELL` | Indica el intérprete de comandos en uso. |
| `$LANG` | Determina el idioma y la codificación de la sesión. |
| `$EDITOR` | Establece el editor de texto por defecto. |

#### Definir y exportar variables

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$PATH:$JAVA_HOME/bin
```

Esto añade el binario de Java al PATH, permitiendo ejecutar `java` o `javac` desde cualquier directorio.

Eliminar una variable:
```bash
unset VARIABLE
```

Listar todas las variables de entorno activas:
```bash
printenv
```

Estas configuraciones pueden añadirse al archivo `~/.bashrc` o `~/.profile` para que sean permanentes.

---

### 4.3 Alias, funciones y personalización del entorno

Los **alias** sirven para crear atajos que simplifican comandos largos o frecuentes.

```bash
alias cls='clear'
alias ejecutar='python3 main.py'
alias actualizar='sudo apt update && sudo apt upgrade -y'
```

Para hacerlos permanentes, se guardan en `~/.bashrc` y se recargan con:
```bash
source ~/.bashrc
```

También se pueden definir **funciones** dentro del shell para automatizar tareas repetitivas.

```bash
deploy() {
    cd ~/proyecto && python3 manage.py runserver
}
```

Este ejemplo cambia al directorio del proyecto y ejecuta el servidor de desarrollo de Django.

---

### 4.4 Configuración del entorno de desarrollo para Python

Python incluye herramientas muy útiles para crear entornos aislados, evitando conflictos entre proyectos.  
Para ello se utiliza el módulo `venv`.

#### Creación y uso de un entorno virtual

```bash
python3 -m venv venv
source venv/bin/activate
# el prompt cambiará indicando que el entorno está activo
pip install flask
deactivate
```

El entorno virtual crea una copia del intérprete y librerías que no afectan al resto del sistema.  
Esto permite que cada proyecto tenga sus propias dependencias.

Para guardar las dependencias instaladas:
```bash
pip freeze > requirements.txt
```

Y para restaurarlas en otro entorno:
```bash
pip install -r requirements.txt
```

---

### 4.5 Configuración del entorno de desarrollo para Kotlin

Kotlin se ejecuta sobre la **JVM (Java Virtual Machine)**, por lo que requiere tener instalado un JDK (Java Development Kit).

#### Instalación del JDK y Kotlin

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
sudo apt install kotlin -y
```

Comprobar la instalación:

```bash
java -version
kotlinc -version
```

#### Compilar y ejecutar un programa Kotlin

```bash
kotlinc Hola.kt -include-runtime -d Hola.jar
java -jar Hola.jar
```

Esto genera un archivo ejecutable `.jar` con el código Kotlin compilado.

Para automatizar compilaciones más complejas se usa **Gradle**, que maneja dependencias y tareas.

```bash
sudo apt install gradle -y
gradle build
```

El entorno Kotlin puede configurarse mediante las variables de entorno:
```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$PATH:/usr/share/kotlin/bin
```

---

### 4.6 Ejemplo práctico: instalación y configuración de un servidor Apache

**Apache HTTP Server** es uno de los servidores web más utilizados.  
Su función es recibir peticiones HTTP y devolver contenido web (HTML, imágenes, scripts, etc.).

#### 1. Instalación del servidor

```bash
sudo apt update
sudo apt install apache2 -y
```

#### 2. Verificar el estado del servicio

```bash
sudo systemctl status apache2
```

Si está inactivo, iniciarlo:
```bash
sudo systemctl start apache2
```

Y configurarlo para que arranque automáticamente con el sistema:
```bash
sudo systemctl enable apache2
```

#### 3. Comprobar funcionamiento

Abre un navegador y accede a:
```
http://localhost
```
Debería mostrarse la página de bienvenida de Apache.

#### 4. Directorio raíz y permisos

El contenido web se encuentra en:
```
/var/www/html
```

Puedes editar el archivo principal con:
```bash
sudo nano /var/www/html/index.html
```

Para probar un cambio, edita y guarda una versión personalizada:
```html
<h1>Servidor Apache funcionando correctamente</h1>
```

Reinicia el servicio para aplicar los cambios:
```bash
sudo systemctl restart apache2
```

#### 5. Configuración básica de un sitio

La configuración por defecto se encuentra en:
```
/etc/apache2/sites-available/000-default.conf
```

Para crear un nuevo sitio:
```bash
sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/miweb.conf
sudo nano /etc/apache2/sites-available/miweb.conf
```

Modificar las líneas principales:
```
ServerName miweb.local
DocumentRoot /var/www/miweb
```

Activar el sitio y reiniciar Apache:
```bash
sudo a2ensite miweb.conf
sudo systemctl reload apache2
```

Por último, crea el directorio del nuevo sitio:
```bash
sudo mkdir /var/www/miweb
sudo chown -R $USER:$USER /var/www/miweb
echo "<h1>Mi sitio Apache</h1>" > /var/www/miweb/index.html
```

Comprobar:
```
http://miweb.local
```

---

### 4.7 Buenas prácticas generales

- Mantener el sistema actualizado (`sudo apt update && sudo apt upgrade -y`).
- No usar `sudo` innecesariamente en entornos de desarrollo.
- Documentar variables de entorno y alias en un README.
- Usar entornos virtuales para aislar dependencias (especialmente en Python).
- Automatizar tareas comunes mediante scripts (`.sh`) o `Makefile`.

---


## 5. Visualización y edición básica de archivos

En los entornos Linux, la terminal permite **consultar, visualizar y editar archivos de texto** directamente, sin necesidad de interfaces gráficas.  
Esto resulta especialmente útil para revisar registros del sistema, modificar configuraciones o inspeccionar código fuente de manera rápida.

---

### 5.1 Comandos para mostrar contenido (`cat`, `less`, `more`)

#### `cat` — Mostrar el contenido completo de un archivo

El comando `cat` (concatenate) permite **visualizar, combinar o crear archivos de texto**.

```bash
cat archivo.txt
```
Muestra el contenido completo del archivo.  
Si el archivo es largo, el texto pasará rápidamente por pantalla.

**Opciones más usadas:**

| Opción | Descripción | Ejemplo |
|---------|--------------|---------|
| `-n` | Numera todas las líneas. | `cat -n archivo.txt` |
| `-b` | Numera solo las líneas no vacías. | `cat -b archivo.txt` |
| `-s` | Suprime líneas vacías repetidas. | `cat -s archivo.txt` |

**Combinar archivos:**
```bash
cat parte1.txt parte2.txt > completo.txt
```

**Crear rápidamente un archivo de texto:**
```bash
cat > notas.txt
Escribe aquí el contenido.
Presiona Ctrl + D para guardar.
```

---

#### `less` — Lectura interactiva y paginada

`less` es ideal para **leer archivos largos** sin saturar la pantalla.  
Permite avanzar, retroceder, buscar texto y salir fácilmente.

```bash
less archivo.log
```
**Controles básicos dentro de `less`:**
- `Espacio`: avanzar una página.
- `b`: retroceder una página.
- `/palabra`: buscar un término.
- `n`: siguiente coincidencia.
- `q`: salir.

Ventajas sobre `cat`: no carga todo el archivo en memoria, lo muestra página a página.

---

#### `more` — Visualización básica por páginas

`more` fue el precursor de `less`. Tiene funciones similares, aunque menos potentes.

```bash
more archivo.txt
```

**Controles básicos:**
- `Espacio`: avanzar una página.
- `Enter`: avanzar una línea.
- `q`: salir.

---

### 5.2 Edición rápida con `nano` y consulta con `head` / `tail`

#### `nano` — Editor de texto en terminal

`nano` es un **editor simple e intuitivo**, perfecto para modificaciones rápidas.

Abrir o crear un archivo:
```bash
nano archivo.txt
```

**Combinaciones más usadas:**
- `Ctrl + O`: guardar cambios.
- `Ctrl + X`: salir del editor.
- `Ctrl + W`: buscar texto.
- `Ctrl + K`: cortar línea.
- `Ctrl + U`: pegar.

**Ejemplo práctico:**  
Editar el archivo de configuración del servidor Apache:
```bash
sudo nano /etc/apache2/apache2.conf
```

---

#### `head` — Mostrar las primeras líneas

Permite ver solo el inicio de un archivo, útil para revisar encabezados o estructuras.

```bash
head archivo.txt
```
Por defecto muestra las 10 primeras líneas.  
Cambiar la cantidad de líneas mostradas:
```bash
head -n 20 archivo.txt
```

---

#### `tail` — Mostrar las últimas líneas

Muestra el final de un archivo, muy útil para consultar registros (logs).

```bash
tail archivo.log
```
Por defecto muestra las últimas 10 líneas.  
Para ver las últimas 50:
```bash
tail -n 50 archivo.log
```

**Modo seguimiento en tiempo real (`-f`):**
```bash
tail -f /var/log/syslog
```
Muestra en vivo las nuevas líneas que se agregan al archivo. Es esencial para monitorear servidores, procesos o aplicaciones web en ejecución.

---

### 5.3 Visualización de archivos ocultos

En Linux, los archivos ocultos son aquellos cuyo nombre comienza con un punto (`.`).  
Estos archivos suelen almacenar configuraciones personales o del sistema, como `.bashrc`, `.gitconfig` o `.ssh/`.

Para mostrar archivos ocultos en el directorio actual:
```bash
ls -a
```

Para mostrar información detallada (permisos, fechas, tamaño):
```bash
ls -la
```

También puedes combinarlos con otros comandos para inspeccionarlos:
```bash
cat .bashrc
less .gitconfig
```

**Ejemplo práctico:**  
Visualizar el archivo de configuración del shell del usuario:
```bash
cat ~/.bashrc
```

---

