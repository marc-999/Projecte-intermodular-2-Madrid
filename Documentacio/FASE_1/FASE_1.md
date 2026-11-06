# PROJECTE INTERMODULAR

**ENRIC SOLER I GODES — 2 ASIX**

## GRUPO: MADRID

---

## Fase 1.2 Instalación de Proxmox en el servidor y estudio de IPs

### Instalación del hipervisor Proxmox VE

Se descarga la imagen ISO oficial de Proxmox VE, que será el hipervisor instalado directamente sobre el hardware (*bare metal*) del servidor físico.

![Descarga de la ISO de Proxmox](Imagenes/pagina02_imagen1.png)

Para generar el medio de instalación se utiliza **balenaEtcher**, herramienta que escribe la imagen ISO en un dispositivo USB y lo deja configurado como unidad de arranque.

![Descarga de balenaEtcher](Imagenes/pagina02_imagen2.png)

Se selecciona la ISO de origen y la unidad USB de destino, y se lanza el proceso de escritura (*flasheo*) del medio.

![Preparación para flashear la ISO](Imagenes/pagina03_imagen1.png)

A continuación se arranca el servidor físico desde el USB y se ejecuta el asistente de instalación de Proxmox VE.

![Servidor encendido](Imagenes/pagina03_imagen2.png)

![Instalación de Proxmox](Imagenes/pagina03_imagen3.png)

Durante la instalación se configura la red de gestión del servidor (dirección IP, máscara de subred, puerta de enlace y DNS). Una vez finalizada, se comprueba que los parámetros se han aplicado correctamente.

![Configuración de las IPs del servidor](Imagenes/pagina04_imagen1.png)

### Despliegue del cliente Linux

Se despliega el cliente Linux Mint en la estación de trabajo.

> **Nota:** la captura pertenece a pruebas previas con Ubuntu Client, descartado por incompatibilidades técnicas. No se documentó gráficamente la instalación final de Linux Mint.

![Instalación de Ubuntu](Imagenes/pagina05_imagen1.png)

### Acceso y configuración del switch Cisco

Se instala y configura **PuTTY** como cliente de terminal para acceder al switch Cisco y habilitar el acceso remoto por **Telnet**.

![Instalación de Putty](Imagenes/pagina05_imagen2.png)

![Configuración de Putty](Imagenes/pagina05_imagen3.png)

Se realiza la configuración inicial del switch (acceso de gestión y parámetros básicos).

![Switch (detalle)](Imagenes/pagina06_imagen1.png)

![Configuración del switch](Imagenes/pagina06_imagen2.png)

Se verifica que la configuración se ha guardado correctamente y que es posible conectarse al switch por Telnet directamente, sin necesidad de PuTTY.

![Comprobación de la conexión por telnet](Imagenes/pagina06_imagen3.png)

### Creación y nombrado de las VLAN

Se crean las VLAN en el switch y se les asigna el nombre correspondiente según su función.

```
Switch(config)# vlan <id>
Switch(config-vlan)# name <nombre>
```

![Nombres de las VLAN](Imagenes/pagina07_imagen1.png)

### Asignación de interfaces a las VLAN

En la captura se accede a la interfaz `GigabitEthernet 0/12` del switch Cisco. Una vez dentro, se configura la interfaz en **modo acceso** (`switchport mode access`) y se le asigna la **VLAN 210** (`switchport access vlan 210`), de modo que el puerto pase a transportar únicamente tráfico sin etiquetar de dicha VLAN.

```
Switch(config)# interface GigabitEthernet 0/12
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 210
```

![Configuración de la interfaz Gi0/12](Imagenes/pagina07_imagen2.png)

El mismo procedimiento se repite para el resto de interfaces y VLAN.

![Configuración del resto de VLAN](Imagenes/pagina08_imagen1.png)

### Verificación de las VLAN

Se ejecuta el comando `show vlan brief` para validar la creación de las VLAN y la asignación de puertos. En la comprobación se detectan algunos errores de configuración (nombres o puertos asignados incorrectamente).

![Resultado de show vlan brief](Imagenes/pagina08_imagen2.png)

---

## Fase 1.3 Despliegue de equipos

Se corrigen los errores detectados y se vuelve a ejecutar `show vlan brief` para confirmar que el estado de las VLAN y la asignación de puertos son los esperados.

![show vlan brief tras corregir](Imagenes/llista_solucionada.png)

### Inventario de dispositivos

Estos son los dispositivos de los que disponemos y sus características:

| Dispositivo | Tipo | IP | VLAN | Puerto | Estado |
|-------------|------|----|------|--------|--------|
| Proxmox | Servidor físico | 10.2.10.1/24 | 210 | 11 | Conectado |
| Linux Mint | Cliente físico | 10.2.10.2/24 | 210 | 12 | Conectado |
| Ubuntu Server | Servidor físico | 10.2.10.3/24 | 210 | Sin asignar | No conectado aún |
| Switch Cisco | Gestión | 10.2.99.1/24 | 299 | Puerto de gestión | Activo |

### Segmentación en VLAN

Estas son las VLAN que hemos asignado. Cada una dispone de su propio direccionamiento IP /24 y de una pareja de interfaces del switch:

| VLAN | Nombre | Red | Interfaces del switch |
|------|--------|-----|-----------------------|
| 210 | servidor_mad | 10.2.10.0/24 | 11, 12 |
| 220 | comercial_mad | 10.2.20.0/24 | 13, 17 |
| 230 | produccion_mad | 10.2.30.0/24 | 14, 18 |
| 299 | gestion_mad | 10.2.99.0/24 | 16, 19 |

### Asignación de puertos del switch Cisco

Esta es la distribución final de los puertos 11 a 20 del switch Cisco, con la VLAN a la que pertenece cada uno y el dispositivo conectado en la actualidad:

| Puerto | VLAN | Nombre VLAN | Dispositivo conectado |
|--------|------|-------------|-----------------------|
| 11 | 210 | servidor_mad | Servidor Proxmox |
| 12 | 210 | servidor_mad | Cliente Linux Mint |
| 13 | 220 | comercial_mad | Libre |
| 14 | 230 | produccion_mad | Libre |
| 15 | Sin asignar | - | Libre |
| 16 | 299 | gestion_mad | Libre |
| 17 | 220 | comercial_mad | Libre |
| 18 | 230 | produccion_mad | Libre |
| 19 | 299 | gestion_mad | Libre |
| 20 | Sin asignar | - | Libre |

### Verificación de conectividad

Verificamos que la configuración de red está correctamente configurada y realizamos un `ping` al servidor para comprobar la conectividad entre cliente y servidor dentro de la VLAN 210.

![Imatge de la configuració de la xarxa](Imagenes/config_xarxa.png)

![Imatge del ping entre client i servidor](Imagenes/ping.png)

