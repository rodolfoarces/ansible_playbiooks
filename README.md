# Ansible Playbooks

Este es mi repositorio personal de Ansible playbooks para varias tareas

## Hosts

La mayoría de los hosts a utilizar en estos plyabooks estab basados en máquinas virtuales de uso internos al hosty físico por lo cual veran varias direcciones como: 127.0.0.1, locahost, *.local, etc.

Esto esta basado en la gestión de VMs del proyecto [vagrant boxes](https://github.com/rodolfoarces/vagrant_boxes)


## Organización de los proyectos

### Inventario

Los hosts estan organizados por plataforma o distribución, y luego subdivididos por versiones generales. Esto es porque se aplicarán los playbooks a grupos de servidores con el mismo comportamiento esperado. También se desarrollan playbooks para servidores que ya están descontinuados y pueden requerir configuraciones particulares.

### Playbooks

Los playbooks estan organizados en archivos con el nombre para la plataforma pero con el "hosts" aplicado a la versión más particular.

Ejemplo:

[centos_base_tool.yml](Playbooks/centos_base_tool.yml) -> *hosts: centos* (Se aplica a todos los hosts centos)

[centos_join_ad.yml](Playbooks/centos_base_tool.yml)  -> *hosts: centos8* (Se aplica solo a los servidores centos8)

### Files

Archivos para copiar a los servidores, debieran ser genéricos y utilizables en todas las distribuciones, en algunos casos, los archivos serán especificos para distrubuciones, el nombre lo indicará.

## Uso general

**-i** Archivo de inventario de hosts.

**-b** Archivo de playbook a ejecutarse.

**-u** Usuario del S.O. destino a ser usado por Ansible para es despliegue.

**--private-key** la llave privada SSH para usar en la conexión con el host.


```
ansible-playbook \
-i ~/ansible_playbooks/Inventory/vagrantboxes.yml \
-u vagrant --private-key="~/.ssh/id_rsa" \
-b ~/ansible_playbooks/Playbooks/centos_base_tools.yml
```

Otra forma de usar es setear en el playbook que se aplique a "hosts: all" pero en el comando indicar que limite (--limit) sólo a ciertos

```
ansible-playbook -i Inventory/vms.yml --limit redhat8 Playbooks/centos_base_tools.yml --user=root
```

## Licencia

Todo el código está disponible bajo la [licencia](LICENSE) GNU GPL v3
