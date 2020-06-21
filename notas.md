# Administración de Servidores Linux

## Monitorear Recursos del Sistema

- `top` muestra en tiempo real todos los procesos del sistema, con el consumo de recursos.
- La cantidad de procesadores lógicos del sistema, y otra información de la CPU se encuentran en el archivo `/proc/cpuinfo`. Se puede ver esa información con los comandos `cat /proc/cpuinfo | grep processor`. El comando `top` mide el uso de los procesadores en la sección  `Load average`, medida cada 1, 5 y 15 minutos.
- `free -h` muestra información sobre la memoria disponible.
- `du -hsc <dirname>` muestra la memoria que está ocupando un directorio.
- `sudo ps auxf  | sort -nr -k 3 | head -5` muestra los procesos que más CPU usan (especificano `-k 3` , la tercera columna de la tabla de `ps auxf`)

