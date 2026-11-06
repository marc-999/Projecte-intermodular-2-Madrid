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
3.7 Planificación y esquema de particionado (Tarea 1)
3.8 Despliegue de la máquina virtual Ubuntu Server
3.9 Verificación del almacenamiento en Ubuntu Server
3.10 Despliegue de la máquina virtual cliente Linux Mint
3.11 Verificación del almacenamiento en Linux Mint
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
  <img src="Imagenes/pagina02_imagen1.png" alt="Descarga de la ISO de Proxmox" width="500"><br>
  <sub><em>Figura 1. Descarga de la ISO de Proxmox</em></sub>
</p>
Para generar el medio de instalación se utiliza balenaEtcher, herramienta que escribe la imagen ISO en un dispositivo USB y lo deja configurado como unidad de arranque.
<p align="center">
  <img src="Imagenes/pagina02_imagen2.png" alt="Descarga de balenaEtcher" width="500"><br>
  <sub><em>Figura 2. Descarga de balenaEtcher</em></sub>
</p>
Se selecciona la ISO de origen y la unidad USB de destino, y se lanza el proceso de escritura (flasheo) del medio.
<p align="center">
  <img src="Imagenes/pagina03_imagen1.png" alt="Preparación para flashear la ISO" width="500"><br>
  <sub><em>Figura 3. Preparación para flashear la ISO</em></sub>
</p>
A continuación se arranca el servidor físico desde el USB y se ejecuta el asistente de instalación de Proxmox VE.
<p align="center">
  <img src="Imagenes/pagina03_imagen2.png" alt="Servidor encendido" width="500"><br>
  <sub><em>Figura 4. Servidor encendido</em></sub>
</p>
<p align="center">
  <img src="Imagenes/pagina03_imagen3.png" alt="Instalación de Proxmox" width="500"><br>
  <sub><em>Figura 5. Instalación de Proxmox</em></sub>
</p>
Durante la instalación se configura la red de gestión del servidor (dirección IP, máscara de subred, puerta de enlace y DNS). Una vez finalizada, se comprueba que los parámetros se han aplicado correctamente.
<p align="center">
  <img src="Imagenes/pagina04_imagen1.png" alt="Configuración de las IPs del servidor" width="500"><br>
  <sub><em>Figura 6. Configuración de las IPs del servidor</em></sub>
</p>
2.2 Despliegue del cliente Linux
Se despliega el cliente Linux Mint en la estación de trabajo.
> ⚠️ **Nota:** la captura pertenece a pruebas previas con Ubuntu Client, descartado por incompatibilidades técnicas. No se documentó gráficamente la instalación final de Linux Mint.
<p align="center">
  <img src="Imagenes/pagina05_imagen1.png" alt="Instalación de Ubuntu (pruebas previas)" width="500"><br>
  <sub><em>Figura 7. Instalación de Ubuntu (pruebas previas)</em></sub>
</p>
2.3 Acceso y configuración del switch Cisco
Se instala y configura PuTTY como cliente de terminal para acceder al switch Cisco y habilitar el acceso remoto por Telnet.
<p align="center">
  <img src="Imagenes/pagina05_imagen2.png" alt="Instalación de PuTTY" width="500"><br>
  <sub><em>Figura 8. Instalación de PuTTY</em></sub>
</p>
<p align="center">
  <img src="Imagenes/pagina05_imagen3.png" alt="Configuración de PuTTY" width="500"><br>
  <sub><em>Figura 9. Configuración de PuTTY</em></sub>
</p>
Se realiza la configuración inicial del switch (acceso de gestión y parámetros básicos).
<p align="center">
  <img src="Imagenes/pagina06_imagen1.png" alt="Switch (detalle)" width="500"><br>
  <sub><em>Figura 10. Switch (detalle)</em></sub>
</p>
<p align="center">
  <img src="Imagenes/pagina06_imagen2.png" alt="Configuración del switch" width="500"><br>
  <sub><em>Figura 11. Configuración del switch</em></sub>
</p>
Se verifica que la configuración se ha guardado correctamente y que es posible conectarse al switch por Telnet directamente, sin necesidad de PuTTY.
<p align="center">
  <img src="Imagenes/pagina06_imagen3.png" alt="Comprobación de la conexión por Telnet" width="500"><br>
  <sub><em>Figura 12. Comprobación de la conexión por Telnet</em></sub>
</p>
2.4 Creación y nombrado de las VLAN
Se crean las VLAN en el switch y se les asigna el nombre correspondiente según su función.
```
Switch(config)# vlan <id>
Switch(config-vlan)# name <nombre>
```
<p align="center">
  <img src="Imagenes/pagina07_imagen1.png" alt="Nombres de las VLAN" width="500"><br>
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
  <img src="Imagenes/pagina07_imagen2.png" alt="Configuración de la interfaz Gi0/12" width="500"><br>
  <sub><em>Figura 14. Configuración de la interfaz Gi0/12</em></sub>
</p>
El mismo procedimiento se repite para el resto de interfaces y VLAN.
<p align="center">
  <img src="Imagenes/pagina08_imagen1.png" alt="Configuración del resto de VLAN" width="500"><br>
  <sub><em>Figura 15. Configuración del resto de VLAN</em></sub>
</p>
2.6 Verificación de las VLAN
Se ejecuta el comando `show vlan brief` para validar la creación de las VLAN y la asignación de puertos. En la comprobación se detectan algunos errores de configuración (nombres o puertos asignados incorrectamente).
<p align="center">
  <img src="Imagenes/pagina08_imagen2.png" alt="Resultado de show vlan brief" width="500"><br>
  <sub><em>Figura 16. Resultado de show vlan brief</em></sub>
</p>
---
Práctica 3. Despliegue de equipos
Se corrigen los errores detectados y se vuelve a ejecutar `show vlan brief` para confirmar que el estado de las VLAN y la asignación de puertos son los esperados.
<p align="center">
  <img src="Imagenes/llista_solucionada.png" alt="show vlan brief tras corregir" width="500"><br>
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
  <img src="Imagenes/config_xarxa.png" alt="Configuración de la red" width="500"><br>
  <sub><em>Figura 18. Configuración de la red</em></sub>
</p>
<p align="center">
  <img src="Imagenes/ping.png" alt="Ping entre cliente y servidor" width="500"><br>
  <sub><em>Figura 19. Ping entre cliente y servidor</em></sub>
</p>
3.5 Acceso a la interfaz web de Proxmox VE
Una vez finalizada la configuración de red del servidor, se accede a la consola de administración de Proxmox VE mediante un navegador web, a través del puerto HTTPS 8006 de la IP de gestión del host (`https://10.2.10.1:8006`). La pantalla de inicio de sesión solicita usuario y contraseña, y permite seleccionar el realm de autenticación (en este caso Linux PAM standard authentication, que valida contra los usuarios del sistema operativo del host) y el idioma de la interfaz.
<p align="center">
  <img src="Imagenes/paso_01_acceso_web_proxmox.png" alt="Pantalla de inicio de sesión de Proxmox VE" width="500"><br>
  <sub><em>Figura 20. Pantalla de inicio de sesión de Proxmox VE</em></sub>
</p>
3.6 Carga de la imagen ISO
Para poder crear la máquina virtual es necesario disponer del medio de instalación en el almacenamiento del nodo. Se sube la imagen ISO de Ubuntu Server al almacenamiento `local` de Proxmox, de forma que quede disponible como unidad de CD/DVD virtual en el asistente de creación de máquinas. El archivo ocupa 2,73 GiB y se identifica con el tipo MIME `application/vnd.efi.iso`. Proxmox avisa de que las subidas se almacenan temporalmente en `/var/tmp`, por lo que debe haber espacio libre suficiente en esa ruta antes de iniciar la carga.
<p align="center">
  <img src="Imagenes/paso_02_carga_iso.png" alt="Carga de la imagen ISO en el almacenamiento de Proxmox" width="500"><br>
  <sub><em>Figura 21. Carga de la imagen ISO en el almacenamiento de Proxmox</em></sub>
</p>
3.7 Planificación y esquema de particionado (Tarea 1)
Antes de iniciar el instalador se elabora la tabla de diseño técnico del almacenamiento, indicando para cada punto de montaje el disco, el tamaño, el sistema de ficheros y su función. El servidor debe cumplir el siguiente esquema obligatorio:
Disco	Punto de montaje	Sistema de ficheros	Tamaño	Uso
`scsi0`	`/boot/efi`	vfat (FAT32)	538 MB	Partición de sistema EFI
`scsi0`	`/boot`	ext4	483 MB	Núcleo Linux e initramfs
`scsi1`	`/`	ext4	20 GB	Sistema operativo
`scsi2`	`/home`	ext4	30 GB	Directorios de los usuarios
`scsi3`	swap	swap	10 GB	Memoria de intercambio (extra)
El criterio técnico del diseño es el siguiente:
`/boot/efi` en vfat: el firmware UEFI solo sabe leer la partición de sistema EFI (ESP) si está formateada en FAT32, y debe estar al inicio del disco de arranque.
`/boot` separado en ext4: aísla el núcleo y el initramfs del resto del sistema, lo que simplifica el arranque y la recuperación.
`/` y `/home` en discos distintos: los datos de los usuarios sobreviven a una reinstalación o restauración del sistema, y cada volumen puede ampliarse de forma independiente.
> **Observación:** el disco `scsi0` se creó con 1 GiB, por lo que `/boot` queda en 483 MB, por debajo del 1 GB que indica el enunciado. Para ajustarse por completo, este disco debería tener un mínimo de 2 GiB (512 MB de ESP más 1 GB de `/boot`).
El mismo esquema se aplica al equipo cliente, con tres discos virtuales:
Disco	Punto de montaje	Sistema de ficheros	Tamaño	Uso
`scsi0`	`/boot/efi`	vfat (FAT32)	487 MiB	Partición de sistema EFI
`scsi0`	`/boot`	ext4	977 MiB	Núcleo Linux e initramfs
`scsi1`	`/`	ext4	30 GB	Sistema operativo
`scsi2`	`/home`	ext4	30 GB	Directorios de los usuarios
En el cliente, el área de intercambio no se define como partición: la gestiona el instalador mediante el archivo `/swapfile`.
3.8 Despliegue de la máquina virtual Ubuntu Server
Se crea la máquina virtual ubuntuSRV en el nodo `madrid` mediante el asistente de Proxmox VE. La pantalla de confirmación resume la configuración que se va a aplicar:
Parámetro	Valor
Firmware (`bios`)	`ovmf` (UEFI) con disco EFI en `local-lvm`
Tipo de máquina	`q35`
CPU	2 cores, tipo `x86-64-v2-AES`
Memoria	4096 MiB
Red	Interfaz VirtIO (`net0`) en el puente `vmbr0`, con firewall activo
Almacenamiento	Discos SCSI sobre `local-lvm`, con IO thread activado
Medio de instalación	`ubuntu-26.04.1-live-server-amd64.iso` (unidad `ide2`, tipo CD/DVD)
Tipo de SO	`l26` (Linux 2.6 o superior)
<p align="center">
  <img src="Imagenes/paso_03_specs_ubuntu_server.png" alt="Especificaciones de la máquina virtual Ubuntu Server" width="500"><br>
  <sub><em>Figura 22. Especificaciones de la máquina virtual Ubuntu Server</em></sub>
</p>
Siguiendo el esquema planificado en el apartado 3.7, el instalador se configura de forma manual (custom storage layout), asignando cada punto de montaje a su disco. Separar `/` y `/home` en discos distintos facilita ampliar o restaurar cada volumen sin afectar al resto del sistema.
<p align="center">
  <img src="Imagenes/paso_04_particiones_ubuntu_server.png" alt="Esquema de particiones del servidor Ubuntu Server" width="500"><br>
  <sub><em>Figura 23. Esquema de particiones del servidor Ubuntu Server</em></sub>
</p>
A continuación se configura la identidad del sistema en el asistente de instalación (Profile configuration): el nombre descriptivo del usuario (`SRVUbuntu`), el nombre del servidor o hostname (`srv-ubuntu`), el nombre de usuario (`ubuntu`) y su contraseña, necesaria para la autenticación y para ejecutar comandos con `sudo`.
<p align="center">
  <img src="Imagenes/paso_05_hostname_usuario_ubuntu_server.png" alt="Configuración del nombre de la máquina, usuario y contraseña" width="500"><br>
  <sub><em>Figura 24. Configuración del nombre de la máquina, usuario y contraseña</em></sub>
</p>
3.9 Verificación del almacenamiento en Ubuntu Server
Con el sistema instalado, se comprueba el resultado desde la línea de comandos. Primero se navega al directorio `/sys` y se lista su contenido. Se trata de sysfs, un sistema de ficheros virtual con el que el kernel expone información de los dispositivos y del hardware. Después se ejecuta `df -h`, que muestra los sistemas de ficheros montados con su tamaño, espacio usado y disponible, y su punto de montaje.
```
$ ls
$ cd /sys
$ ls
$ df -h
```
La salida confirma que el esquema definido en el instalador se ha aplicado: `/dev/sdb1` (20 GB) montado en `/`, `/dev/sdc1` (30 GB) en `/home`, `/dev/sda2` en `/boot` y `/dev/sda1` en `/boot/efi`. La partición de intercambio no aparece porque `df` solo lista sistemas de ficheros montados.
<p align="center">
  <img src="Imagenes/paso_06_comandos_ubuntu_server.png" alt="Listado del directorio /sys y salida de df -h" width="500"><br>
  <sub><em>Figura 25. Listado del directorio /sys y salida de df -h</em></sub>
</p>
Por último, se consulta el archivo `/etc/fstab`, que define los sistemas de ficheros que se montan en el arranque. Cada entrada indica el dispositivo (identificado por su UUID, más robusto que el nombre del dispositivo), el punto de montaje, el tipo de sistema de ficheros, las opciones de montaje y los campos de volcado y comprobación (dump y pass). Los comentarios generados por `curtin`, la herramienta de instalación de Ubuntu, indican el dispositivo original de cada entrada. El archivo incluye `/` y `/boot` en ext4, `/boot/efi` en vfat, `/home` en ext4 y la partición de intercambio (`swap`).
```
$ sudo nano /etc/fstab
```
<p align="center">
  <img src="Imagenes/paso_07_fstab_ubuntu_server.png" alt="Contenido del archivo /etc/fstab en Ubuntu Server" width="500"><br>
  <sub><em>Figura 26. Contenido del archivo /etc/fstab en Ubuntu Server</em></sub>
</p>
3.10 Despliegue de la máquina virtual cliente Linux Mint
El cliente se crea también como máquina virtual en Proxmox VE, a partir de la imagen `linuxmint-22.3-cinnamon-64bit.iso`, cargada en el almacenamiento `local`. En la pestaña SO se selecciona la imagen ISO como unidad de CD/DVD y se define el sistema operativo invitado como Linux con versión 6.x - 2.6 Kernel.
<p align="center">
  <img src="Imagenes/paso_08a_vm_mint_so.png" alt="Asistente de creación de la VM: pestaña SO" width="500"><br>
  <sub><em>Figura 27. Asistente de creación de la VM: pestaña SO</em></sub>
</p>
En la pestaña Sistema se mantiene el tipo de máquina `q35`, se selecciona firmware OVMF (UEFI) con su disco EFI en `local-lvm` y se utiliza el controlador VirtIO SCSI single.
<p align="center">
  <img src="Imagenes/paso_08b_vm_mint_sistema.png" alt="Asistente de creación de la VM: pestaña Sistema" width="500"><br>
  <sub><em>Figura 28. Asistente de creación de la VM: pestaña Sistema</em></sub>
</p>
En la pestaña Discos se define el primer disco (`scsi0`) sobre `local-lvm`, con un tamaño de 15 GiB y IO thread activado. La máquina dispone además de dos discos adicionales de 30 GiB, como se comprueba más adelante en el listado de dispositivos de bloque.
<p align="center">
  <img src="Imagenes/paso_08c_vm_mint_discos.png" alt="Asistente de creación de la VM: pestaña Discos" width="500"><br>
  <sub><em>Figura 29. Asistente de creación de la VM: pestaña Discos</em></sub>
</p>
Durante la instalación se realiza el particionado del disco del cliente. En la captura se asigna la partición `/dev/sdc1` (ext4, 32 GB aproximadamente) al punto de montaje `/home`, con la opción de formateo activada. El cargador de arranque se instala en el primer disco, `/dev/sda` (16,1 GB).
<p align="center">
  <img src="Imagenes/paso_09_particionado_mint.png" alt="Particionado del disco del cliente Linux Mint" width="500"><br>
  <sub><em>Figura 30. Particionado del disco del cliente Linux Mint</em></sub>
</p>
Finalmente se crean el usuario y el equipo: el nombre del equipo (hostname) y el usuario de la máquina (`mintmadrid`), con su contraseña. Se mantiene activada la opción de solicitar la contraseña para iniciar sesión.
<p align="center">
  <img src="Imagenes/paso_10_usuario_mint.png" alt="Creación del usuario y la contraseña del cliente Linux Mint" width="500"><br>
  <sub><em>Figura 31. Creación del usuario y la contraseña del cliente Linux Mint</em></sub>
</p>
3.11 Verificación del almacenamiento en Linux Mint
Ya instalado el cliente, se repiten las comprobaciones desde el terminal. Se lista el contenido de `/sys/firmware/efi`; la existencia de este directorio confirma que el sistema ha arrancado en modo UEFI, coherente con el firmware OVMF de la máquina virtual. Después se ejecuta `lsblk` con las columnas de nombre, sistema de ficheros, tamaño y punto de montaje.
```
$ ls -l /sys/firmware/efi
$ lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINTS
```
El resultado refleja el esquema de tres discos: `sda` (15 GB) con `/boot/efi` (vfat) y `/boot` (ext4), `sdb` (30 GB) con `/`, y `sdc` (30 GB) con `/home`. También aparece `sr0`, la unidad virtual con la ISO de Linux Mint.
<p align="center">
  <img src="Imagenes/paso_11_comandos_mint.png" alt="Listado de /sys/firmware/efi y salida de lsblk" width="500"><br>
  <sub><em>Figura 32. Listado de /sys/firmware/efi y salida de lsblk</em></sub>
</p>
Por último, se consulta el contenido de `/etc/fstab`. En este caso las particiones `/`, `/boot`, `/boot/efi` y `/home` se montan por UUID, con la opción `errors=remount-ro` en la raíz y `umask=0077` en la partición EFI. El área de intercambio se gestiona mediante el archivo `/swapfile` en lugar de una partición.
```
$ cat /etc/fstab
```
<p align="center">
  <img src="Imagenes/paso_12_fstab_mint.png" alt="Contenido del archivo /etc/fstab en Linux Mint" width="500"><br>
  <sub><em>Figura 33. Contenido del archivo /etc/fstab en Linux Mint</em></sub>
</p>
---
<div align="center">
Projecte Intermodular · Enric Soler i Godes · 2º ASIX · Grupo Madrid
</div>
