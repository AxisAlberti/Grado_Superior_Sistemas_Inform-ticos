

# Índice — Redes 

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


## 1) Unicast — *uno a uno*
**Qué es:** Comunicación entre **un emisor** y **un receptor** concretos.  
**Ejemplos:** Abrir una web (tu navegador ↔ servidor), enviar un correo SMTP, una petición a una API.

**Cómo funciona**
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

**Cómo funciona**
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


### Componentes básicos de una LAN
- **Switch:** conmutación a nivel de enlace; crea dominios de colisión separados.
- **Router:** interconecta **redes distintas** y enruta tráfico IP.
- **Punto de acceso (AP):** conecta dispositivos **Wi-Fi** a la LAN.
- **Cableado/Medios:** UTP/FTP (cobre), **fibra óptica**, radio (Wi-Fi).

---


## Medios y hardware de red

En este apartado se estudian los **medios físicos** (por donde viajan los datos) y los **dispositivos** que forman la infraestructura básica de una red. La idea es reconocer **qué usar**, **dónde** y **por qué**.

---

### 2.1 Medios de transmisión

#### Cable de par trenzado (UTP/STP)
Es el cable **Ethernet** típico con conector **RJ-45**. Está formado por pares de hilos **trenzados** para reducir interferencias.

- **UTP (Unshielded Twisted Pair)**: sin malla metálica. Es el más común en oficinas y aulas.  
- **STP/FTP (Shielded/Foil Twisted Pair)**: con **apantallamiento** (malla o lámina). Se usa en entornos con más **ruido eléctrico** o tiradas largas junto a cables de potencia.

---

<div style="text-align: center;">
  <img src="../imagenes/utp.png" alt="Descripción de la imagen" style="display: block; margin: 0 auto; max-width: 100%; height: auto;">
</div>

---


**Categorías (ejemplos habituales)**  
- **Cat5e**: hasta **1 Gb/s** (Gigabit) a **100 m**.  
- **Cat6**: **1 Gb/s** a 100 m y **10 Gb/s** hasta ~**55 m** en condiciones típicas.  
- **Cat6a**: **10 Gb/s** hasta **100 m** (mejor blindaje y separación).  
- *(Cat7/7a existen, suelen ser blindados y menos comunes en LAN estándar; en muchos casos Cat6a es suficiente.)*

**Aplicaciones**  
Conexión de **PCs, switches, routers, APs**, impresoras… en **redes internas (LAN)**.

**Ventajas**  
- Barato, flexible, fácil de crimpar e instalar.  
- Alimentación **PoE** posible (Power over Ethernet) para **APs**, cámaras, etc.

**Limitaciones**  
- Distancia típica **máxima 100 m** entre equipos de red.  
- Sensible a interferencias si el tendido es deficiente; en entornos ruidosos conviene **STP/FTP** y buena **puesta a tierra**.

---

#### Cable coaxial
Históricamente usado en redes locales (bus). Hoy se ve sobre todo en **operadores** (TV por cable / **DOCSIS**) y en **CCTV**.

- **Estructura**: conductor central, aislante, malla metálica (pantalla) y cubierta.  
- **Tipos** (según impedancia y uso): **75 Ω** (televisión/DOCSIS), **50 Ω** (radio, antenas).

---

<div style="text-align: center;">
  <img src="../imagenes/coaxial.jpeg" alt="Descripción de la imagen" style="display: block; margin: 0 auto; max-width: 100%; height: auto;">
</div>

---

**Ventajas**  
- Buena **inmunidad** al ruido, tiradas largas para señales específicas.

**Limitaciones**  
- Menos flexible para LAN modernas frente a UTP/fibra.  
- Conectores y equipos menos estándar en redes de usuario final.

---

#### Fibra óptica
Transmite **luz** en lugar de electricidad. Permite **altísimas velocidades** y **grandes distancias** con **inmunidad** a interferencias electromagnéticas.

- **Principio**: la luz se guía dentro de un núcleo por **reflexión interna**.
- **Tipos**:
  - **Monomodo (SMF, OS1/OS2)**: un solo “camino” de luz. Ideal para **largas distancias** (kilómetros a decenas de km).  
  - **Multimodo (MMF, OM1/OM2/OM3/OM4/OM5)**: varios “caminos”. Usado dentro de **edificios/campus**.

---

<div style="text-align: center;">
  <img src="../imagenes/fibra.jpeg" alt="Descripción de la imagen" style="display: block; margin: 0 auto; max-width: 100%; height: auto;">
</div>

---

- **Conectores** habituales: **LC**, **SC**.  
- **Transceptores**: SFP/SFP+/SFP28/QSFP… (se insertan en switches/routers para elegir **velocidad** y **alcance**).

**Ventajas**  
- **Muy alta velocidad** (10G, 25G, 40G, 100G…).  
- **Gran distancia** (decenas de km en monomodo).  
- **Inmune** a interferencias, no conduce electricidad.

**Limitaciones**  
- Más **coste** y **delicadeza** en conectorización (requiere limpieza y radio de curvatura adecuado).  
- No transporta **PoE** (no corriente).

---

#### Medios inalámbricos
Comunican por **radio** (o luz en IR). Dan **movilidad** y ahorran cableado.

- **Wi-Fi (802.11 a/b/g/n/ac/ax)**:  
  - Bandas **2,4 GHz** (más alcance, más interferencias) y **5 GHz** (más velocidad, menos alcance); **6 GHz** (Wi-Fi 6E) en equipos modernos.  
  - Uso típico: redes domésticas y de oficina para portátiles y móviles.  
  - **Seguridad**: **WPA2/WPA3**; evitar WEP y WPA antiguos.
- **Bluetooth**: corta distancia, periféricos.  
- **IR (infrarrojo)**: línea de visión, hoy minoritario en datos.  
- **LTE/4G/5G**: acceso **móvil** a Internet; útil como **backup** de la conexión fija o para ubicaciones sin cable.

**Ventajas**  
- Movilidad, despliegue rápido, sin obras.

**Limitaciones**  
- **Interferencias**, **canales** saturados, **paredes** que atenúan.  
- **Seguridad**: proteger con buenas contraseñas, cifrado y segmentación.  
- Rendimiento **variable** (distancia, obstáculos, usuarios simultáneos).

---

### 2.2 Hardware y dispositivos de red

#### Tarjeta de red (NIC)
Interfaz que conecta el equipo a la red (**Ethernet** o **Wi-Fi**).  
- Velocidades comunes en Ethernet: **1 Gb/s**, **2.5 Gb/s**, **10 Gb/s**.  
- En Wi-Fi: depende del estándar y de las **antenas** del AP y del cliente.

#### Concentradores (Hub)
Equipo antiguo que **repite** todo lo que recibe a **todos** los puertos.  
- **No** diferencia destinatarios; provoca **colisiones** y comparte ancho de banda.  
- Hoy está **en desuso**; se prefiere **switch**.

#### Conmutadores (Switch)
Dispositivo **capa 2** que reenvía tramas según la **tabla MAC** (puerto ↔ MAC).  
- **Full-duplex**, sin colisiones, mejor **rendimiento** que un hub.  
- Puede ser:
  - **No gestionable**: enchufar y listo (SOHO, aulas pequeñas).  
  - **Gestionable**: soporta **VLAN**, **QoS**, **Spanning Tree**, **port mirroring**, **PoE**, etc.  
- **Beneficios**: más **eficiencia**, **segmentación** (VLAN), priorizar tráfico (QoS), alimentar equipos por **PoE**.

#### Enrutadores (Router)
Equipo **capa 3** que une **redes distintas** y decide la **ruta** de los paquetes.  
- En casa/pyme suele incorporar **NAT**, **DHCP**, **firewall**, **Wi-Fi**.  
- En empresa puede separar **subredes**, aplicar **políticas** y conectar a Internet con redundancia.

#### Puntos de acceso (Access Point, AP)
Conecta dispositivos **inalámbricos** a la red cableada.  
- Puede ser un **AP autónomo** o formar parte de una **red gestionada** por un **controlador** (mejor roaming y canales coordinados).  
- A menudo alimentados por **PoE** (un solo cable para datos + energía).

#### Puentes (Bridge) y repetidores
- **Bridge**: une dos segmentos **capa 2**, filtrando por **MAC** (conceptualmente, un switch básico).  
- **Repetidor**: **amplifica/extiende** la señal (capa 1). En Wi-Fi, los “extensores” pueden **repetir** la red, aunque el rendimiento puede bajar si no se planifica bien.

#### Firewalls (visión básica)
Equipo o función que **filtra tráfico** según reglas (IP, puertos, protocolos).  
- Pueden ser **dispositivos dedicados** o funciones del **router**.  
- Nivel inicial: pensar en “**permitir/bloquear**” conexiones entrantes/salientes; en entornos web, suelen proteger el **perímetro** y segmentar zonas (DMZ).

---





