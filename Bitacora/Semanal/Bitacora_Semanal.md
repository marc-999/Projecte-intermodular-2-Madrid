# Bitácora Semanal del Grupo

*Secretario encargado:* Ismael Cerveró *(Suplente: Amin Boutighmass)*

---

## Semana 1

* **(a) Objetivo general del grupo:**
  * Crear el grupo de proyecto.
  * Asignar los roles de cada miembro del equipo.
  * Crear el README del proyecto.
* **(b) Qué hemos podido conseguir:**
  * Hemos conseguido con éxito todos los objetivos anteriores: el grupo de proyecto está creado, los roles están asignados y el README está creado.
* **(c) Qué NO hemos podido conseguir y por qué:**
  * Nada, porque hemos conseguido todos los objetivos marcados.

---

## Semana 2

* **(a) Objetivo general del grupo:**
  * Instalar el cliente de Ubuntu en el ordenador.
  * Instalar y configurar Putty para abrir los puertos del switch y conectarlo por telnet.
  * Realizar la configuración del switch.
  * Comprobar que los cambios se han guardado correctamente y que es posible conectarse al switch sin necesidad de Putty.
* **(b) Qué hemos podido conseguir:**
  * Hemos instalado el cliente de Ubuntu en el ordenador.
  * Hemos instalado y configurado Putty.
  * Hemos configurado el switch y hemos comprobado que la conexión por telnet funciona correctamente.
  * Hemos logrado todos los objetivos planteados para esta sesión.
* **(c) Qué NO hemos podido conseguir y por qué:**
  * No hemos podido dar por acabada del todo la configuración del switch porque no teníamos el cable SERIAL.

---

## Semana 3

* **(a) Objetivo general del grupo:**
  * Asignar los nombres correspondientes a las VLAN.
  * Configurar las interfaces del switch Cisco en modo acceso y asignarles su VLAN correspondiente.
  * Repetir el proceso con el resto de VLAN.
  * Verificar la configuración con el comando `show vlan brief` y corregir los posibles errores.
* **(b) Qué hemos podido conseguir:**
  * Hemos asignado los nombres a las VLAN y configurado las interfaces en modo acceso con su VLAN (por ejemplo, la interfaz GigabitEthernet 0/12 en la VLAN 210).
  * Hemos repetido el proceso con todas las VLAN.
  * Tras detectar algunos errores con `show vlan brief`, los hemos corregido y hemos verificado de nuevo la configuración.
  * Hemos conseguido todos los objetivos.
* **(c) Qué NO hemos podido conseguir y por qué:**
  * Nada, hemos logrado todo y no nos ha faltado nada.

---

## Semana 4

* **(a) Objetivo general del grupo:**
  * Corregir los errores generales de configuración detectados en las interfaces y reasignarlas a sus correspondientes VLANs.
  * Configurar los direccionamientos IP y los parámetros de red necesarios para permitir la comunicación entre el servidor y el cliente.
  * Verificar la conectividad abriendo la interfaz web de Proxmox desde el navegador del cliente.
* **(b) Qué hemos podido conseguir:**
  * Solucionamos los errores de configuración previos y reasignamos con éxito las interfaces a las VLANs designadas.
  * Establecimos y validamos la configuración de red IP, logrando la conectividad directa entre el cliente y el servidor.
  * Accedimos satisfactoriamente a la consola de administración de Proxmox mediante el navegador web del cliente.
  * Cumplimos con la totalidad de los objetivos planificados para la sesión.
* **(c) Qué NO hemos podido conseguir y por qué:**
  * Ninguno. Se completaron todas las tareas asignadas dentro del tiempo previsto.

---

## Semana 5

* **(a) Objetivo general del grupo:**
  * Desplegar y configurar una máquina virtual de Ubuntu Server sobre el entorno de virtualización Proxmox.
  * Desplegar y configurar una máquina virtual con el sistema operativo Linux Mint en Proxmox.
  * Instalar un sistema Ubuntu Server de forma nativa en un equipo cliente físico.
  * Instalar un sistema Linux Mint de forma nativa en otro equipo cliente físico.
* **(b) Qué hemos podido conseguir:**
  * Creamos y configuramos con éxito las dos máquinas virtuales (Ubuntu Server y Linux Mint) dentro del hipervisor Proxmox.
  * Realizamos la instalación y puesta a punto de Ubuntu Server en el equipo cliente designado.
  * Completamos la instalación de Linux Mint en el segundo equipo cliente.
  * Alcanzamos todos los objetivos marcados para la sesión de trabajo.
* **(c) Qué NO hemos podido conseguir y por qué:**
  * Ninguno. Todas las tareas de despliegue e instalación de sistemas operativos se completaron según lo previsto.

---

## Semana 6 (Práctica 4: Despliegue de servicios con Windows Server)

* **(a) Objetivo general del grupo:**
  * Elaborar el documento de planificación de la infraestructura (recursos de la máquina virtual, esquema de discos y volúmenes, esquema de red y justificación del nombre del servidor y del dominio).
  * Crear en Proxmox la máquina virtual `WS2025-ASIXXX` (UEFI, 2 vCPU, 8 GB de RAM y cuatro discos: 60 GB, 50 GB, 50 GB y 20 GB) e instalar Windows Server 2025 en modo UEFI/GPT.
  * Configurar el almacenamiento: inicializar los discos secundarios, crear los volúmenes simples, asignar letras de unidad y etiquetarlos (D: recursos compartidos, E: datos departamentales, F: copias de seguridad).
  * Configurar el TCP/IP del servidor (IP estática, máscara, puerta de enlace y DNS) y verificar la conectividad con `ipconfig /all` y `ping`.
* **(b) Qué hemos podido conseguir:**
  * Hemos elaborado el documento de planificación, instalado Windows Server 2025 en modo UEFI/GPT, configurado los discos secundarios (D:, E: y F:) y establecido el TCP/IP del servidor, verificando la conectividad.
  * Hemos conseguido todos los objetivos planteados para esta sesión.
* **(c) Qué NO hemos podido conseguir y por qué:**
  * Nada, hemos logrado todos los objetivos marcados.

---

## Semana 7 (Práctica 4: DHCP y DHCP Snooping)

* **(a) Objetivo general del grupo:**
  * Instalar el rol de servidor DHCP en Windows Server 2025, completar la configuración posterior a la instalación y autorizar el servidor en Active Directory (si forma parte del dominio).
  * Crear y activar un ámbito adecuado a la red asignada (rango, máscara, exclusiones) y configurar sus opciones (puerta de enlace, DNS y nombre de dominio).
  * Comprobar que un cliente virtual obtiene la configuración por DHCP y asignar una IP fija mediante reserva DHCP a un equipo cliente físico.
  * Desplegar un servidor DHCP fraudulento (*rogue DHCP*) en una máquina física con Ubuntu Server, con una configuración errónea controlada, y comprobar que sin protección un cliente puede recibir su oferta.
  * Activar DHCP Snooping en el switch Cisco, configurar como *trusted* únicamente el puerto del servidor Windows y mantener *untrusted* el resto de puertos.
  * Verificar con `show ip dhcp snooping` y `show ip dhcp snooping binding` que se descartan las respuestas del servidor Ubuntu y que los clientes siguen recibiendo la configuración correcta de Windows Server.
  * Documentar la topología (máquinas y puertos) y recoger las capturas necesarias, y actualizar la documentación del proyecto y el repositorio.
* **(b) Qué hemos podido conseguir:**
  * Hemos instalado y autorizado el rol DHCP, creado y activado el ámbito con sus opciones y asignado una IP fija por reserva al cliente físico.
  * Hemos desplegado el servidor DHCP fraudulento en Ubuntu Server y configurado DHCP Snooping en el switch Cisco, verificando que se bloquean sus respuestas y que los clientes reciben la configuración correcta de Windows Server.
  * Hemos conseguido todos los objetivos.
* **(c) Qué NO hemos podido conseguir y por qué:**
  * Nada, hemos logrado todos los objetivos marcados.
