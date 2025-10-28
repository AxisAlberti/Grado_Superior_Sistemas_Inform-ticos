

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


<div style="text-align: center;">
  <img src="../imagenes/topologia.webp" alt="Descripción de la imagen" style="display: block; margin: 0 auto; max-width: 100%; height: auto;">
</div>

---

### Modos de comunicación
- **Unicast:** uno-a-uno (la mayoría del tráfico).
- **Broadcast:** uno-a-todos dentro de la misma red (ARP, descubrimientos).
- **Multicast:** uno-a-muchos interesados (streaming, videoconferencia).

<div style="text-align: center;">
  <img src="../imagenes/broadcast.webp" alt="Descripción de la imagen" style="display: block; margin: 0 auto; max-width: 100%; height: auto;">
</div>
---

# Modos de envío en redes: Unicast, Broadcast y Multicast

## 1) Unicast — *uno a uno*
**Qué es:** Comunicación entre **un emisor** y **un receptor** concretos.  
**Ejemplos:** Abrir una web (tu navegador ↔ servidor), enviar un correo SMTP, una petición a una API.

**Cómo funciona (idea)**
- **Capa 3 (IP):** el paquete va dirigido a **una IP destino**.
- **Capa 2 (Ethernet):** la trama lleva **una MAC destino** concreta.
- **Switch:** reenvía solo por el puerto donde está el receptor (si lo conoce).
- **Router:** encamina hacia la red del destinatario.

**Ventajas**
- Eficiente cuando solo **una** máquina necesita el dato.
- Fácil de **controlar y asegurar** (firewall, QoS por flujo).

**Limitaciones**
- Si **muchos** clientes piden **lo mismo**, el servidor repite N veces el envío (N flujos unicast).

---

## 2) Broadcast — *uno a todos* (en la misma red)
**Qué es:** Un emisor envía a **todas** las máquinas de su **red local** (dominio de broadcast).  
**Ejemplos típicos:**  
- **ARP**: “¿Quién tiene la IP X? respóndeme tu MAC”  
- Descubrimientos automáticos (algunos servicios locales)

**Cómo funciona (idea)**
- **IPv4:** dirección **255.255.255.255** (o broadcast de la subred).  
- **Ethernet:** MAC destino **ff:ff:ff:ff:ff:ff** (especial “todos”).  
- **Switch:** inunda **todos los puertos** de la VLAN (menos el de origen).  
- **Router:** **no** reenvía broadcast a otras redes (lo **bloquea** por defecto).

**Ventajas**
- Útil para **descubrir** quién está en la red cuando aún no sabes su MAC/IP.

**Riesgos / límites**
- Si hay **mucho broadcast**, **satura** la red (broadcast storm).
- No atraviesa routers: su alcance se limita a tu **subred/VLAN**.

> Nota: **DHCP** usa broadcast para descubrir el servidor, pero a menudo el router actúa como **relay** para “traspasar” la petición a otra red.

---

## 3) Multicast — *uno a muchos interesados*
**Qué es:** Un emisor envía **un solo flujo** y **varios receptores** que **se apuntan** a un “grupo” lo reciben. Es “uno a muchos”, **pero solo a quienes se suscriben**.

**Ejemplos típicos**
- Vídeo en directo/streaming corporativo a muchas aulas.
- Conferencias o distribución de datos en tiempo real.

**Cómo funciona (idea suave)**
- **IPv4:** direcciones **224.0.0.0–239.255.255.255** (rango multicast).
- **IPv6:** **ff00::/8**.
- Los receptores se **suscriben** al grupo (protocolo **IGMP** en IPv4 / **MLD** en IPv6).
- **Switches** con *IGMP snooping* aprenden **qué puertos** quieren ese grupo y **evitan inundar** toda la red.
- **Routers** pueden usar **PIM** para distribuir el tráfico entre redes si hace falta (detalle avanzado).

**Ventajas**
- Muy **eficiente** cuando **muchos** clientes necesitan **el mismo** contenido: el emisor solo manda **una vez**.

**Limitaciones**
- Requiere **soporte** de la red (IGMP/MLD, IGMP snooping, a veces configuración en routers).
- No todos los entornos/ISPs permiten multicast más allá de la red local sin configuración específica.

---

## Comparativa rápida

| Modo        | Destino            | Alcance por defecto        | Ejemplos                       | Pros                               | Contras                                  |
|-------------|--------------------|----------------------------|---------------------------------|-------------------------------------|-------------------------------------------|
| **Unicast** | 1 receptor         | Enrutado entre redes       | Navegar web, API, email         | Sencillo, controlable               | Poco eficiente si hay muchos receptores   |
| **Broadcast** | Todos en la subred | **Solo** la subred/VLAN    | ARP, descubrimiento local       | Descubrimiento rápido               | Puede saturar; no cruza routers           |
| **Multicast** | Varios suscritos   | Subred y (opcional) entre redes | Streaming, avisos simultáneos | Un envío para muchos (eficiente)    | Requiere soporte/configuración de red     |

---

## Mini-ejemplos “mentales”

- **Unicast:** Tu PC → servidor web: *“Dame /index.html”* → Solo el servidor responde.  
- **Broadcast:** Tu PC pregunta por ARP: *“¿Quién tiene 192.168.1.20?”* → Todos escuchan; **solo** quien tiene esa IP responde.  
- **Multicast:** Un profesor emite un vídeo a la clase: los PCs que se apuntaron al **grupo multicast** lo reciben; los demás **no**.

---

## Buenas prácticas (para devs y admins junior)
- Usa **unicast** para el tráfico normal de tus apps web.  
- **Minimiza** broadcast: segmenta en **VLAN** si la red crece.  
- Para “uno a muchos”, evalúa **multicast** (si tu red lo soporta) o usa **CDN**/streaming sobre HTTP (unicast) según tu caso.  
- En aulas/labs, activa **IGMP snooping** en switches si usas multicast para evitar inundaciones.

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




