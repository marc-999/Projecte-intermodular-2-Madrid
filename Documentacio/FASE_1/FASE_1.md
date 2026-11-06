<div align="center">
PROJECTE INTERMODULAR
Fase 1 · Despliegue de infraestructura de red y virtualización
Enric Soler i Godes · 2º ASIX
Grupo Madrid
</div>
---
Índice
Resumen ejecutivo
Práctica 2. Instalación de Proxmox en el servidor y estudio de IPs
2.1 Instalación del hipervisor Proxmox VE
2.2 Despliegue del cliente Linux
2.3 Acceso y configuración del switch Cisco
2.4 Creación y nombrado de las VLAN
2.5 Asignación de interfaces a las VLAN
2.6 Verificación de las VLAN
Práctica 3. Despliegue de equipos
3.1 Inventario de dispositivos
3.2 Segmentación en VLAN
3.3 Asignación de puertos del switch Cisco
3.4 Verificación de conectividad
3.5 Acceso a la interfaz web de Proxmox VE
3.6 Carga de la imagen ISO
3.7 Despliegue de la máquina virtual Ubuntu Server
3.8 Verificación del almacenamiento en Ubuntu Server
3.9 Despliegue de la máquina virtual cliente Linux Mint
---
Resumen ejecutivo
En esta primera fase se ha desplegado la infraestructura base del proyecto: un servidor físico con el hipervisor Proxmox VE, un cliente Linux Mint y un switch Cisco gestionado por Telnet. La red se ha segmentado en cuatro VLAN (servidores, comercial, producción y gestión), cada una con su propio direccionamiento /24, y se ha verificado la conectividad entre cliente y servidor mediante `ping`.
Elemento	Detalle
Hipervisor	Proxmox VE (instalación bare metal)
Cliente	Linux Mint (físico)
Conmutación	Switch Cisco, puertos 11 a 20
Segmentación	4 VLAN: 210, 220, 230 y 299
Direccionamiento	Redes 10.2.X.0/24
---
Práctica 2. Instalación de Proxmox en el servidor y estudio de IPs
2.1 Instalación del hipervisor Proxmox VE
Se descarga la imagen ISO oficial de Proxmox VE, que será el hipervisor instalado directamente sobre el hardware (bare metal) del servidor físico.
<p align="center">
  <img src="Imagenes/pagina02\_imagen1.png" alt="Descarga de la ISO de Proxmox" width="500"><br>
  <sub><em>Figura 1. Descarga de la ISO de Proxmox</em></sub>
</p>
Para generar el medio de instalación se utiliza balenaEtcher, herramienta que escribe la imagen ISO en un dispositivo USB y lo deja configurado como unidad de arranque.
<p align="center">
  <img src="Imagenes/pagina02\_imagen2.png" alt="Descarga de balenaEtcher" width="500"><br>
  <sub><em>Figura 2. Descarga de balenaEtcher</em></sub>
</p>
Se selecciona la ISO de origen y la unidad USB de destino, y se lanza el proceso de escritura (flasheo) del medio.
<p align="center">
  <img src="Imagenes/pagina03\_imagen1.png" alt="Preparación para flashear la ISO" width="500"><br>
  <sub><em>Figura 3. Preparación para flashear la ISO</em></sub>
</p>
A continuación se arranca el servidor físico desde el USB y se ejecuta el asistente de instalación de Proxmox VE.
<p align="center">
  <img src="Imagenes/pagina03\_imagen2.png" alt="Servidor encendido" width="500"><br>
  <sub><em>Figura 4. Servidor encendido</em></sub>
</p>
<p align="center">
  <img src="Imagenes/pagina03\_imagen3.png" alt="Instalación de Proxmox" width="500"><br>
  <sub><em>Figura 5. Instalación de Proxmox</em></sub>
</p>
Durante la instalación se configura la red de gestión del servidor (dirección IP, máscara de subred, puerta de enlace y DNS). Una vez finalizada, se comprueba que los parámetros se han aplicado correctamente.
<p align="center">
  <img src="Imagenes/pagina04\_imagen1.png" alt="Configuración de las IPs del servidor" width="500"><br>
  <sub><em>Figura 6. Configuración de las IPs del servidor</em></sub>
</p>
2.2 Despliegue del cliente Linux
Se despliega el cliente Linux Mint en la estación de trabajo.
> ⚠️ \*\*Nota:\*\* la captura pertenece a pruebas previas con Ubuntu Client, descartado por incompatibilidades técnicas. No se documentó gráficamente la instalación final de Linux Mint.
<p align="center">
  <img src="Imagenes/pagina05\_imagen1.png" alt="Instalación de Ubuntu (pruebas previas)" width="500"><br>
  <sub><em>Figura 7. Instalación de Ubuntu (pruebas previas)</em></sub>
</p>
2.3 Acceso y configuración del switch Cisco
Se instala y configura PuTTY como cliente de terminal para acceder al switch Cisco y habilitar el acceso remoto por Telnet.
<p align="center">
  <img src="Imagenes/pagina05\_imagen2.png" alt="Instalación de PuTTY" width="500"><br>
  <sub><em>Figura 8. Instalación de PuTTY</em></sub>
</p>
<p align="center">
  <img src="Imagenes/pagina05\_imagen3.png" alt="Configuración de PuTTY" width="500"><br>
  <sub><em>Figura 9. Configuración de PuTTY</em></sub>
</p>
Se realiza la configuración inicial del switch (acceso de gestión y parámetros básicos).
<p align="center">
  <img src="Imagenes/pagina06\_imagen1.png" alt="Switch (detalle)" width="500"><br>
  <sub><em>Figura 10. Switch (detalle)</em></sub>
</p>
<p align="center">
  <img src="Imagenes/pagina06\_imagen2.png" alt="Configuración del switch" width="500"><br>
  <sub><em>Figura 11. Configuración del switch</em></sub>
</p>
Se verifica que la configuración se ha guardado correctamente y que es posible conectarse al switch por Telnet directamente, sin necesidad de PuTTY.
<p align="center">
  <img src="Imagenes/pagina06\_imagen3.png" alt="Comprobación de la conexión por Telnet" width="500"><br>
  <sub><em>Figura 12. Comprobación de la conexión por Telnet</em></sub>
</p>
2.4 Creación y nombrado de las VLAN
Se crean las VLAN en el switch y se les asigna el nombre correspondiente según su función.
```
Switch(config)# vlan <id>
Switch(config-vlan)# name <nombre>
```
<p align="center">
  <img src="Imagenes/pagina07\_imagen1.png" alt="Nombres de las VLAN" width="500"><br>
  <sub><em>Figura 13. Nombres de las VLAN</em></sub>
</p>
2.5 Asignación de interfaces a las VLAN
Se accede a la interfaz `GigabitEthernet 0/12` del switch Cisco. Una vez dentro, se configura la interfaz en modo acceso (`switchport mode access`) y se le asigna la VLAN 210 (`switchport access vlan 210`), de modo que el puerto pase a transportar únicamente tráfico sin etiquetar de dicha VLAN.
```
Switch(config)# interface GigabitEthernet 0/12
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 210
```
<p align="center">
  <img src="Imagenes/pagina07\_imagen2.png" alt="Configuración de la interfaz Gi0/12" width="500"><br>
  <sub><em>Figura 14. Configuración de la interfaz Gi0/12</em></sub>
</p>
El mismo procedimiento se repite para el resto de interfaces y VLAN.
<p align="center">
  <img src="Imagenes/pagina08\_imagen1.png" alt="Configuración del resto de VLAN" width="500"><br>
  <sub><em>Figura 15. Configuración del resto de VLAN</em></sub>
</p>
2.6 Verificación de las VLAN
Se ejecuta el comando `show vlan brief` para validar la creación de las VLAN y la asignación de puertos. En la comprobación se detectan algunos errores de configuración (nombres o puertos asignados incorrectamente).
<p align="center">
  <img src="Imagenes/pagina08\_imagen2.png" alt="Resultado de show vlan brief" width="500"><br>
  <sub><em>Figura 16. Resultado de show vlan brief</em></sub>
</p>
---
Práctica 3. Despliegue de equipos
Se corrigen los errores detectados y se vuelve a ejecutar `show vlan brief` para confirmar que el estado de las VLAN y la asignación de puertos son los esperados.
<p align="center">
  <img src="Imagenes/llista\_solucionada.png" alt="show vlan brief tras corregir" width="500"><br>
  <sub><em>Figura 17. show vlan brief tras corregir</em></sub>
</p>
3.1 Inventario de dispositivos
Estos son los dispositivos de los que disponemos y sus características:
Dispositivo	Tipo	IP	VLAN	Puerto	Estado
Proxmox	Servidor físico	10.2.10.1/24	210	11	Conectado
Linux Mint	Cliente físico	10.2.10.2/24	210	12	Conectado
Ubuntu Server	Servidor físico	10.2.10.3/24	210	Sin asignar	No conectado aún
Switch Cisco	Gestión	10.2.99.1/24	299	Puerto de gestión	Activo
3.2 Segmentación en VLAN
Estas son las VLAN que hemos asignado. Cada una dispone de su propio direccionamiento IP /24 y de una pareja de interfaces del switch:
VLAN	Nombre	Red	Interfaces del switch
210	servidor_mad	10.2.10.0/24	11, 12
220	comercial_mad	10.2.20.0/24	13, 17
230	produccion_mad	10.2.30.0/24	14, 18
299	gestion_mad	10.2.99.0/24	16, 19
3.3 Asignación de puertos del switch Cisco
Esta es la distribución final de los puertos 11 a 20 del switch Cisco, con la VLAN a la que pertenece cada uno y el dispositivo conectado en la actualidad:
Puerto	VLAN	Nombre VLAN	Dispositivo conectado
11	210	servidor_mad	Servidor Proxmox
12	210	servidor_mad	Cliente Linux Mint
13	220	comercial_mad	Libre
14	230	produccion_mad	Libre
15	Sin asignar	-	Libre
16	299	gestion_mad	Libre
17	220	comercial_mad	Libre
18	230	produccion_mad	Libre
19	299	gestion_mad	Libre
20	Sin asignar	-	Libre
3.4 Verificación de conectividad
Verificamos que la configuración de red está correctamente configurada y realizamos un `ping` al servidor para comprobar la conectividad entre cliente y servidor dentro de la VLAN 210.
<p align="center">
  <img src="Imagenes/config\_xarxa.png" alt="Configuración de la red" width="500"><br>
  <sub><em>Figura 18. Configuración de la red</em></sub>
</p>
<p align="center">
  <img src="Imagenes/ping.png" alt="Ping entre cliente y servidor" width="500"><br>
  <sub><em>Figura 19. Ping entre cliente y servidor</em></sub>
</p>
3.5 Acceso a la interfaz web de Proxmox VE
Una vez finalizada la configuración de red del servidor, se accede a la consola de administración de Proxmox VE mediante un navegador web, a través del puerto HTTPS 8006 de la IP de gestión del host (`https://10.2.10.1:8006`). La autenticación se realiza con el usuario `root` definido durante la instalación. Desde esta interfaz se gestionan los nodos, el almacenamiento, la red y las máquinas virtuales.
<!-- Sustituir la ruta de cada imagen (src) por el archivo real. Mantener el resto de la etiqueta. -->
<p align="center">
  <img src="Imagenes/paso\_01\_acceso\_web\_proxmox.png" alt="Acceso a la interfaz web de Proxmox VE" width="500"><br>
  <sub><em>Figura 20. Acceso a la interfaz web de Proxmox VE</em></sub>
</p>
3.6 Carga de la imagen ISO
Para poder crear la máquina virtual es necesario disponer del medio de instalación en el almacenamiento del nodo. Se sube la imagen ISO del sistema operativo al repositorio local de Proxmox (almacenamiento `local`, sección ISO Images), de forma que quede disponible como unidad de CD/DVD virtual en el asistente de creación de máquinas.
<p align="center">
  <img src="Imagenes/paso\_02\_carga\_iso.png" alt="Carga de la imagen ISO en el almacenamiento de Proxmox" width="500"><br>
  <sub><em>Figura 21. Carga de la imagen ISO en el almacenamiento de Proxmox</em></sub>
</p>
3.7 Despliegue de la máquina virtual Ubuntu Server
Se crea la máquina virtual de Ubuntu Server mediante el asistente de Proxmox VE y se revisan sus especificaciones de hardware (CPU, memoria, controlador y tamaño del disco virtual e interfaz de red), comprobando que los recursos asignados son los previstos para el servicio.
<p align="center">
  <img src="Imagenes/paso\_03\_specs\_ubuntu\_server.png" alt="Especificaciones de hardware de la máquina Ubuntu Server" width="500"><br>
  <sub><em>Figura 22. Especificaciones de hardware de la máquina Ubuntu Server</em></sub>
</p>
Durante la instalación del sistema se define el esquema de almacenamiento. Se crean manualmente las particiones sobre el disco virtual, indicando para cada una su tamaño, sistema de ficheros y punto de montaje.
<p align="center">
  <img src="Imagenes/paso\_04\_particiones\_ubuntu\_server.png" alt="Creación de las particiones en Ubuntu Server" width="500"><br>
  <sub><em>Figura 23. Creación de las particiones en Ubuntu Server</em></sub>
</p>
A continuación se configura la identidad del sistema: el nombre de la máquina (hostname), el usuario administrador y su contraseña.
<p align="center">
  <img src="Imagenes/paso\_05\_hostname\_usuario\_ubuntu\_server.png" alt="Configuración del nombre de la máquina y de la contraseña" width="500"><br>
  <sub><em>Figura 24. Configuración del nombre de la máquina y de la contraseña</em></sub>
</p>
3.8 Verificación del almacenamiento en Ubuntu Server
Con el sistema ya instalado, se realizan comprobaciones desde la línea de comandos. En primer lugar se lista el contenido del directorio `/sys`, el sistema de ficheros virtual (sysfs) con el que el kernel expone información de los dispositivos y del hardware. Después se ejecuta un segundo comando que muestra las particiones del disco y confirma que coinciden con el esquema definido en la instalación.
```
$ ls /sys
```
<p align="center">
  <img src="Imagenes/paso\_06\_comandos\_sys\_particiones.png" alt="Listado del directorio /sys y visualización de las particiones" width="500"><br>
  <sub><em>Figura 25. Listado del directorio /sys y visualización de las particiones</em></sub>
</p>
Por último, se consulta el contenido del archivo `/etc/fstab`, donde se definen los sistemas de ficheros que se montan en el arranque. Cada línea identifica el dispositivo (normalmente por su UUID), el punto de montaje, el tipo de sistema de ficheros, las opciones de montaje y los campos de volcado y comprobación (dump y pass).
```
$ cat /etc/fstab
```
<p align="center">
  <img src="Imagenes/paso\_07\_fstab\_ubuntu\_server.png" alt="Contenido del archivo /etc/fstab" width="500"><br>
  <sub><em>Figura 26. Contenido del archivo /etc/fstab</em></sub>
</p>
3.9 Despliegue de la máquina virtual cliente Linux Mint
Se configura la máquina virtual del cliente Linux Mint en Proxmox VE, revisando su configuración de hardware y los discos virtuales asociados.
<p align="center">
  <img src="Imagenes/paso\_08\_config\_vm\_linux\_mint.png" alt="Configuración de la máquina virtual Linux Mint y sus discos" width="500"><br>
  <sub><em>Figura 27. Configuración de la máquina virtual Linux Mint y sus discos</em></sub>
</p>
Durante la instalación se realiza el particionado del disco del cliente, definiendo las particiones y los puntos de montaje del sistema.
<p align="center">
  <img src="Imagenes/paso\_09\_particionado\_linux\_mint.png" alt="Particionado del disco del cliente Linux Mint" width="500"><br>
  <sub><em>Figura 28. Particionado del disco del cliente Linux Mint</em></sub>
</p>
Finalmente, se crea el usuario del equipo y se establece su contraseña, dejando el cliente listo para su uso.
<p align="center">
  <img src="Imagenes/paso\_10\_usuario\_linux\_mint.png" alt="Creación de usuario y contraseña del cliente Linux Mint" width="500"><br>
  <sub><em>Figura 29. Creación de usuario y contraseña del cliente Linux Mint</em></sub>
</p>
---
<div align="center">
Projecte Intermodular · Enric Soler i Godes · 2º ASIX · Grupo Madrid
</div>
