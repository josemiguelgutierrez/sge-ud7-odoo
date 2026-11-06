# Errores de instalación

He instalado Odoo 19 Community con Docker Compose en Windows. Estos son los errores que me han salido y cómo los he solucionado.

| # | Error | Causa | Solución | Fuente |
|---|---|---|---|---|
| 1 | Docker Desktop no arrancaba y decía `Virtualization support not detected` | Tenía la virtualización desactivada en la BIOS y Docker la necesita para funcionar | Entré en la BIOS, activé la virtualización del procesador y reinicié. Luego miré en el Administrador de tareas, en Rendimiento > CPU, que pusiera Virtualización: Habilitado | [Docker docs](https://docs.docker.com/desktop/troubleshoot-and-support/troubleshoot/topics/#virtualization) |
| 2 | En clase, después de activar la virtualización, Docker Desktop seguía sin arrancar y pedía WSL 2 | No tenía instalado WSL 2, que es lo que usa Docker en Windows para funcionar | Abrí PowerShell como administrador, puse `wsl --install` y reinicié el ordenador | [Microsoft Learn](https://learn.microsoft.com/es-es/windows/wsl/install) |
| 3 | En casa, al poner `docker compose up -d` me salió `error during connect ... dockerDesktopLinuxEngine: The system cannot find the file specified` | No tenía abierto Docker Desktop | Abrí Docker Desktop, esperé a que estuviera en verde y volví a poner `docker compose up -d` | [Docker docs](https://docs.docker.com/desktop/setup/install/windows-install/) |

## Por qué los errores 1 y 2 van juntos

Docker en Windows necesita una máquina virtual de Linux. Para eso hace falta tener la virtualización activada en la BIOS y además tener WSL 2 instalado. A mí me faltaban las dos cosas, por eso después de arreglar la BIOS me seguía fallando hasta que instalé WSL.

## Comprobaciones

- Con `docker --version` comprobé que Docker estaba instalado.
- Con `docker ps` vi que los dos contenedores estaban en Up y que odoo-web usaba el puerto 8069.
- Entré en `http://localhost:8069` y Odoo cargaba bien.