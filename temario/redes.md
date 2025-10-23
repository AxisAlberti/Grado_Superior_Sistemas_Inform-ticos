

# Índice orientativo — Redes (Grado Medio)

1. [Introducción a las redes](#introducción-a-las-redes)
2. [Medios y hardware de red](#medios-y-hardware-de-red)
3. [Modelo OSI (7 capas)](#modelo-osi-7-capas)
4. [Modelo TCP/IP](#modelo-tcpip)
5. [Direccionamiento IPv4](#direccionamiento-ipv4)
6. [Cálculo de subredes (IPv4)](#cálculo-de-subredes-ipv4)
7. [Introducción a IPv6](#introducción-a-ipv6)
8. [Servicios esenciales](#servicios-esenciales)

## Introducción a las redes

### ¿Qué es una red?
Una **red** es un conjunto de **dispositivos** (ordenadores, móviles, impresoras, cámaras, IoT…) **interconectados** que **intercambian datos** y **comparten recursos** (archivos, Internet, servicios). El objetivo es **comunicar** de forma **fiable, eficiente y segura**.

### Objetivos de aprendizaje
- Comprender los **beneficios** de una red frente al trabajo aislado.
- Identificar **componentes** básicos (nodo, medio, interfaz) y **métricas** de rendimiento.
- Reconocer **tipos de redes** según su alcance y **topologías** más comunes.
- Diferenciar **modos de comunicación** (unicast/multicast/broadcast) y **arquitecturas** (cliente-servidor/peer-to-peer).

---

### Beneficios principales
- **Compartición de recursos:** Internet, impresoras, almacenamiento, apps.
- **Colaboración:** trabajo en equipo, mensajería, videoconferencia.
- **Centralización y control:** copias de seguridad, políticas, autenticación.
- **Escalabilidad y disponibilidad:** crecer sin reconfigurar desde cero.

---

### Conceptos clave y terminología
- **Nodo / Host:** dispositivo conectado a la red (PC, móvil, servidor…).
- **Enlace / Medio:** camino por el que viajan los datos (**cobre, fibra, radio**).
- **Interfaz de red (NIC):** hardware que conecta el dispositivo a la red (tiene **MAC**).
- **Dirección MAC:** identificador **físico** (capa de enlace).
- **Dirección IP:** identificador **lógico** (capa de red) para enrutar entre redes.
- **Encapsulación:** cada capa añade su **cabecera** (y a veces tráiler) a los datos.

---

### Métricas de rendimiento (y por qué importan)
- **Ancho de banda (capacidad):** tasa máxima teórica (p. ej., 1 Gb/s).
- **Throughput (rendimiento real):** tasa efectiva que se logra en práctica.
- **Latencia:** tiempo que tarda un mensaje en ir de origen a destino.
- **Jitter:** variación de la latencia entre paquetes (crítico en voz/vídeo).
- **Pérdida de paquetes:** porcentaje de paquetes que no llegan.

> Regla mental: para **juegos/voz** prima **baja latencia/jitter**; para **copias** prima **throughput**.

---

### Clasificación por alcance
- **PAN** (Personal Area Network): muy corta distancia (Bluetooth, tethering).
- **LAN** (Local Area Network): red local de casa/centro educativo/oficina.
- **WLAN**: LAN inalámbrica (Wi-Fi).
- **CAN** (Campus): varias LAN dentro de un campus/edificio.
- **MAN** (Metropolitana): red de ciudad/área metropolitana.
- **WAN** (Wide Area Network): gran alcance (proveedores, Internet).

---

### Topologías (físicas/lógicas)
- **Estrella:** todos al **switch** central (la más común en LAN cableada).
- **Malla:** múltiples caminos redundantes (alta disponibilidad).
- **Árbol (jerárquica):** combinación escalable de estrellas.
- **Anillo / Bus:** históricas o nicho; aparecen en ciertos contextos industriales.

> **Física ≠ Lógica**: una red Wi-Fi puede verse lógicamente como estrella (AP central) aunque físicamente sea radio compartida.

topologia.webp

<div style="text-align: center;">
  <img src="../imagenes/topologia.webp" alt="Descripción de la imagen" style="display: block; margin: 0 auto; max-width: 100%; height: auto;">
</div>

---

### Modos de comunicación
- **Unicast:** uno-a-uno (la mayoría del tráfico).
- **Broadcast:** uno-a-todos dentro de la misma red (ARP, descubrimientos).
- **Multicast:** uno-a-muchos interesados (streaming, videoconferencia).

---

### Arquitecturas lógicas de servicio
- **Cliente-servidor:** servicios centralizados (web, bases de datos, DNS, DHCP).
- **Peer-to-peer (P2P):** los nodos actúan como clientes y servidores entre sí (uso didáctico: compartición simple en pequeñas redes).

---

### Componentes básicos de una LAN
- **Switch:** conmutación a nivel de enlace; crea dominios de colisión separados.
- **Router:** interconecta **redes distintas** y enruta tráfico IP.
- **Punto de acceso (AP):** conecta dispositivos **Wi-Fi** a la LAN.
- **Cableado/Medios:** UTP/FTP (cobre), **fibra óptica**, radio (Wi-Fi).

---




