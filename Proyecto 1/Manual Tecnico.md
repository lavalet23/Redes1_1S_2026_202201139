# Manual Técnico  
## Proyecto 1 - NetCore Academy  
**Curso:** Redes de Computadoras 1  
**Universidad:** Universidad de San Carlos de Guatemala  
**Facultad:** Facultad de Ingeniería  
**Escuela:** Ciencias y Sistemas  
**Carné:** 202201139  

---

# 1. Introducción

El presente manual técnico documenta la implementación del proyecto **NetCore Academy**, desarrollado en Cisco Packet Tracer. La red fue diseñada a nivel de **capa 2**, integrando segmentación lógica mediante VLANs, propagación de VLANs con VTP, prevención de bucles con STP y redundancia con EtherChannel.

La topología está compuesta por **cuatro edificios** interconectados entre sí por medio de **fibra óptica**, mientras que internamente cada edificio utiliza enlaces troncales y puertos de acceso según el área funcional de cada dispositivo.

El objetivo principal fue construir una red segmentada, estable y documentada, donde:

- Los dispositivos de una misma VLAN sí pueden comunicarse.
- Los dispositivos de distintas VLANs no pueden comunicarse.
- SW-A1 actúa como **VTP Server** y **Root Bridge**.
- Se implementan enlaces redundantes con **EtherChannel**.
- Se evidencia el comportamiento de la capa física mediante hubs, repetidor y access points.

---
# Topología

La topología completa consta de 4 edificios los cuales se comunican por fibra óptica entre sí.

<p align="center">
    <img src="https://i.ibb.co/Gv6jdG0s/imagen-2026-04-10-001625167.png">
</p>

Luego tenemos las topologías internas a cada Edificio.

## Edificio A

<p align="center">
    <img src="https://i.ibb.co/39TnQGjy/imagen-2026-04-10-001910759.png">
</p>

## Edificio B

<p align="center">
    <img src="https://i.ibb.co/DDR084DS/imagen-2026-04-10-001956628.png">
</p>

## Edificio C

<p align="center">
    <img src="https://i.ibb.co/bMLMPhv4/imagen-2026-04-10-002049756.png">
</p>

## Edificio D

<p align="center">
    <img src="https://i.ibb.co/nq2bTb6L/imagen-2026-04-10-002134203.png">
</p>


# VLANs Creadas

Las VLAN creadas fueron 5 diferentes esparcidas alrededor de los 4 
edificios.

| Dispositivo    | Identificador |
|----------------|---------------|
| Administración | 19            |
| Docentes       | 29            |
| Biblioteca     | 39            |
| Laboratorio    | 49            |
| Visitantes     | 59            |

# Tabla de direcciones IP

## VLAN 19 - ADMIN

| Dispositivo | Tipo   | Ubicación   | IP           |
|------------|--------|-------------|--------------|
| Admin1     | Laptop | Edificio B  | 192.168.19.1 |
| Admin2     | PC     | Edificio A  | 192.168.19.2 |
| Admin3     | PC     | Edificio C  | 192.168.19.3 |
| Admin4     | PC     | Edificio D  | 192.168.19.4 |
| Admin5     | PC     | Edificio D  | 192.168.19.5 |

## VLAN 29 - DOCENTES

| Dispositivo | Tipo       | Ubicación   | IP            |
|------------|------------|-------------|---------------|
| Docentes1  | Smartphone | Edificio A  | 192.168.29.1  |
| Docentes2  | Laptop     | Edificio A  | 192.168.29.2  |
| Docentes3  | Laptop     | Edificio A  | 192.168.29.3  |
| Docentes6  | Laptop     | Edificio B  | 192.168.29.6  |
| Docentes7  | Laptop     | Edificio C  | 192.168.29.7  |
| Docentes8  | PC         | Edificio C  | 192.168.29.8  |
| Docentes9  | PC         | Edificio C  | 192.168.29.9  |
| Docentes10 | Server     | Edificio D  | 192.168.29.10 |

## VLAN 39 - BIBLIOTECA

| Dispositivo  | Tipo   | Ubicación   | IP            |
|-------------|--------|-------------|---------------|
| Biblioteca1 | PC     | Edificio B  | 192.168.39.1  |
| Biblioteca2 | Laptop | Edificio B  | 192.168.39.2  |
| Biblioteca3 | PC     | Edificio B  | 192.168.39.3  |
| Biblioteca4 | PC     | Edificio B  | 192.168.39.4  |
| Biblioteca5 | PC     | Edificio B  | 192.168.39.5  |
| Biblioteca6 | PC     | Edificio C  | 192.168.39.6  |
| Biblioteca7 | PC     | Edificio D  | 192.168.39.7  |

## VLAN 49 - LABORATORIO

| Dispositivo   | Tipo | Ubicación   | IP            |
|--------------|------|-------------|---------------|
| Laboratorio2 | PC   | Edificio A  | 192.168.49.2  |
| Laboratorio3 | PC   | Edificio D  | 192.168.49.3  |
| Laboratorio4 | PC   | Edificio A  | 192.168.49.4  |

## VLAN 59 - VISITANTES

| Dispositivo | Tipo | Ubicación   | IP            |
|------------|------|-------------|---------------|
| Visitante1 | PC   | Edificio D  | 192.168.59.1  |
| Visitante2 | PC   | Edificio D  | 192.168.59.2  |
| Visitante3 | PC   | Edificio D  | 192.168.59.3  |

# Configuracion Generales

## Access Point

Vamos a ingresar al AccessPoint y luego vamos a ir a la pestaña `Config` y `Port 1`, 
vamos a configurar los siguientes datos:  

- Cambiaremos el SSID de `Default` a cualquier otro, en el caso del Access Point del Edificio A usamos: `AC-A1`.
- En autenticación vamos a seleccionar `WPA2-PSK` y la PSK Pass Phrase será `proyecto12026`.

<p align="center">
    <img src="https://i.ibb.co/SDXdxPyP/imagen-2026-04-10-002847409.png">
</p>


# Comandos de configuración Switches

# Configuración General de Switches (Comandos)

Este bloque contiene únicamente los comandos utilizados de forma general en la configuración de switches del proyecto **NetCore Academy**, aplicados según el carnet **202201139**.

---

## Acceso al switch

```bash
enable
configure terminal
```
## Banner MOTD
```bash
banner motd #Bienvenido a [Nombre del Edificio] - NETCORE_202201139#
```
## Configuración VTP
```bash
Switch Servidor (Ej: SW-A1)

vtp version 2
vtp domain C3_NetCore
vtp password proyecto12026
vtp mode server

Switch Cliente

vtp version 2
vtp domain C3_NetCore
vtp password proyecto12026
vtp mode client

Switch Transparente (SW-E1)

vtp version 2
vtp domain C3_NetCore
vtp password proyecto12026
vtp mode transparent
```

## Creación de VLANs
```bash
vlan 19
name ADMIN
exit

vlan 29
name DOCENTES
exit

vlan 39
name BIBLIOTECA
exit

vlan 49
name LABORATORIO
exit

vlan 59
name VISITANTE
exit
```

## Configuración de puertos TRUNK
```bash
interface GigabitEthernet 0/1
switchport mode trunk
switchport trunk allowed vlan 19,29,39,49,59
exit
```
## Configuración de puertos ACCESS
```bash
interface FastEthernet 0/1
switchport mode access
switchport access vlan 19
exit
```
## EtherChannel (PAgP - Inter-edificios)
```bash
interface range FastEthernet 4/1 - 5/1
channel-group 1 mode desirable
exit
```
## EtherChannel (LACP - Intra-edificio)
```bash
interface range FastEthernet 0/4 - 0/5
channel-group 1 mode active
exit
```
## Configuración de Port-Channel
```bash
interface Port-channel 1
switchport mode trunk
switchport trunk allowed vlan 19,29,39,49,59
exit
```
## Configuración STP (Rapid-PVST)
```bash
spanning-tree mode rapid-pvst
spanning-tree vlan 19,29,39,49,59 root primary
spanning-tree vlan 19,29,39,49,59 priority 4096
```
## Guardar configuración
```bash
end
write memory
```
## Comandos de verificación
```bash
show vlan brief
show interfaces trunk
show etherchannel summary
show spanning-tree
show ip interface brief
```


# Tablas de dominios de Broadcast

Dado que el dominio de broadcast es el conjunto de dispositivos que reciben un mensaje de broadcast enviado por cualquiera de ellos. En redes con VLANs, cada VLAN es un dominio de broadcast separado, independientemente de cuántos switches físicos haya.

En nuestra topología se usan 5 VLANS por lo tanto tenemos 5 dominios de broadcast.  

| # | VLAN | Nombre      | Dispositivos                 | Total |
|---|------|-------------|------------------------------|-------|
| 1 | 19   | ADMIN       | Admin1 - Admin5              | 5     |
| 2 | 29   | DOCENTES    | Docentes1 - Docentes10       | 8     |
| 3 | 39   | BIBLIOTECA  | Biblioteca1 – Biblioteca7    | 7     |
| 4 | 49   | LABORATORIO | Laboratorio2 - Laboratorio4  | 3     |
| 5 | 59   | VISITANTES  | Visitante1 - Visitante3      | 3     |

**Nota**: En la VLAN de docentes no existen docentes4 y docentes5

# Tablas de dominios de colisión

Cada puerto access (con un dispositivo final conectado) es un dominio de colisión independiente. Los enlaces trunk entre switches también son dominios de colisión individuales, pero lo más relevante documentar son los puertos de acceso y los hubs (HUB-B1 y HUB-C1 crean un dominio de colisión compartido entre sus puertos).

| Switch   | Puerto/Enlace         | Dispositivo / Destino         | VLAN  | Dominio de Colisión  |
|----------|-----------------------|-------------------------------|-------|----------------------|
| SW-A3    | Fa0/1 (AC-A1)         | Docentes1 (Smartphone), Docentes2 (Laptop), Docentes3 (Laptop) | 24 | **Compartido (AP Wireless)** |
| SW-A2    | Fa0/4                 | Admin2                        | 19    | Independiente        |
| SW-A2    | Fa0/2                 | Laboratorio2                  | 49    | Independiente        |
| SW-A2    | Fa0/3                 | Laboratorio4                  | 49    | Independiente        |
| SW-A3    | Fa0/1                 | Access Point (Docentes1/2/3)  | 29    | Independiente        |
| SW-B3    | Fa0/1                 | Biblioteca1                   | 39    | Independiente        |
| SW-B3    | Fa0/2                 | Docentes6                     | 29    | Independiente        |
| SW-B4    | Fa0/1                 | Admin1                        | 19    | Independiente        |
| SW-B4    | Fa0/2                 | Biblioteca2                   | 39    | Independiente        |
| SW-B2    | Gi8/1 → HUB-B1        | Biblioteca3, Bib4, Bib5       | 39    | **Compartido (HUB)** |
| SW-C1    | Fa0/1                 | Docentes9                     | 29    | Independiente        |
| SW-C2    | Fa0/3 → HUB-C1        | (hacia SW-C1, SW-C3)          | Trunk | Compartido (HUB)     |
| SW-C2    | Fa0/2                 | Docentes7                     | 29    | Independiente        |
| SW-C2    | Fa0/1                 | Docentes8                     | 29    | Independiente        |
| SW-C3    | Fa0/2                | Biblioteca6                   | 39    | Independiente        |
| SW-C3    | Fa0/1                 | Admin3                        | 19    | Independiente        |
| SW-D3    | Fa0/1                 | Admin4                        | 19    | Independiente        |
| SW-D3    | Fa0/3                | Admin5                        | 19    | Independiente        |
| SW-D3    | Fa0/2                 | Docentes10                    | 29    | Independiente        |
| SW-D4    | Fa0/1                 | Laboratorio3                  | 49    | Independiente        |
| SW-D4    | Fa0/2                | Biblioteca7                   | 39    | Independiente        |
| SW-E1    | Gi0/2 (AC-D1)         | Visitante1, Visitante2, Visitante3 | 59 | **Compartido (AP Wireless)** |

# Capturas de pantalla

A continuación se presentan las capturas de pantalla de la 
ejecución de los comandos `show spanning-tree`, `show interface trunk` 
y de `show etherchannel summary`.  

## SW-A1 (Server)

### show spanning-tree

<p align="center">
    <img src="https://i.ibb.co/84fBkrBx/imagen-2026-04-10-010944435.png">
</p>

<p align="center">
    <img src="https://i.ibb.co/KdCTPqR/imagen-2026-04-10-011059735.png">
</p>

### show etherchannel summary

<p align="center">
    <img src="https://i.ibb.co/Ys3KgQs/imagen-2026-04-10-011525236.png">
</p>

### show interfaces trunk

<p align="center">
    <img src="https://i.ibb.co/bRFLqQbv/imagen-2026-04-10-011634819.png">
</p>

## SW-C4 (Cliente)

### show spanning-tree

<p align="center">
    <img src="https://i.ibb.co/Dgv6DM2b/imagen-2026-04-10-011848610.png">
</p>

<p align="center">
    <img src="https://i.ibb.co/5WtmJHwq/imagen-2026-04-10-011923252.png">
</p>

### show etherchannel summary

<p align="center">
    <img src="https://i.ibb.co/m51TQv5r/imagen-2026-04-10-012003979.png">
</p>

### show interfaces trunk

<p align="center">
    <img src="https://i.ibb.co/MxQh6TtT/imagen-2026-04-10-012134316.png">
</p>


# Pruebas de ping

## VLAN 19 - Administración

Ping Funcional de Admin1 - Admin4
Ping Fallido de Admin1 -Docencia7

<p align="center">
    <img src="https://i.ibb.co/r20J81sw/imagen-2026-04-10-012747318.png">
</p>

## VLAN 29 - Docentes

Ping Funcional de Docencia9 - Docencia8
Ping Fallido de Docencia9 - Biblioteca1

<p align="center">
    <img src="https://i.ibb.co/WN6FcDs5/imagen-2026-04-10-013251765.png">
</p>

## VLAN 39 - Biblioteca

Ping Funcional de Biblioteca7 - Biblioteca2
Ping Fallido de Biblioteca7 - Admin4

<p align="center">
    <img src="https://i.ibb.co/VpYFsyPZ/imagen-2026-04-10-013620034.png">
</p>

## VLAN 49 - Laboratorio

Ping Funcional de Laboratorio4 - Laboratorio3
Ping Fallido de Laboratorio4 - Docencia8

<p align="center">
    <img src="https://i.ibb.co/Hfc1dBx9/imagen-2026-04-10-013926232.png">
</p>

## VLAN 59 - Visitantes

Ping Funcional de Visitante1 - Visitante3
Ping Fallido de Visitante1 - Biblioteca5

<p align="center">
    <img src="https://i.ibb.co/b5dKthrj/imagen-2026-04-10-014139555.png">
</p>

# Presupuesto de Red – Proyecto Cisco Packet Tracer (Quetzales)

| # | Categoría | Descripción | Cant. | P. Unit. (Q) | Total (Q) |
|---|---|---|:---:|---:|---:|
| 1 | **Switches** | Switch Cisco PT (núcleo, fibra óptica) | 6 | Q9,300.00 | Q55,800.00 |
| 2 | **Switches** | Switch Cisco Catalyst 2960-24TT | 11 | Q2,945.00 | Q32,395.00 |
| 3 | **Conectividad** | Hub de red PT | 2 | Q348.75 | Q697.50 |
| 4 | **Conectividad** | Repetidor PT | 1 | Q271.25 | Q271.25 |
| 5 | **Conectividad** | AccessPoint PT | 2 | Q581.25 | Q1,162.50 |
| 6 | **Fibra OM3** | Cable fibra óptica OM3 (200 m) | 200 | Q27.13 | Q5,425.00 |
| 7 | **Fibra OM3** | Conectores LC/SC (par) | 24 | Q62.00 | Q1,488.00 |
| 8 | **Fibra OM3** | Patch panel fibra 24p | 2 | Q930.00 | Q1,860.00 |
| 9 | **Cobre Cat6** | Cable UTP Cat6 (caja 305 m) | 3 | Q736.25 | Q2,208.75 |
| 10 | **Cobre Cat6** | Conectores RJ-45 Cat6 (x100) | 2 | Q139.50 | Q279.00 |
| 11 | **Cobre Cat6** | Panel de parcheo Cat6 24p | 4 | Q503.75 | Q2,015.00 |
| 12 | **Cobre Cat5e** | Cable UTP Cat5e (caja 305 m) | 2 | Q503.75 | Q1,007.50 |
| 13 | **Cobre Cat5e** | Conectores RJ-45 Cat5e (x100) | 2 | Q93.00 | Q186.00 |
| 14 | **Dispositivos** | PC de escritorio | 18 | Q4,030.00 | Q72,540.00 |
| 15 | **Dispositivos** | Laptop | 6 | Q5,812.50 | Q34,875.00 |
| 16 | **Dispositivos** | Smartphone | 1 | Q1,937.50 | Q1,937.50 |
| 17 | **Dispositivos** | Servidor de red | 1 | Q17,050.00 | Q17,050.00 |
| 18 | **Infraestructura** | Rack de pared 12U | 2 | Q1,395.00 | Q2,790.00 |
| 19 | **Infraestructura** | UPS 1500VA | 2 | Q2,480.00 | Q4,960.00 |
| 20 | **Infraestructura** | PDU + organizadores | 6 | Q310.00 | Q1,860.00 |
| 21 | **Software** | Licencia Cisco IOS (x switch 2960) | 11 | Q1,162.50 | Q12,787.50 |
| 22 | **Software** | Antivirus (PCs + laptops, 1 año) | 24 | Q232.50 | Q5,580.00 |
| | | | | **TOTAL** | **Q266,975.50** |


# Conclusiones

1. La implementación de VLANs permitió segmentar la red y reducir el dominio de broadcast, mejorando la organización y el rendimiento.

2. El uso de VTP facilitó la administración centralizada de las VLANs entre los switches.

3. La configuración de enlaces troncales permitió transportar múltiples VLANs entre switches de forma eficiente.

4. Rapid-PVST aseguró la estabilidad de la red al evitar bucles y permitir una rápida convergencia.

5. EtherChannel proporcionó mayor capacidad y redundancia en los enlaces, mejorando la disponibilidad de la red.

6. En general, el proyecto permitió aplicar de forma práctica conceptos de capa 1 y capa 2, logrando una red funcional, segmentada y estable.
