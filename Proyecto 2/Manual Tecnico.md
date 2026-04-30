# Manual Técnico  
## Proyecto 2 - Enrutamiento Multi-Sede  
**Curso:** Redes de Computadoras 1  
**Universidad:** Universidad de San Carlos de Guatemala  
**Facultad:** Facultad de Ingeniería  
**Escuela:** Ciencias y Sistemas  
**Carné:** 202201139  

---

# 1. Introducción

El presente manual técnico documenta la implementación del **Proyecto 2 de Redes**, desarrollado en Cisco Packet Tracer. El proyecto consiste en la creación de una red multi-sede en la cual se aplican conceptos de direccionamiento IP, enrutamiento dinámico, rutas estáticas y redistribución entre protocolos.

A diferencia de un proyecto enfocado únicamente en capa 2, este proyecto trabaja principalmente la **capa 3 del modelo OSI**, ya que se configuraron routers para permitir la comunicación entre diferentes redes. Para lograrlo, se utilizaron protocolos de enrutamiento como **OSPF, EIGRP y RIP**, además de rutas estáticas en puntos específicos de la topología.

El objetivo principal fue lograr que todos los dispositivos finales pudieran comunicarse correctamente, aunque sus redes estuvieran administradas por diferentes protocolos de enrutamiento. Para esto fue necesario configurar correctamente las interfaces, anunciar redes, aplicar redistribución de rutas y validar la conectividad mediante comandos de diagnóstico y pruebas de ping.

---

# 2. Objetivos

## 2.1 Objetivo general

Implementar una red multi-sede funcional en Cisco Packet Tracer, aplicando protocolos de enrutamiento dinámico, rutas estáticas y redistribución de rutas para permitir la comunicación completa entre todas las redes del proyecto.

## 2.2 Objetivos específicos

- Diseñar una topología de red que conecte varias sedes mediante routers.
- Configurar el direccionamiento IP en routers y dispositivos finales.
- Implementar el protocolo OSPF en la sección correspondiente de la red.
- Implementar el protocolo EIGRP en la sección correspondiente de la red.
- Implementar el protocolo RIP en la sección correspondiente de la red.
- Configurar rutas estáticas donde sea necesario.
- Aplicar redistribución entre protocolos de enrutamiento.
- Verificar las tablas de enrutamiento en cada router.
- Comprobar la conectividad entre redes mediante pruebas de ping.
- Documentar los comandos utilizados y las pruebas realizadas.

---

# 3. Descripción general del proyecto

El Proyecto 2 consiste en una red formada por varias sedes conectadas entre sí mediante routers. Cada sede contiene su propia red local y está asociada a un protocolo de enrutamiento específico.

En la topología se trabajaron diferentes dominios de enrutamiento. Esto significa que una parte de la red funciona con OSPF, otra con EIGRP, otra con RIP y otra puede utilizar rutas estáticas. Para que todas estas redes pudieran comunicarse entre sí, fue necesario configurar redistribución en los routers que conectan diferentes protocolos.

La redistribución permitió que las rutas aprendidas por un protocolo fueran compartidas con los demás. De esta forma, una red aprendida por OSPF pudo ser conocida por EIGRP o RIP, y viceversa.

---

# 4. Herramientas utilizadas

| Herramienta | Descripción |
|------------|-------------|
| Cisco Packet Tracer | Simulador utilizado para crear y configurar la red |
| Routers Cisco | Dispositivos encargados del enrutamiento entre redes |
| Switches Cisco | Dispositivos utilizados para conectar equipos finales |
| PCs | Dispositivos finales utilizados para realizar pruebas de conectividad |
| CLI de Cisco | Consola utilizada para la configuración de routers y switches |

---

# 5. Topología

La topología del proyecto está formada por varias sedes conectadas entre sí. Cada sede cuenta con una red LAN y un router encargado de comunicarla con el resto de la infraestructura.

La red fue organizada de forma que cada sección utilizara un método de enrutamiento distinto, permitiendo practicar la convivencia entre protocolos.

<p align="center">
    <img src="https://i.ibb.co/zhknMZXz/imagen-2026-04-29-171526004.png">
</p>

---

# 6. Dispositivos utilizados

| Dispositivo | Función dentro de la red |
|------------|---------------------------|
| R-CEN | Router central o principal de la topología |
| Router OSPF | Router encargado del dominio OSPF |
| Router EIGRP | Router encargado del dominio EIGRP |
| Router RIP | Router encargado del dominio RIP |
| Router de rutas estáticas | Router o sección donde se configuraron rutas manuales |
| Switches de acceso | Conectan los dispositivos finales de cada sede |
| PCs | Equipos utilizados para probar conectividad |


---

# 7. Tabla de direccionamiento IP

En el proyecto se utilizaron redes privadas para identificar las diferentes LAN y los enlaces punto a punto entre routers.

## 7.1 Redes LAN

| Red | Dirección de red | Máscara | Gateway sugerido | Protocolo asociado |
|-----|------------------|---------|------------------|--------------------|
| LAN Central | 192.168.10.0 | 255.255.255.0 | 192.168.10.1 | Core / Redistribución |
| LAN OSPF | 192.168.20.0 | 255.255.255.0 | 192.168.20.1 | OSPF |
| LAN EIGRP | 192.168.30.0 | 255.255.255.0 | 192.168.30.1 | EIGRP |
| LAN RIP | 192.168.40.0 | 255.255.255.0 | 192.168.40.1 | RIP |
| LAN Estática | 192.168.50.0 | 255.255.255.0 | 192.168.50.1 | Ruta estática |

## 7.2 Enlaces entre routers

| Enlace | Red | Máscara | Uso |
|-------|-----|---------|-----|
| Enlace 1 | 10.0.0.0 | 255.255.255.252 | Conexión entre routers |
| Enlace 2 | 10.0.0.4 | 255.255.255.252 | Conexión entre routers |
| Enlace 3 | 10.0.0.8 | 255.255.255.252 | Conexión entre routers |
| Enlace 4 | 10.0.0.12 | 255.255.255.252 | Conexión entre routers |



---

# 8. Configuración básica de routers

Antes de configurar los protocolos de enrutamiento, se aplicó una configuración básica en los routers.

```bash
enable
configure terminal

hostname R-NOMBRE

no ip domain-lookup

banner motd #Acceso restringido - Proyecto 2 Redes 202201139#

enable secret class

line console 0
password cisco
login
exit

line vty 0 4
password cisco
login
exit

service password-encryption
```

## Explicación

- `hostname`: permite asignar un nombre al router.
- `no ip domain-lookup`: evita búsquedas DNS cuando se escribe mal un comando.
- `banner motd`: muestra un mensaje de advertencia al ingresar.
- `enable secret`: protege el acceso al modo privilegiado.
- `line console 0`: configura la contraseña de consola.
- `line vty 0 4`: configura el acceso remoto.
- `service password-encryption`: cifra las contraseñas visibles.

---

# 9. Configuración de interfaces

Cada interfaz utilizada en los routers debe tener una dirección IP y estar habilitada.

```bash
configure terminal

interface GigabitEthernet0/0
description Conexion hacia LAN
ip address 192.168.10.1 255.255.255.0
no shutdown
exit

interface Serial0/0/0
description Enlace hacia otro router
ip address 10.0.0.1 255.255.255.252
clock rate 64000
no shutdown
exit
```

## Explicación

- Las interfaces LAN conectan el router con switches o PCs.
- Las interfaces seriales o gigabit pueden utilizarse como enlaces entre routers.
- El comando `no shutdown` activa la interfaz.
- En enlaces seriales, si el router tiene el lado DCE, se debe colocar `clock rate`.

---

# 10. Configuración de OSPF

OSPF se utilizó para permitir el enrutamiento dinámico en una parte de la red.

```bash
configure terminal

router ospf 1
router-id 1.1.1.1
network 192.168.20.0 0.0.0.255 area 0
network 10.0.0.0 0.0.0.3 area 0
exit
```

## Explicación

- `router ospf 1`: activa el proceso OSPF.
- `router-id`: identifica al router dentro del dominio OSPF.
- `network`: indica las redes que participarán en OSPF.
- `area 0`: corresponde al área principal de OSPF.

---

# 11. Configuración de EIGRP

EIGRP se utilizó para otra sección de la red.

```bash
configure terminal

router eigrp 100
network 192.168.30.0 0.0.0.255
network 10.0.0.4 0.0.0.3
no auto-summary
exit
```

## Explicación

- `router eigrp 100`: activa EIGRP con el sistema autónomo 100.
- `network`: agrega las redes que serán anunciadas.
- `no auto-summary`: evita el resumen automático de redes.

---

# 12. Configuración de RIP

RIP fue utilizado en una sección específica de la red.

```bash
configure terminal

router rip
version 2
network 192.168.40.0
network 10.0.0.8
no auto-summary
exit
```

## Explicación

- `router rip`: activa RIP.
- `version 2`: permite utilizar RIP versión 2.
- `network`: anuncia las redes conectadas.
- `no auto-summary`: evita el resumen automático.

---

# 13. Configuración de rutas estáticas

Las rutas estáticas se utilizaron para indicar manualmente cómo llegar a ciertas redes.

```bash
configure terminal

ip route 192.168.50.0 255.255.255.0 10.0.0.2
```

La estructura general del comando es:

```bash
ip route RED_DESTINO MASCARA SIGUIENTE_SALTO
```

Ejemplo:

```bash
ip route 192.168.50.0 255.255.255.0 10.0.0.2
```

Esto indica que para llegar a la red `192.168.50.0/24`, el router debe enviar los paquetes hacia `10.0.0.2`.

---

# 14. Redistribución de rutas

La redistribución fue necesaria porque el proyecto utilizó varios protocolos de enrutamiento. Sin redistribución, cada protocolo únicamente conocería sus propias redes.

Al aplicar redistribución, las rutas aprendidas por OSPF pueden ser compartidas con EIGRP o RIP, y las rutas de EIGRP o RIP pueden llegar también a OSPF.

---

# 15. Redistribución entre OSPF y EIGRP

## Redistribuir EIGRP dentro de OSPF

```bash
router ospf 1
redistribute eigrp 100 subnets
exit
```

## Redistribuir OSPF dentro de EIGRP

```bash
router eigrp 100
redistribute ospf 1 metric 10000 100 255 1 1500
exit
```

## Explicación

En OSPF se utiliza `subnets` para que se redistribuyan correctamente las subredes.

En EIGRP es necesario colocar una métrica porque EIGRP necesita valores de ancho de banda, retardo, confiabilidad, carga y MTU.

---

# 16. Redistribución entre OSPF y RIP

## Redistribuir RIP dentro de OSPF

```bash
router ospf 1
redistribute rip subnets
exit
```

## Redistribuir OSPF dentro de RIP

```bash
router rip
redistribute ospf 1 metric 2
exit
```

## Explicación

RIP utiliza saltos como métrica. Por eso, al redistribuir rutas hacia RIP, se coloca una métrica como `2`.

---

# 17. Redistribución entre EIGRP y RIP

## Redistribuir RIP dentro de EIGRP

```bash
router eigrp 100
redistribute rip metric 10000 100 255 1 1500
exit
```

## Redistribuir EIGRP dentro de RIP

```bash
router rip
redistribute eigrp 100 metric 2
exit
```

---

# 18. Redistribución de rutas estáticas

También se redistribuyeron rutas estáticas para que los protocolos dinámicos pudieran aprenderlas.

## Redistribuir estáticas en OSPF

```bash
router ospf 1
redistribute static subnets
exit
```

## Redistribuir estáticas en EIGRP

```bash
router eigrp 100
redistribute static metric 10000 100 255 1 1500
exit
```

## Redistribuir estáticas en RIP

```bash
router rip
redistribute static metric 2
exit
```

---

# 19. Configuración básica de switches

Los switches se utilizaron para conectar los dispositivos finales dentro de cada red LAN.

```bash
enable
configure terminal

hostname SW-NOMBRE

no ip domain-lookup

banner motd #Switch de acceso - Proyecto 2 Redes 202201139#

enable secret class

line console 0
password cisco
login
exit

line vty 0 4
password cisco
login
exit

service password-encryption
```

---

# 20. Configuración de puertos de acceso

Los puertos conectados a PCs deben configurarse como puertos de acceso.

```bash
configure terminal

interface FastEthernet0/1
description Conexion hacia PC
switchport mode access
no shutdown
exit
```

Si se utilizan VLANs dentro de alguna LAN, se puede asignar el puerto a una VLAN específica:

```bash
interface FastEthernet0/1
switchport mode access
switchport access vlan 10
no shutdown
exit
```

---

# 21. Configuración IP en PCs

Cada PC debe configurarse con:

- Dirección IP.
- Máscara de subred.
- Gateway predeterminado.

| Dispositivo | IP | Máscara | Gateway |
|------------|----|---------|---------|
| PC Central | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 |
| PC OSPF | 192.168.20.2 | 255.255.255.0 | 192.168.20.1 |
| PC EIGRP | 192.168.30.2 | 255.255.255.0 | 192.168.30.1 |
| PC RIP | 192.168.40.2 | 255.255.255.0 | 192.168.40.1 |
| PC Red Estática | 192.168.50.2 | 255.255.255.0 | 192.168.50.1 |

El gateway siempre debe ser la IP del router que conecta la LAN correspondiente.

---

# 22. Comandos de verificación

Para comprobar el funcionamiento de la red se utilizaron diferentes comandos.

## 22.1 Ver interfaces

```bash
show ip interface brief
```

Este comando permite revisar si las interfaces están activas. Lo ideal es que aparezcan como:

```text
Status: up
Protocol: up
```

---

## 22.2 Ver tabla de enrutamiento

```bash
show ip route
```

En la tabla de enrutamiento se pueden observar rutas conectadas, estáticas y aprendidas por protocolos dinámicos.

Códigos comunes:

```text
C  - Connected
L  - Local
S  - Static
R  - RIP
D  - EIGRP
EX - EIGRP external
O  - OSPF
```

---

## 22.3 Ver protocolos activos

```bash
show ip protocols
```

Este comando permite revisar qué protocolos están configurados, qué redes se anuncian y si existe redistribución.

---

## 22.4 Ver vecinos OSPF

```bash
show ip ospf neighbor
```

Permite verificar si OSPF formó adyacencias correctamente.

---

## 22.5 Ver vecinos EIGRP

```bash
show ip eigrp neighbors
```

Permite verificar si EIGRP formó relación de vecinos correctamente.

---

## 22.6 Ver rutas específicas

```bash
show ip route ospf
show ip route eigrp
show ip route rip
```

Estos comandos permiten revisar únicamente las rutas aprendidas por cada protocolo.

---

# 23. Capturas de pantalla

A continuación se deben colocar las capturas correspondientes a la configuración y verificación del proyecto.

## 23.1 Topología general

<p align="center">
    <img src="https://i.ibb.co/zhknMZXz/imagen-2026-04-29-171526004.png">
</p>

## 23.2 Configuración de interfaces

<p align="center">
    <img src="https://i.ibb.co/ynpvzWPD/imagen-2026-04-29-173642893.png">
</p>

<p align="center">
    <img src="https://i.ibb.co/1fww1fZM/imagen-2026-04-29-173746695.png">
</p>

## 23.3 Tabla de enrutamiento

<p align="center">
    <img src="https://i.ibb.co/nMBNYvkK/imagen-2026-04-29-173854488.png">
</p>

## 23.4 Protocolos activos

<p align="center">
    <img src="https://i.ibb.co/sdzLkHBp/imagen-2026-04-29-173952049.png">
</p>

## 23.5 Vecinos OSPF

<p align="center">
    <img src="https://i.ibb.co/27hx9Nfg/imagen-2026-04-29-174430313.png">
</p>

<p align="center">
    <img src="https://i.ibb.co/WdCH8TM/imagen-2026-04-29-174518139.png">
</p>

## 23.6 Vecinos EIGRP

<p align="center">
    <img src="https://i.ibb.co/zV1wNt3W/imagen-2026-04-29-174740199.png">
</p>

---

# 24. Pruebas de conectividad

Para validar el funcionamiento de la red, se realizaron pruebas de ping entre dispositivos ubicados en diferentes redes.

## 24.1 Ping desde LAN Central hacia LAN OSPF

```bash
ping 192.168.20.2
```

<p align="center">
    <img src="https://i.ibb.co/YBn6gKHy/imagen-2026-04-29-175242391.png">
</p>

## 24.2 Ping desde LAN Central hacia LAN EIGRP

```bash
ping 192.168.30.2
```

<p align="center">
    <img src="https://i.ibb.co/hFJrXHYQ/imagen-2026-04-29-175406385.png">
</p>

## 24.3 Ping desde LAN Central hacia LAN RIP

```bash
ping 192.168.40.2
```

<p align="center">
    <img src="https://i.ibb.co/ZRtwbbDr/imagen-2026-04-29-175925674.png">
</p>


# 25. Resultado de pruebas

Durante las pruebas se comprobó que los dispositivos finales lograron comunicarse entre sí a través de las diferentes sedes.

En algunos casos, los primeros paquetes del ping pueden fallar. Esto puede ocurrir porque los dispositivos están resolviendo ARP o porque los protocolos están terminando de converger. Si después los paquetes responden correctamente, la conectividad se considera funcional.

Ejemplo de respuesta correcta:

```text
Reply from 192.168.40.2: bytes=32 time=2ms TTL=124
Reply from 192.168.40.2: bytes=32 time=1ms TTL=124
```

---

# 26. Problemas encontrados y soluciones

## 26.1 Interfaces apagadas

Uno de los problemas más comunes fue que algunas interfaces no estaban activas.

### Solución

```bash
interface GigabitEthernet0/0
no shutdown
exit
```

---

## 26.2 Falta de rutas hacia redes remotas

Cuando un ping fallaba, se revisaba si el router tenía una ruta hacia la red destino.

### Comando utilizado

```bash
show ip route
```

### Solución

Dependiendo del caso, se podía:

- Agregar la red al protocolo de enrutamiento.
- Crear una ruta estática.
- Configurar redistribución entre protocolos.

---

## 26.3 Redistribución incompleta

Al usar varios protocolos, algunas redes no eran conocidas por todos los routers.

### Solución

Configurar redistribución en los routers que conectaban diferentes dominios de enrutamiento.

```bash
router ospf 1
redistribute eigrp 100 subnets
redistribute rip subnets
redistribute static subnets
exit
```

---

## 26.4 Primeros pings fallidos

En algunas pruebas, los primeros pings mostraron `Request timed out`, pero luego empezaron a responder.

### Explicación

Esto puede ocurrir por resolución ARP o por convergencia inicial de la red. Se considera normal si después los paquetes responden correctamente.

---

# 27. Comandos finales de guardado

Al finalizar la configuración de cada router o switch, se debe guardar la configuración.

```bash
copy running-config startup-config
```

También se puede utilizar:

```bash
write memory
```

---

# 28. Presupuesto de red

A continuación se presenta un presupuesto aproximado para la implementación física de la red.

| # | Categoría | Descripción | Cant. | P. Unit. (Q) | Total (Q) |
|---|-----------|-------------|:----:|-------------:|----------:|
| 1 | Routers | Router Cisco para interconexión de sedes | 5 | Q4,500.00 | Q22,500.00 |
| 2 | Switches | Switch Cisco 2960 para redes LAN | 5 | Q2,945.00 | Q14,725.00 |
| 3 | Dispositivos finales | PC de escritorio | 5 | Q4,030.00 | Q20,150.00 |
| 4 | Cableado | Cable UTP Cat6 caja 305 m | 2 | Q736.25 | Q1,472.50 |
| 5 | Conectores | Conectores RJ-45 Cat6 x100 | 1 | Q139.50 | Q139.50 |
| 6 | Infraestructura | Rack de pared 12U | 1 | Q1,395.00 | Q1,395.00 |
| 7 | Energía | UPS 1500VA | 1 | Q2,480.00 | Q2,480.00 |
| 8 | Organización | PDU y organizadores | 2 | Q310.00 | Q620.00 |
| 9 | Software | Licencias o soporte de IOS | 5 | Q1,162.50 | Q5,812.50 |
|   |   |   |   | **TOTAL** | **Q69,294.50** |

---

# 29. Conclusiones

1. Se logró implementar una red multi-sede funcional utilizando diferentes protocolos de enrutamiento.

2. La configuración de OSPF, EIGRP y RIP permitió practicar el funcionamiento de protocolos dinámicos en una misma topología.

3. La redistribución de rutas fue fundamental para lograr comunicación entre redes administradas por diferentes protocolos.

4. Las rutas estáticas permitieron definir caminos manuales hacia redes específicas.

5. Los comandos de verificación ayudaron a identificar errores en interfaces, rutas y protocolos.

6. Las pruebas de ping demostraron que la conectividad entre sedes fue completada correctamente.

---

# 30. Recomendaciones

1. Revisar siempre el estado de las interfaces con `show ip interface brief`.

2. Verificar la tabla de enrutamiento con `show ip route` antes de modificar configuraciones.

3. Confirmar que cada protocolo esté anunciando las redes correctas.

4. Utilizar `no auto-summary` en EIGRP y RIP para evitar problemas con redes divididas.

5. Aplicar redistribución únicamente en los routers que conectan diferentes dominios de enrutamiento.

6. Guardar la configuración en todos los dispositivos al finalizar.

7. Realizar pruebas de ping desde diferentes puntos de la red para comprobar conectividad total.

---

# 31. Anexos

## 31.1 Comandos generales

```bash
show running-config
show startup-config
show ip interface brief
show ip route
show ip protocols
ping
traceroute
copy running-config startup-config
```

## 31.2 Comandos OSPF

```bash
show ip ospf neighbor
show ip ospf database
show ip route ospf
show ip protocols
```

## 31.3 Comandos EIGRP

```bash
show ip eigrp neighbors
show ip eigrp topology
show ip route eigrp
show ip protocols
```

## 31.4 Comandos RIP

```bash
show ip route rip
show ip protocols
debug ip rip
undebug all
```

---

# 32. Resumen final

El Proyecto 2 permitió implementar una red compuesta por varias sedes conectadas mediante routers. Para lograr comunicación completa se utilizaron protocolos de enrutamiento dinámico, rutas estáticas y redistribución.

La red fue validada mediante tablas de enrutamiento, revisión de protocolos activos y pruebas de ping entre dispositivos finales. Con esto se comprobó que la configuración realizada cumplió con el objetivo principal del proyecto: permitir conectividad entre todas las redes, aunque utilizaran diferentes protocolos de enrutamiento.
