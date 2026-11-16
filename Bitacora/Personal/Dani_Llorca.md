## Bitácora Personal: Daniel Llorca (Semana 1)

**Fecha:** [2026-09-18]

- **a. Objetivo del día:**
  - Coordinar la creación del grupo de proyecto y asegurar que todos los miembros tengan sus roles asignados correctamente.
  - Liderar la creación y estructura inicial del archivo README del proyecto.

- **b. Qué se ha hecho:**
  - Se ha organizado una reunión inicial para establecer el grupo de proyecto.
  - Se han definido y asignado los roles de cada integrante del equipo.
  - Se ha redactado y creado conjuntamente el README del proyecto.

- **c. Qué se ha podido conseguir:**
  - El grupo de proyecto se ha creado con éxito.
  - Los roles están perfectamente asignados y asumidos por el equipo.
  - El README del proyecto está completado y publicado.

- **d. Qué NO se ha podido conseguir y por qué:**
  - Nada, ya que se han cumplido todos los objetivos planificados para la primera sesión.

---

## Bitácora Personal: Daniel Llorca (Semana 2)

**Fecha:** [2026-09-25]

- **a. Objetivo del día:**
  - Supervisar la instalación del cliente de Ubuntu en el ordenador del equipo.
  - Coordinar la instalación y configuración de Putty para la apertura de puertos del switch y su conexión por telnet.
  - Gestionar la configuración del switch y verificar su persistencia y acceso sin Putty.

- **b. Qué se ha hecho:**
  - He supervisado y apoyado en la instalación del cliente de Ubuntu.
  - He participado en la configuración de Putty y en los ajustes necesarios para la conexión.
  - He dirigido los pasos para la configuración del switch y las comprobaciones de conexión por telnet.

- **c. Qué se ha podido conseguir:**
  - Instalación exitosa del cliente de Ubuntu en el equipo.
  - Putty instalado y configurado correctamente.
  - Configuración del switch completada y verificación de que la conexión por telnet funciona de forma adecuada.

- **d. Qué NO se ha podido conseguir y por qué:**
  - No se ha podido finalizar por completo la configuración del switch porque no disponíamos del cable SERIAL necesario en ese momento.

---

## Bitácora Personal: Daniel Llorca (Semana 3)

**Fecha:** [2026-10-23]

- **a. Objetivo del día:**
  - Guiar al equipo en la asignación de nombres correspondientes a las VLAN.
  - Coordinar la configuración de las interfaces del switch Cisco en modo acceso y la asignación de sus respectivas VLAN.
  - Verificar la correcta implementación mediante el comando `show vlan brief` y corregir posibles incidencias.

- **b. Qué se ha hecho:**
  - He coordinado la asignación de nombres a las VLAN y la configuración de las interfaces en modo acceso (por ejemplo, asignando la interfaz GigabitEthernet 0/12 a la VLAN 210).
  - He supervisado la repetición del proceso para el resto de las VLAN.
  - He participado en la revisión del comando `show vlan brief`, la detección de pequeños errores y su subsanación.

- **c. Qué se ha podido conseguir:**
  - Todas las VLAN tienen sus nombres e interfaces configuradas correctamente en modo acceso.
  - Se ha revisado y verificado la configuración completa tras corregir los errores detectados.
  - Se han alcanzado todos los objetivos previstos para esta sesión.

- **d. Qué NO se ha podido conseguir y por qué:**
  - Nada, se ha logrado completar todo el plan de trabajo sin incidencias bloqueantes.

  ---

# Bitácora Personal: Daniel Llorca (Semana 4)

**Fecha:** [2026-11-06]

* **a. Objetivo del día:**
   * Coordinar al equipo para verificar la conectividad entre el cliente y el servidor mediante `ping`.
   * Liderar el acceso a la interfaz web de Proxmox, la carga de la imagen ISO y la creación de la máquina virtual Ubuntu Server.
   * Supervisar el esquema de particionado del servidor según el enunciado (Tarea 1) y la instalación del cliente Linux Mint.
   * Verificar el almacenamiento de ambos equipos y revisar la documentación del esquema de red.
* **b. Qué se ha hecho:**
   * He coordinado la comprobación de conectividad con `ping` entre el cliente y el servidor, y la documentación del esquema de red (dispositivos, VLAN y puertos del switch).
   * He dirigido el acceso a Proxmox desde el navegador y la carga de la ISO en el almacenamiento del nodo.
   * He supervisado la creación de la máquina virtual Ubuntu Server (arranque UEFI, 2 núcleos, 4096 MiB de memoria) y el reparto de los discos: `/boot/efi` y `/boot` en el primero, `/` en el segundo, `/home` en el tercero y swap en el cuarto.
   * He participado en la configuración del nombre del servidor y del usuario.
   * He coordinado las comprobaciones desde la terminal (`ls /sys`, `df -h` y el contenido de `/etc/fstab`).
   * He supervisado la creación de la máquina virtual del cliente Linux Mint con sus tres discos, su particionado y la creación del usuario, y la repetición de las comprobaciones (`lsblk` y `/etc/fstab`).
* **c. Qué se ha podido conseguir:**
   * Conectividad correcta entre cliente y servidor.
   * Acceso a Proxmox por navegador y carga de la ISO completada.
   * Servidor Ubuntu instalado con las particiones planificadas, que se confirman en la salida de `df -h` y en `/etc/fstab`.
   * Cliente Linux Mint instalado y particionado, con `/boot/efi` y `/boot` en el primer disco, `/` en el segundo y `/home` en el tercero.
   * Documentación del esquema de red y del particionado completada y revisada.
* **d. Qué NO se ha podido conseguir y por qué:**
   * Nada, ya que se han resuelto con éxito todos los objetivos planificados para la sesión.
