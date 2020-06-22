# Administración de Servidores Linux

## Monitorear Recursos del Sistema

- `top` muestra en tiempo real todos los procesos del sistema, con el consumo de recursos.
- La cantidad de procesadores lógicos del sistema, y otra información de la CPU se encuentran en el archivo `/proc/cpuinfo`. Se puede ver esa información con los comandos `cat /proc/cpuinfo | grep processor`. El comando `top` mide el uso de los procesadores en la sección  `Load average`, medida cada 1, 5 y 15 minutos.
- `free -h` muestra información sobre la memoria disponible.
- `du -hsc <dirname>` muestra la memoria que está ocupando un directorio.
- `sudo ps auxf  | sort -nr -k 3 | head -5` muestra los procesos que más CPU usan (especificano `-k 3` , la tercera columna de la tabla de `ps auxf`)

### Recursos de Red

**Direcciones IP Privadas y Públicas**

Los comandos `ifconfig` o `ip a` muestran información sobre las tarjetas de red del equipo.

Las IP Privadas (`inet`) se pueden acceder sólo dentro de la red local.

Con `hostname`  se puede ver el nombre con el que se identifica el equipo en las redes.

Con `route -n` se pueden ver los endpoints de la red.

## Gestión de Paquetes

### Red Hat / CentOS / Fedora

Extensión .rpm (red hat package management)

Se puede instalar un paquete con el comando rpm o desde repositorios con gestor de paquetes yum.

La base de datos de rpm está localizada en `/var/lib/rpm`

- `rpm -qa` para listar todos los rpms instalados en la máquina
- `rpm -i <filename.rpm>` para instalar un paquete desde un archivo
- `rpm -e <filename.rpm>` para remover un paquete desde un archivo
- `yum install <packageName>` para instalar un paquete desde repositorios

### Debian/Ubuntu

Extensión .deb

Se puede instalar un paquete con el comando dpkg o desde repositorios con gestor de paquetes apt o snap.

La base de datos está localizada en `/var/lib/dpkg`

- `dpkg -l` para listar todos los debs instalados
- `dpkg -i <filename.deb>` para instalar un paquete desde un archivo
- `dpkg -r <filename.deb>` para remover un paquete desde un archivo.
- `dpkg-reconfigure <packageName>` para reconfigurar un paquete, si el paquete dispone de una reconfiguración
- `apt install <packageName>` para instalar un paquete desde repositorios. `apt` y `apt-get` son lo mismo.

