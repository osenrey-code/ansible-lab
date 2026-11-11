# Práctica 2do Parcial: Ansible con Docker

## Objetivo

Crear un laboratorio con dos servidores Linux Ubuntu ejecutándose en Docker y administrarlos con Ansible. El playbook identifica cada servidor, muestra su sistema operativo, crea `/tmp/ansible-demo`, escribe `info.txt`, genera los directorios `logs`, `backup` y `config`, y muestra un mensaje cuando el sistema es Ubuntu.

## Estructura

```text
ansible-lab/
├── docker-compose.yml
├── inventory.ini
├── playbook.yml
└── README.md
```

## Iniciar los servidores

Desde esta carpeta:

```bash
docker compose up -d
docker ps
```

Los contenedores se llaman `server1` y `server2` y usan `ubuntu:24.04`.

## Ejecutar Ansible

Si Ansible está instalado localmente:

```bash
ansible docker -i inventory.ini -m ping
ansible-playbook -i inventory.ini playbook.yml
```

En Windows, si Ansible no está instalado localmente, se puede ejecutar con una imagen de Ansible y el socket de Docker:

```bash
docker run --rm -it \
  -v //var/run/docker.sock:/var/run/docker.sock \
  -v "$PWD:/ansible-lab" \
  -w /ansible-lab \
  quay.io/ansible/ansible-runner:latest \
  ansible-playbook -i inventory.ini playbook.yml
```

## Resultado esperado

En ambos servidores se crea la siguiente estructura:

```text
/tmp/ansible-demo/
├── info.txt
├── logs/
├── backup/
└── config/
```

La salida debe mostrar el nombre de cada host, Ubuntu 24.04 y el mensaje de laboratorio configurado correctamente.

## Evidencia de ejecución

Pegar aquí una captura de pantalla de la ejecución exitosa de `ansible-playbook` y de los dos contenedores activos.

## Entrega

Subir esta carpeta completa a un repositorio público de GitHub y pegar aquí el enlace del repositorio.
