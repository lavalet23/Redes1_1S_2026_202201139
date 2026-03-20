# Manual Técnico - Proyecto 1  
## NetCore Academy  

---

## Información General

- **Curso:** Redes de Computadoras 1  
- **Proyecto:** NetCore Academy  
- **Estudiante:** Keitlyn Valentina Tunchez Castañeda  
- **Carnet:** 202201139 
- **Fecha:** 19/03/2026  

---

## Objetivo

Diseñar e implementar una red de área local (LAN) basada en las capas física y de enlace de datos del modelo OSI, aplicando técnicas de segmentación, redundancia y optimización del tráfico mediante el uso de VLANs, VTP, STP y EtherChannel.

---

## Descripción General de la Solución

Se desarrolló una infraestructura de red para un campus académico compuesto por múltiples edificios interconectados. La solución propone una topología jerárquica que permite mejorar el rendimiento, la organización del tráfico y la disponibilidad del servicio.

El diseño contempla el uso de diferentes medios de transmisión según el nivel de la red, así como la segmentación lógica mediante VLANs para separar el tráfico de acuerdo con las áreas funcionales del campus.

---

## Diseño de la Topología

> Insertar imagen de la topología general

La red se estructura en tres niveles principales:

- **Nivel de núcleo/interconexión:** Comunicación entre edificios mediante enlaces de fibra óptica.
- **Nivel de distribución:** Interconexión de switches dentro de cada edificio.
- **Nivel de acceso:** Conexión de dispositivos finales como computadoras, laptops y puntos de acceso inalámbricos.

Este enfoque permite escalabilidad, mejor administración y control del tráfico.

---

## Segmentación de la Red (VLANs)

Se implementó segmentación lógica mediante VLANs para separar el tráfico según el tipo de usuario o área de trabajo.

| Área | VLAN ID | Nombre |
|------|--------|--------|
| Administración | 1X | ADMIN |
| Docencia | 2X | DOCENTES |
| Biblioteca | 3X | BIBLIOTECA |
| Laboratorio | 4X | LABORATORIO |
| Visitantes | 5X | VISITANTES |

> Nota: X representa el último dígito del carnet.

Cada VLAN funciona como un dominio de broadcast independiente, lo que reduce el tráfico innecesario y mejora la seguridad.

---

## Esquema de Direccionamiento IP

Se utilizó una red base privada con direccionamiento estático asignado manualmente a los dispositivos finales.

```
192.168.1X.0/24
```

La asignación de direcciones se realizó en función de la VLAN correspondiente, asegurando que los dispositivos únicamente puedan comunicarse dentro de su misma red lógica.

---

## Medios de Transmisión y Tipos de Enlace

| Tipo de Enlace | Medio | Aplicación |
|---------------|------|-----------|
| 100Base-FX | Fibra óptica | Interconexión entre edificios |
| GigabitEthernet | UTP Cat6 | Enlaces troncales |
| FastEthernet | UTP Cat5e | Acceso a dispositivos finales |

El uso de fibra óptica permite mayor alcance y menor interferencia, mientras que el cableado UTP se utiliza en niveles internos por su practicidad.

---

## Configuración de VLANs

```bash
enable
configure terminal

vlan 10
name ADMIN

vlan 20
name DOCENTES

vlan 30
name BIBLIOTECA

vlan 40
name LABORATORIO

vlan 50
name VISITANTES
```

---

## Configuración del Protocolo VTP

### Switch en modo servidor

```bash
vtp mode server
vtp domain C#_NetCore
vtp password proyecto12026
```

### Switches en modo cliente

```bash
vtp mode client
vtp domain C#_NetCore
vtp password proyecto12026
```

### Switch en modo transparente

```bash
vtp mode transparent
```

El uso de VTP permite la propagación automática de las VLANs a través de la red.

---

## Configuración de Enlaces Troncales

```bash
interface fa0/1
switchport mode trunk
switchport trunk allowed vlan all
```

Los enlaces troncales permiten el transporte de múltiples VLANs entre switches.

---

## Configuración del Protocolo STP

```bash
spanning-tree mode rapid-pvst
spanning-tree vlan 1-50 priority 4096
```

Se estableció un switch como puente raíz con el fin de evitar bucles en la red y garantizar la estabilidad de la topología.

---

## Configuración de EtherChannel

```bash
interface range fa0/1 - 2
channel-group 1 mode active

interface port-channel 1
switchport mode trunk
```

EtherChannel permite agrupar múltiples enlaces físicos en uno lógico, aumentando el ancho de banda y proporcionando redundancia.

---

## Configuración de Puertos de Acceso

```bash
interface fa0/10
switchport mode access
switchport access vlan 20
```

Cada puerto de acceso se asigna a una VLAN específica según el tipo de dispositivo conectado.

---

## Configuración de Access Point

Los puntos de acceso se integran a la red mediante un puerto configurado en modo access. Su función es permitir la conexión inalámbrica de dispositivos, los cuales se integran a la VLAN correspondiente a través del switch.

---

## Seguridad Básica

```bash
banner motd # Bienvenido a [Edificio] - NETCORE_[Carnet] #
```

Se configuró un mensaje de bienvenida para identificar los equipos dentro de la red.

---

## Pruebas de Conectividad

Se realizaron pruebas para validar el correcto funcionamiento de la red:

- Comunicación exitosa entre dispositivos dentro de la misma VLAN.
- Bloqueo de comunicación entre dispositivos de diferentes VLANs.

> Insertar capturas de pruebas de ping

---

## Comandos de Verificación

```bash
show spanning-tree
show etherchannel summary
show interfaces trunk
```

Estos comandos permiten validar el estado de los protocolos y enlaces configurados.

---

## Análisis de Dominios

- Cada VLAN representa un dominio de broadcast independiente.
- Los switches segmentan los dominios de colisión por puerto.
- Los dispositivos como hubs generan dominios de colisión compartidos.

---

## Presupuesto Estimado

| Equipo | Cantidad | Precio |
|-------|--------|--------|
| Switches | [Cantidad] | [Precio] |
| Cable UTP | [Cantidad] | [Precio] |
| Fibra óptica | [Cantidad] | [Precio] |

---

## Archivo del Proyecto

- **Nombre del archivo:** Proyecto1_[Carnet].pkt  
- **Herramienta utilizada:** Cisco Packet Tracer  

---

## Conclusiones

La implementación de segmentación mediante VLANs permitió organizar el tráfico de la red de manera eficiente. La integración de protocolos como STP y EtherChannel contribuyó a la estabilidad y redundancia de la infraestructura.

El diseño propuesto facilita la administración de la red y establece una base sólida para futuras ampliaciones o integración de servicios adicionales.

---

## Observaciones Finales

- La red opera exclusivamente en capa 2.
- No se implementó enrutamiento entre VLANs.
- Se validó el cumplimiento de los requerimientos mediante pruebas de conectividad.

---
