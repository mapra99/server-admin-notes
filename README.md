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

## Administración de Usuarios

### Creación de Usuarios y Contraseñas

- `id` muestra la identidad del usuario actual. Todo usuario tiene un id (`uid`), un id de grupo (`gid`) y los grupos a los que pertenece el usuario.

  En distribuciones Debian la creación de usuarios empieza desde el id 1000, y en Red Hat empieza desde el 500. El `uid` 0 está para el root.

- `/etc/paswd`es un archivo que contiene a todos los usuarios del sistema.

- `/etc/shadow` contiene las contraseñas de cada usuario (cifradas).

- `passwd <username> ` permite cambiar la contraseña de un usuario.

- `useradd <username> ` para crear un nuevo usuario.
- `adduser <username>` tambien sirve para crear un usuario, pero de forma interactiva. Crea una ruta para la carpeta home en `home/<username>`, y también pide una contraseña.
- `userdel <username>` borra un usuario.
- `su - <username>`  inicia sesión con ese nuevo usuario

### Grupos y Privilegios a Root

- groups <username> lista los grupos a los que pertenece el usuario
- `gpasswd -a <username> <groupname>` agrega al usuario a un grupo
- `usermod -aG <groupname> <username>` agrega al usuario a un grupo
- `gpasswd -d <username> <groupname>` elimina al usuario del grupo

### PAM para control de acceso de usuarios

Los archivos `/etc/pam.d/` contienen la configuración de PAM.

`/lib64/security/` contiene archivos de PAM sobre seguridad y privilegios

`/etc/security/` contiene otros archivos de configuración de seguridad.

#### `pwscore` para verificar fortaleza de una contraseña

Es una herramienta de la librería`libpwqualitytools`, sirve para revisar el nivel de seguridad de una contraseña.

`ulimit` muestra los limites que tiene el usuario sobre recursos del sistema.

`ulimit -u 10` cambia el numero maximo de procesos a 10

`"*;*;edison|nodejs;Wk0800-1800" > /etc/security/time.conf` para crear reglas sobre el acceso restringido por ssh en horarios determinados.



## Autenticación de Clientes y Servidores sobre SSH

Secure Shell (SSH) es el protocolo más usado para conectarse remotamente a servidores. OpenSSL es un paquete que permite realizar la configuración para este acceso. SSH funciona mediante encriptación en doble sentido, con una llave pública y una privada en cada lado.

En el servidor, el archivo`/etc/ssh/sshd_config` contiene opciones de configuración para la conexión SSH.

En el cliente, se debe generar una llave privada y una pública. Se puede usar el comando

`ssh-keygen`

La llave por defecto se guarda en `~/.ssh`. Se crea un archivo `id_rsa` con la llave privada y `id_rsa.pub` con la llave pública.

`ssh-copy-id -i ~/.ssh/id_rsa.pub tato-server@192.168.0.12` para enviar la llave pública del cliente al servidor.

`ssh -vvvv tato-server@192.168.0.12` para acceder remotamente. En el servidor con el comando  `hostname` se puede ver el nombre de red, y con `ifconfig` o `ip a` se puede ver la IP.

`sudo systemctl stop ssh` para detener la conexión

`sudo systemctl start ssh` para iniciar la ultima conexión otra vez

## Administración de Servicios

El comando `systemctl`

`sudo systemctl status apache2`

`sudo systemctl enable apache2`

`sudo systemctl stop apache2`

`sudo systemctl start apache2`

`sudo systemctl restart apache2`

`sudo systemctl list-units -t service --all`

`sudo journalctl -fu apache2 ` para ver los logs de algun servicio. Los logs se guardan en `/var/log/`

`sudo journalctl --disk-usage` para mirar el uso del disco. Tener cuidado con esto, se debe gestionar una forma de hacer backups y también ir borrando logs viejos para darle paso a nuevos.

`sudo journalctl -p crit` para mostrar los procesos que han tenido la palabra crit.

## Logs

- `find /var/log -iname "*.log" -type f`  busca todos los archivos que terminan en .log
- `find /var/log -mtime 2` busca todos los archivos que fueron modificados hace 2 días o menos

## Bash Scripting

