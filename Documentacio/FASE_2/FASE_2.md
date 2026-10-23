# PROJECTE INTERMODULAR

**ENRIC SOLER I GODES — 2 ASIX**

## GRUPO: MADRID

---

Descargamos la ISO correspondiente del “Proxmox”.

![Descarga de la ISO de Proxmox](Imagenes/pagina02_imagen1.png)

Descargamos el programa que sirve para cargar la ISO en el USB.

![Descarga de balenaEtcher](Imagenes/pagina02_imagen2.png)

Ahora preparamos todo para “flashear” la ISO en el USB.

![Preparación para flashear la ISO](Imagenes/pagina03_imagen1.png)

Encendemos el servidor y le instalamos el “Proxmox” a éste.

![Servidor encendido](Imagenes/pagina03_imagen2.png)

![Instalación de Proxmox](Imagenes/pagina03_imagen3.png)

Configuramos las Ips del servidor, y comprobamos si se han aplicado los cambios.

![Configuración de las IPs del servidor](Imagenes/pagina04_imagen1.png)

Instalamos el cliente de Linux Mint al ordenador (la captura es de Ubuntu Client porque probamos con este SO pero no funcionó y no hicimos fotos de la instalación de linux mint.)

![Instalación de Ubuntu](Imagenes/pagina05_imagen1.png)

Instalamos y configuramos el “Putty”, para abrir los puertos del switch y conectarlo a telnet.

![Instalación de Putty](Imagenes/pagina05_imagen2.png)

![Configuración de Putty](Imagenes/pagina05_imagen3.png)

Configuramos el switch.

![Switch (detalle)](Imagenes/pagina06_imagen1.png)

![Configuración del switch](Imagenes/pagina06_imagen2.png)

Comprobamos si los cambios se han guardado correctamente y vemos si nos podemos conectar al switch sin necesidad del “Putty”.

![Comprobación de la conexión por telnet](Imagenes/pagina06_imagen3.png)

Empezamos el día asignándole los nombres correspondientes a las VLAN.

![Nombres de las VLAN](Imagenes/pagina07_imagen1.png)

En la captura se accede a la interfaz GigabitEthernet 0/12 de un switch Cisco.
Una vez dentro, se configura esa interfaz en modo acceso (`switchport mode access`) y se le asigna la VLAN 210 (`switchport access vlan 210`).

![Configuración de la interfaz Gi0/12](Imagenes/pagina07_imagen2.png)

Repetimos el proceso con todas las VLAN

![Configuración del resto de VLAN](Imagenes/pagina08_imagen1.png)

Aquí ponemos el comando “`show vlan brief`” para verificar que hemos creado correctamente las VLAN. En la comprobación nos percatamos de que hemos hecho algunos erorres.

![Resultado de show vlan brief](Imagenes/pagina08_imagen2.png)

Corregimos los errores y volvemos a ejecutar el comando “`show vlan brief`” para ver si ya hemos corregido los errores.

![show vlan brief tras corregir](Imagenes/pagina09_imagen1.png)
