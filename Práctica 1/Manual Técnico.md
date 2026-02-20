# UNIVERSIDAD DE SAN CARLOS DE GUATEMALA  
## Facultad de Ingeniería  
## Escuela de Ciencias y Sistemas  

---

# PRÁCTICA 1  
# Diseño e Implementación de Red LAN  

---

### Curso:
Redes de Computadoras 1  

### Estudiante:
Keitlyn Valentina Tunchez Castañeda  

### Carnet:
202201139  

### Red asignada:
192.178.39.0/24  

### Fecha de entrega:
19 de febrero de 2026  

---

# 1. Introducción

El presente documento describe el diseño e implementación de una red LAN para la empresa Constructiva S.A., desarrollada en el simulador Cisco Packet Tracer.

El objetivo principal fue diseñar una infraestructura de red funcional distribuida en tres niveles, aplicando correctamente:

- Direccionamiento IPv4 estático.
- Configuración básica de switches Cisco 2960 mediante CLI.
- Estándar de cableado estructurado TIA/EIA-568B.
- Organización visual por departamentos.
- Verificación de conectividad mediante pruebas de ping y simulación de paquetes ARP e ICMP.

---

# 2. Objetivo del Proyecto

Diseñar e implementar una red LAN completamente funcional para un edificio corporativo de tres niveles, garantizando conectividad total entre dispositivos y una correcta organización física y lógica de la red.

---

# 3. Información de Red

- ID de red: 192.178.39.0
- Máscara de subred: 255.255.255.0
- Rango válido de hosts: 192.178.39.1 – 192.178.39.254
- Dirección de broadcast: 192.178.39.255
- Tipo de direccionamiento: Estático
- Topología: LAN plana (sin segmentación VLAN)

Total de dispositivos configurados: **60**

- 54 computadoras
- 6 servidores

---

# 4. Distribución de Dispositivos

## Piso 1 – Recepción y Administración

- Recepción: 11 computadoras + 1 servidor
- Contabilidad: 8 computadoras
- Legal: 5 computadoras
- Sala de reuniones: 5 computadoras

Total Piso 1: 30 dispositivos

---

## Piso 2 – Arquitectura y Urbanismo

- Arquitectura: 6 computadoras
- Urbanismo: 5 computadoras + 1 servidor
- Sala de revisión de planos: 5 computadoras

Total Piso 2: 17 dispositivos

---

## Piso 3 – Ingeniería y Dirección

- Dirección General: 4 computadoras
- Ingeniería Civil: 5 computadoras + 1 servidor
- Servidores principales: 3 servidores

Total Piso 3: 13 dispositivos

---

# 5. Tabla Completa de Direcciones IP

# PISO 1 – RECEPCIÓN Y ADMINISTRACIÓN

## Recepción

| Dispositivo | Dirección IP | Máscara |
|------------|-------------|----------|
| RECEP1 | 192.178.39.1 | 255.255.255.0 |
| RECEP2 | 192.178.39.2 | 255.255.255.0 |
| RECEP3 | 192.178.39.3 | 255.255.255.0 |
| RECEP4 | 192.178.39.4 | 255.255.255.0 |
| RECEP5 | 192.178.39.5 | 255.255.255.0 |
| RECEP6 | 192.178.39.6 | 255.255.255.0 |
| RECEP7 | 192.178.39.7 | 255.255.255.0 |
| RECEP8 | 192.178.39.8 | 255.255.255.0 |
| RECEP9 | 192.178.39.9 | 255.255.255.0 |
| RECEP10 | 192.178.39.10 | 255.255.255.0 |
| RECEP11 | 192.178.39.11 | 255.255.255.0 |
| RECEP_SERV | 192.178.39.20 | 255.255.255.0 |

---

## Contabilidad

| Dispositivo | Dirección IP | Máscara |
|------------|-------------|----------|
| CONTA1 | 192.178.39.21 | 255.255.255.0 |
| CONTA2 | 192.178.39.22 | 255.255.255.0 |
| CONTA3 | 192.178.39.23 | 255.255.255.0 |
| CONTA4 | 192.178.39.24 | 255.255.255.0 |
| CONTA5 | 192.178.39.25 | 255.255.255.0 |
| CONTA6 | 192.178.39.26 | 255.255.255.0 |
| CONTA7 | 192.178.39.27 | 255.255.255.0 |
| CONTA8 | 192.178.39.28 | 255.255.255.0 |

---

## Legal

| Dispositivo | Dirección IP | Máscara |
|------------|-------------|----------|
| LEGAL1 | 192.178.39.31 | 255.255.255.0 |
| LEGAL2 | 192.178.39.32 | 255.255.255.0 |
| LEGAL3 | 192.178.39.33 | 255.255.255.0 |
| LEGAL4 | 192.178.39.34 | 255.255.255.0 |
| LEGAL5 | 192.178.39.35 | 255.255.255.0 |

---

## Reuniones

| Dispositivo | Dirección IP | Máscara |
|------------|-------------|----------|
| REUNIONES1 | 192.178.39.41 | 255.255.255.0 |
| REUNIONES2 | 192.178.39.42 | 255.255.255.0 |
| REUNIONES3 | 192.178.39.43 | 255.255.255.0 |
| REUNIONES4 | 192.178.39.44 | 255.255.255.0 |
| REUNIONES5 | 192.178.39.45 | 255.255.255.0 |

---

# PISO 2 – ARQUITECTURA Y URBANISMO

## Arquitectura

| Dispositivo | Dirección IP | Máscara |
|------------|-------------|----------|
| ARQUI1 | 192.178.39.51 | 255.255.255.0 |
| ARQUI2 | 192.178.39.52 | 255.255.255.0 |
| ARQUI3 | 192.178.39.53 | 255.255.255.0 |
| ARQUI4 | 192.178.39.54 | 255.255.255.0 |
| ARQUI5 | 192.178.39.55 | 255.255.255.0 |
| ARQUI6 | 192.178.39.56 | 255.255.255.0 |

---

## Urbanismo

| Dispositivo | Dirección IP | Máscara |
|------------|-------------|----------|
| URBA1 | 192.178.39.61 | 255.255.255.0 |
| URBA2 | 192.178.39.62 | 255.255.255.0 |
| URBA3 | 192.178.39.63 | 255.255.255.0 |
| URBA4 | 192.178.39.64 | 255.255.255.0 |
| URBA5 | 192.178.39.65 | 255.255.255.0 |
| URBA_SERV | 192.178.39.70 | 255.255.255.0 |

---

## Planos

| Dispositivo | Dirección IP | Máscara |
|------------|-------------|----------|
| PLANOS1 | 192.178.39.71 | 255.255.255.0 |
| PLANOS2 | 192.178.39.72 | 255.255.255.0 |
| PLANOS3 | 192.178.39.73 | 255.255.255.0 |
| PLANOS4 | 192.178.39.74 | 255.255.255.0 |
| PLANOS5 | 192.178.39.75 | 255.255.255.0 |

---

# PISO 3 – INGENIERÍA Y DIRECCIÓN

## Dirección General

| Dispositivo | Dirección IP | Máscara |
|------------|-------------|----------|
| DIRECCION1 | 192.178.39.81 | 255.255.255.0 |
| DIRECCION2 | 192.178.39.82 | 255.255.255.0 |
| DIRECCION3 | 192.178.39.83 | 255.255.255.0 |
| DIRECCION4 | 192.178.39.84 | 255.255.255.0 |

---

## Ingeniería Civil

| Dispositivo | Dirección IP | Máscara |
|------------|-------------|----------|
| INGENIERIA1 | 192.178.39.91 | 255.255.255.0 |
| INGENIERIA2 | 192.178.39.92 | 255.255.255.0 |
| INGENIERIA3 | 192.178.39.93 | 255.255.255.0 |
| INGENIERIA4 | 192.178.39.94 | 255.255.255.0 |
| INGENIERIA5 | 192.178.39.95 | 255.255.255.0 |
| INGENIERIA_SERV | 192.178.39.100 | 255.255.255.0 |

---

## Servidores Principales

| Dispositivo | Dirección IP | Máscara |
|------------|-------------|----------|
| SERVER_1 | 192.178.39.101 | 255.255.255.0 |
| SERVER_2 | 192.178.39.102 | 255.255.255.0 |
| SERVER_3 | 192.178.39.103 | 255.255.255.0 |

---

# 6. Configuración de Switches

Se configuraron todos los switches Cisco 2960 mediante CLI.
cccc
Configuración aplicada:

```bash
enable
configure terminal
hostname Ingenieria
enable secret 202201139
line console 0
password 202201139
login
exit
service password-encryption
end
write memory
```

---

# 7. Configuración de VPCs 

Para validar la correcta asignación de direccionamiento IP estático, se realizó la configuración manual de los equipos desde:

Desktop → IP Configuration

En cada equipo se configuró:

- Dirección IP correspondiente
- Máscara de subred: 255.255.255.0
- Gateway: No configurado (red LAN plana sin router)

A continuación, se presentan las evidencias de configuración en 10 áreas representativas de la red:


## 7.1 Configuración de VPCs (Recep, Conta, Legal, Reuniones, Arqui)
![Configuración IP 1](https://i.ibb.co/KpNSdLLx/Captura-de-pantalla-2026-02-19-180550.png)

---

## 7.2 Configuración de VPCs (Urba, Planos, Dirección, Ingeniería, Servidores)
![Configuración IP 2](https://i.ibb.co/Df0Z3gfs/Captura-de-pantalla-2026-02-19-180810.png)


---

# 8. Pruebas de Conectividad 

Se realizaron pruebas de conectividad mediante el comando `ping` desde el símbolo del sistema de cada equipo.

En todos los casos se verificó:

- 4 paquetes enviados
- 4 paquetes recibidos
- 0% de pérdida

Lo que confirma conectividad total en la red LAN.

A continuación, se presentan las evidencias de 10 pings entre dispositivos de la red:

## 8.1 Ping – LEGAL1 →  URBA3
![Ping 1](https://i.ibb.co/pvms897x/Captura-de-pantalla-2026-02-19-162430.png)

---

## 8.2 Ping – RECEP1 →  LEGAL3
![Ping 2](https://i.ibb.co/sdgSmyyz/Captura-de-pantalla-2026-02-19-162926.png)

---

## 8.3 Ping – RECEP_SERV →  PLANOS1

![Ping 3](https://i.ibb.co/Y7tsn2bF/Captura-de-pantalla-2026-02-19-163424.png)

---

## 8.4 Ping – CONTA8 →  CONTA7

![Ping 4](https://i.ibb.co/fTN4DXb/Captura-de-pantalla-2026-02-19-163535.png)

---

## 8.5 Ping – INGENIERIA2 →  RECEP11
![Ping 5](https://i.ibb.co/KpF74p7L/Captura-de-pantalla-2026-02-19-163947.png)

---

## 8.6 Ping – URBA_SERV →  SERVER_2
![Ping 6](https://i.ibb.co/209dSk0c/Captura-de-pantalla-2026-02-19-164125.png)

---

## 8.7 Ping – SERVER_3 →  URBA5

![Ping 7](https://i.ibb.co/B50fDS5Y/Captura-de-pantalla-2026-02-19-164237.png)

---

## 8.8 Ping – URBA1 →  SERVER_1
![Ping 8](https://i.ibb.co/p65J25XR/Captura-de-pantalla-2026-02-19-164643.png)

---

## 8.9 Ping – PLANOS4 →  CONTA5

![Ping 9](https://i.ibb.co/7drdRMXj/Captura-de-pantalla-2026-02-19-164936.png)

---

## 8.10 Ping – DIRECCION4 →  ARQUI5

![Ping 10](https://i.ibb.co/mFFgkrFm/Captura-de-pantalla-2026-02-19-184947.png)

---

# 9. Análisis en Modo Simulación – Protocolos ARP e ICMP

Para analizar el comportamiento interno de la red, se utilizó el modo **Simulation** de Cisco Packet Tracer.

Se observó el proceso de resolución de direcciones MAC mediante ARP y la posterior transmisión del paquete ICMP.

---

# 10. Conclusiones

- Se implementó correctamente la red LAN solicitada.
- Se aplicó direccionamiento IPv4 estático sin conflictos.
- Todos los dispositivos presentan conectividad total.
- Se verificó el funcionamiento correcto de los protocolos ARP e ICMP.
- La práctica cumple con los requerimientos establecidos en el documento guía.

