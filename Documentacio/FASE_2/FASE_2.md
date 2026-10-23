# PROJECTE INTERMODULAR

**ENRIC SOLER I GODES — 2 ASIX**

## GRUPO: MADRID

---

## Instalación del Proxmox y configuración de las IP del servidor.

Descargamos la ISO correspondiente del “Proxmox”.

[🖼️ Ver imagen: descarga de la ISO de Proxmox](Imagenes/pagina03_imagen1.png)

Descargamos el programa que sirve para cargar la ISO en el USB.

[🖼️ Ver imagen: descarga de balenaEtcher](Imagenes/pagina03_imagen2.png)

Ahora preparamos todo para “flashear” la ISO en el USB.

[🖼️ Ver imagen: preparación para flashear la ISO](Imagenes/pagina04_imagen1.png)

Encendemos el servidor y le instalamos el “Proxmox” a éste.

[🖼️ Ver imagen: servidor encendido](Imagenes/pagina04_imagen2.png)

[🖼️ Ver imagen: instalación de Proxmox](Imagenes/pagina04_imagen3.png)

Configuramos las Ips del servidor, y comprobamos si se han aplicado los cambios.

[🖼️ Ver imagen: configuración de IPs del servidor](Imagenes/pagina05_imagen1.png)

---

## Instalación del SO y configuración del switch CISCO.

Instalamos el cliente de Linux Mint al ordenador.

Instalamos y configuramos el “Putty”, para abrir los puertos del switch y conectarlo a telnet.

[🖼️ Ver imagen: instalación de Putty (1)](Imagenes/pagina06_imagen2.png)

[🖼️ Ver imagen: configuración de Putty (2)](Imagenes/pagina06_imagen3.png)

Configuramos el switch.

[🖼️ Ver imagen: switch (detalle)](Imagenes/pagina07_imagen1.png)

[🖼️ Ver imagen: configuración del switch](Imagenes/pagina07_imagen2.png)

Comprobamos si los cambios se han guardado correctamente y vemos si nos podemos conectar al switch sin necesidad del “Putty”.

[🖼️ Ver imagen: comprobación de la conexión por telnet](Imagenes/pagina07_imagen3.png)

---

## Configuración de las VLAN

Empezamos el día asignándole los nombres correspondientes a las VLAN.

[🖼️ Ver imagen: nombres de las VLAN](Imagenes/pagina08_imagen1.png)

En la captura se accede a la interfaz GigabitEthernet 0/12 de un switch Cisco.
Una vez dentro, se configura esa interfaz en modo acceso (`switchport mode access`) y se le asigna la VLAN 210 (`switchport access vlan 210`).

[🖼️ Ver imagen: configuración de la interfaz Gi0/12](Imagenes/pagina08_imagen2.png)

Repetimos el proceso con todas las VLAN

[🖼️ Ver imagen: configuración del resto de VLAN](Imagenes/pagina09_imagen1.png)

Aquí ponemos el comando “`show vlan brief`” para verificar que hemos creado correctamente las VLAN. En la comprobación nos percatamos de que hemos hecho algunos erorres.

[🖼️ Ver imagen: resultado de show vlan brief](Imagenes/pagina09_imagen2.png)

Corregimos los errores y volvemos a ejecutar el comando “`show vlan brief`” para ver si ya hemos corregido los errores.

[🖼️ Ver imagen: show vlan brief tras corregir](Imagenes/pagina10_imagen1.png)
