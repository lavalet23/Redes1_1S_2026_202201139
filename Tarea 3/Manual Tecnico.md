# UNIVERSIDAD DE SAN CARLOS DE GUATEMALA  
## Facultad de Ingeniería  
## Escuela de Ciencias y Sistemas  

---

# TAREA 3  
# Configuración de VLANs y VTP en Red LAN  

---

### Curso:
Redes de Computadoras 1  

### Estudiante:
Keitlyn Valentina Tunchez Castañeda  

### Carnet:
202201139  

### Fecha de entrega:
27 de Febrero de 2026  

---

# 1. Introducción

En la presente práctica se implementó una red LAN segmentada mediante el uso de VLANs (Virtual Local Area Networks) y el protocolo VTP (VLAN Trunking Protocol) utilizando el simulador Cisco Packet Tracer.

El objetivo fue dividir la red en segmentos lógicos independientes, mejorando la organización, seguridad y administración del tráfico. Además, se utilizó VTP para centralizar la creación y propagación de VLANs entre los switches.

---

# 2. Objetivo del Proyecto

Implementar una red LAN utilizando VLANs y VTP, garantizando comunicación entre dispositivos de la misma VLAN y aislamiento entre diferentes VLANs.

---

# 3. Conceptos Teóricos

## 3.1 VLAN (Virtual Local Area Network)

Una VLAN permite segmentar una red física en múltiples redes lógicas independientes.

### Beneficios:
- Reduce tráfico broadcast
- Mejora seguridad
- Facilita la administración
- Permite organización por departamentos

---

## 3.2 Tipos de Puertos

### Modo Access
- Se utiliza para conectar dispositivos finales
- Pertenece a una sola VLAN

### Modo Trunk
- Se utiliza entre switches
- Transporta múltiples VLANs
- Usa etiquetado 802.1Q

---

## 3.3 VTP (VLAN Trunking Protocol)

Permite compartir información de VLANs entre switches dentro de un mismo dominio.

### Modos:

- Server: crea y distribuye VLANs  
- Client: recibe VLANs  
- Transparent: maneja VLANs localmente  

---

# 4. Topología de la Red

La red está compuesta por:

- 4 switches Cisco 2960:
  - 1 CORE (Servidor VTP)
  - 2 Clientes (MERCA y VENTAS)
  - 1 Transparente (ADMIN)

- 6 computadoras

### VLANs:

- VLAN 10 → ADMIN  
- VLAN 20 → MERCA  
- VLAN 30 → VENTAS  

---

# 5. Configuración de la Red

## 5.1 Configuración de VTP

### CORE (Server)

```bash
conf t
vtp version 2
vtp domain Redes1
vtp password semana5
vtp mode server
```

---

### MERCA y VENTAS (Client)

```bash
conf t
vtp version 2
vtp domain Redes1
vtp password semana5
vtp mode client
```

---

### ADMIN (Transparent)

```bash
conf t
vtp version 2
vtp domain Redes1
vtp password semana5
vtp mode transparent
```

---

## 5.2 Creación de VLANs

```bash
conf t
vlan 10
 name ADMIN
vlan 20
 name MERCA
vlan 30
 name VENTAS
```

---

## 5.3 Configuración de Trunks

```bash
interface fa0/x
switchport mode trunk
switchport trunk allowed vlan 10,20,30
```

---

## 5.4 Configuración de Access

```bash
interface fa0/x
switchport mode access
switchport access vlan X
```

---

# 6. Configuración de Direccionamiento IP

### VLAN 10 – ADMIN
- PC0 → 192.168.10.10  

### VLAN 20 – MERCA
- PC1 → 192.168.20.10  
- PC2 → 192.168.20.20

### VLAN 30 – VENTAS
- PC3 → 192.168.30.10  
- PC4 → 192.168.30.20
- PC5 → 192.168.30.30 

Máscara:
```
255.255.255.0
```

---

# 7. Verificación

```bash
show vlan brief
show vtp status
show interfaces trunk
```

---

# 8. Pruebas de Conectividad

## 8.1 Misma VLAN

- 4 enviados
- 4 recibidos
- 0% pérdida

✔ Correcto

---

## 8.2 Diferente VLAN

- 4 enviados
- 0 recibidos
- 100% pérdida

✔ Correcto (aislamiento)

---

# 9. Análisis

- VLANs segmentan correctamente la red
- VTP distribuye VLANs automáticamente
- Trunks permiten comunicación entre switches
- No hay comunicación entre VLANs (no hay router)

---

# 10. Conclusiones

- Se implementaron correctamente VLANs
- VTP funcionó correctamente
- Se logró aislamiento entre redes
- La red es escalable y organizada

---

# 11. Anexos

- Topología  
![PING 1](https://i.ibb.co/YFnGJBp4/Captura-de-pantalla-2026-02-26-175453.png)

- Pings  

    Prueba de Ping 1 (Misma VLAN) - PC1 a PC2 
![PING 1](https://i.ibb.co/v6Jg51fL/Captura-de-pantalla-2026-02-26-174458.png) 

    Prueba de Ping 2 (Diferente VLAN) - PC0 a PC3 
![PING 1](https://i.ibb.co/9m1G5JQK/Captura-de-pantalla-2026-02-26-175010.png)

- Comandos show  

    Comando "show vlan brief"
![PING 1](https://i.ibb.co/HTChvLqV/Captura-de-pantalla-2026-02-26-175856.png)

    Comando "show vtp status"
![PING 1](https://i.ibb.co/kgcxMHLL/Captura-de-pantalla-2026-02-26-175913.png)

    Comando "show interfaces trunk"
![PING 1](https://i.ibb.co/6cKhPwGd/Captura-de-pantalla-2026-02-26-175931.png)
