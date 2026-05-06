# Proyecto de Enrutamiento Linux - Redes de Computadoras 1

- Keitlyn Valentina Tunchez Castañeda
- 202201139

---

# Descripción del Proyecto

El proyecto consiste en implementar un entorno de red utilizando máquinas virtuales en VirtualBox, donde una máquina con Kali Linux funciona como router Linux entre dos redes distintas.

Se configuró:

- Una red Host-Only entre Windows y Kali Linux.
- Una red Internal Network entre Kali Linux y Ubuntu.
- Enrutamiento IP en Kali Linux.
- Rutas estáticas en Windows.
- Comunicación entre distintas subredes.

---

# Topología de Red

```text
Windows Host
192.168.59.1
        |
Host-Only Network
        |
Kali Linux Router
eth0 → 192.168.59.10
eth1 → 192.168.109.1
        |
Internal Network
        |
Ubuntu Client
192.168.109.20
```

---

# Direccionamiento IP

| Dispositivo | Interfaz | Dirección IP |
|---|---|---|
| Windows Host | VirtualBox Host-Only | 192.168.59.1 |
| Kali Linux | eth0 | 192.168.59.10 |
| Kali Linux | eth1 | 192.168.109.1 |
| Ubuntu Client | enp0s3 | 192.168.109.20 |

---

# Configuración Realizada

## Kali Linux

### Configuración de IPs

```bash
sudo ip addr add 192.168.59.10/24 dev eth0
sudo ip addr add 192.168.109.1/24 dev eth1
```

### Activación de interfaces

```bash
sudo ip link set eth0 up
sudo ip link set eth1 up
```

### Habilitación de IP Forwarding

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

### Configuración de iptables

```bash
sudo iptables -P FORWARD ACCEPT
```

---

## Ubuntu Client

### Configuración IP

```bash
sudo ip addr add 192.168.109.20/24 dev enp0s3
sudo ip link set enp0s3 up
```

### Configuración de Gateway

```bash
sudo ip route add default via 192.168.109.1
```

---

## Windows Host

### Configuración de ruta estática

```powershell
route -p add 192.168.109.0 mask 255.255.255.0 192.168.59.10
```

---

# Pruebas de Conectividad

## Ping desde Windows hacia Kali

```powershell
ping 192.168.59.10
```

## Ping desde Kali hacia Ubuntu

```bash
ping 192.168.109.20
```

## Ping desde Ubuntu hacia Windows

```bash
ping 192.168.59.1
```

## Ping desde Windows hacia Ubuntu

```powershell
ping 192.168.109.20
```

---

# Traceroute

```powershell
tracert 192.168.109.20
```

Resultado esperado:

```text
1   192.168.59.10
2   192.168.109.20
```

---

# Evidencias

## Capturas incluidas

### Configuración de adaptadores en VirtualBox

Kali adaptador 1

<img src="https://i.ibb.co/BK35gGQV/Captura-de-pantalla-2026-05-06-115106.png">

---

Kali adaptador 2

<img src="https://i.ibb.co/ZzjbCkDV/Captura-de-pantalla-2026-05-06-115144.png">

---

---

Ubuntu adaptador 1

<img src="https://i.ibb.co/CKdy8CdP/Captura-de-pantalla-2026-05-06-154105.png">

---

### Configuración IP en Kali Linux
<img src="https://i.ibb.co/21Fs8qYW/Captura-de-pantalla-2026-05-06-140337.png">

---

### Configuración IP en Ubuntu
<img src="https://i.ibb.co/6Jr8VrL8/Captura-de-pantalla-2026-05-06-134106.png">

---

### Configuración de rutas en Windows
<img src="https://i.ibb.co/7dXhN6vN/imagen-2026-05-06-154933738.png">

---



### Pruebas de ping
<img src="https://i.ibb.co/6cpHFKTn/Captura-de-pantalla-2026-05-06-140608.png">
<img src="https://i.ibb.co/tM99jmvd/Captura-de-pantalla-2026-05-06-142909.png">
<img src="https://i.ibb.co/jvYXZ6SM/Captura-de-pantalla-2026-05-06-143117.png">

---

### Resultado de traceroute
<img src="https://i.ibb.co/9HhxsnRX/Captura-de-pantalla-2026-05-06-155522.png">

---

# Conclusiones

- Se logró implementar correctamente un router Linux utilizando Kali Linux.
- Se configuró comunicación entre dos redes distintas utilizando rutas estáticas.
- Se comprobó el funcionamiento del enrutamiento mediante pruebas de conectividad y traceroute.
- El proyecto permitió comprender el funcionamiento básico del routing en Linux y el reenvío de paquetes entre interfaces.
