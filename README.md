![Platform: ALL](https://img.shields.io/badge/platform-ALL-green)
![Follow @NUCC Inc. on Twitter](https://img.shields.io/twitter/follow/nucc_inc?label=follow&style=social)
![Tweet about this Project](https://img.shields.io/twitter/url?style=social&url=https%3A%2F%2Fgithub.com%2Fphx%2Fnucc)

![NUCC logo](./logo.png?raw=true)

# NUCC Computación Distribuida para la Ayuda en la Investigación del COVID-19

<<<<<<< HEAD
> Repositorio original creado por [Phoenix](https://github.com/phx)
> Traduccion por [theJuan](https://github.com/theJuan1112)
- [English Version](https://github.com/phx/nucc)
=======
**Latest Update: March 30, 2020**
>>>>>>> upstream/master

**Ultima Actualización: Marzo 28, 2020**

Únete al [National Upcycled Computing Collective (NUCC)](https://www.nuccinc.org/) en un esfuerzo colaborativo para combinar nuestros recursos computacionales para ayudar en la investigación del COVID-19.
Este proyecto se basa en [la configuracion predeterminada de Docker creado por BOINC](https://github.com/BOINC/boinc-client-docker). La diferencia es que no hay que registrar ninguna cuenta y no comparte información personal. Solamente es utilizada para conectarse automáticamente al proyecto en curso de NUCC en [Rosseta@home](https://boinc.bakerlab.org/), que es un equipo de investigación el cual esta activamente procesando cargas especificas de el COVID-19.

---

### La forma mas rapida y facil de contribuir si ya tienes BOINC instalado:
- Windows:
  - `boinccmd --project_attach http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec`
- Cualquier otro sistema operativo:
  - `boinccmd --attach_project http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec`

### La forma mas rapida y facil de contribuir si ya tienes Docker instalado es la siguiente:

Copiar y pegar la siguiente linea en tu terminal para comenzar inmediatamente en MacOS o Linux:

`docker run -d --restart always --name boinc -p 31416 -v "${HOME}/.boinc:/var/lib/boinc" -e BOINC_GUI_RPC_PASSWORD="123" -e BOINC_CMD_LINE_OPTIONS="--allow_remote_gui_rpc --attach_project http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec" boinc/client:baseimage-alpine`


### The fastest and easiest way to contribute if you already have BOINC installed natively:
- Windows:
  - `C:\PROGRA~1\BOINC\boinccmd.exe --project_attach http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec`
- MacOS:
  - `(/Applications/BOINCManager.app/Contents/Resources/boinc -redirectio "/Library/Application Support/BOINC Data/" --daemon --attach_project http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec &) >/dev/null 2>&1 && open /Applications/BOINCManager.app`
- Linux:
  - `boinccmd --project_attach http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec`

Note: If you don't have things configured exactly right, you may have to pass the password located in `gui_rpc_passwd.cfg` in the command line to `boinccmd`.

Example: `boinccmd --passwd <yourpassword> --project_attach http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec`

---

<<<<<<< HEAD
## Contenido

- [Instalación Nativa de Windows](#instalaci%c3%b3n-nativa-de-windows)
- [Instalacion de Docker en Windows](#instalacion-de-docker-en-windows)
- [Instalacion en BSD Jail](#instalacion-bsd-jail)
- [Instalacion de Docker en MacOS/Linux](#instalacion-de-docker-en-linux-y-macos)
- [Arquitectura y Etiquetas Compatibles](#arquitecturas-y-etiquetas-compatibles)
- [Modo Docker Swarm](#modo-docker-swarm)
- [Ver y Administrar cargas de trabajo](#ver-y-administrar-cargas-de-trabajo)
- [Comandos para BOINC](#comandos-para-boinc-y-atajos)
- [Actualizaciones](#actualizaciones)
- [Sobre NUCC](#sobre-el-national-upcycled-computing-collective-nucc)

---

## Instalación Nativa de Windows:
=======
**Contents**
- [Automated Linux/MacOS Docker-based Installation](#automated-linux-and-macos-docker-installation)
- [Automated Windows Native Installation](#automated-windows-native-installation)
- [Automated Windows Docker-based Installation](#windows-docker-installation)
- [Automated MacOS Native Installation](#automated-macos-native-installation)
- [BSD Jail Installation](#bsd-jail-installation)
- [Manual Installation](#manual-installation)
- [Docker Supported Architectures and Tags](#docker-supported-architectures-and-tags)
- [Docker Swarm Mode](#docker-swarm-mode)
- [Viewing and Managing Workloads](#viewing-and-managing-workloads)
- [BOINC Commands and Shortcuts](#boinc-commands-and-shortcuts)
- [Updates](#updates)
- [About NUCC](#about-the-national-upcycled-computing-collective)

---

## Automated Linux and MacOS Docker Installation

If Docker is not already installed, the [`quickstart.sh`](quickstart.sh) script will install Docker via [The Almost Universal Docker Installer](https://github.com/phx/dockerinstall),
then pull [the official boinc/client image from DockerHub](https://hub.docker.com/r/boinc/client) ([`base-alpine`](https://github.com/BOINC/boinc-client-docker/blob/master/Dockerfile.base-alpine) by default).

You can run a custom image by running `IMG=boinc/client[tag-name] ./quickstart.sh` (see [Supported Architectures and Tags](#docker-supported-architectures-and-tags)).

- MacOS 10.8+
- Ubuntu
- Debian 8+
- Raspbian 8+
- CentOS/RHEL/Amazon Linux
- Fedora 30+
- Kali 2018+ (based on Debian Stretch)
- Arch

```
git clone http://github.com/phx/nucc.git
cd nucc
./quickstart.sh
```

*If the script errors out after installing Docker, run it again in a new login shell that recognizes your user as a member of the `docker` group, and you should be squared away.*

#### Firewall Caveats:

If you are running `firewalld` or `ufw` or something like that, you will need to either create a rule for the `docker0` interface on port `31416`.

Alternately, you can disable the service altogether by running `systemctl disable firewalld` (etc.), and then rebooting.

This is necessary to be able to resolve DNS inside the containers.

If you have already installed and spun up a container via `quickstart.sh`, just implement the firewall rules and run `docker restart boinc`.

If you disable the firewall completely, the `boinc` container should spin up immediately after reboot and will be able to process workloads successfully.

---

## Automated Windows Native Installation:
>>>>>>> upstream/master

Descarga el archivo zip del repositorio, descomprimirlo, y ejecuta `quickstart.bat --native --attach` desde la Consola CMD en modo Administrador.

Otra alternativa es si tienes `git` instalado, en tu Consola CMD (Administrador) ejecuta los siguientes comandos:

```
git clone https://github.com/theJuan1112/nucc.git
cd nucc
quickstart.bat --native --attach
```

Esto instalara el administrador de paquetes [Chocolatey](https://chocolatey.org/), que a su vez instalara BOINC.

Automáticamente lanzara el BOINC Manager, en este momento esperaras hasta que la ventana *Select a Project* aparezca.

Cierra la ventana, confirma, y presiona enter para continuar ejecutando el script.

Este se va a conectar automáticamente al proyecto correcto y comenzara a procesar las cargas de trabajo inmediatamente.

<<<<<<< HEAD
## Instalacion de Docker en Windows:
=======
I find it easier to view and manage by going to `View > Advanced`, as things appear to be more organized.

## Windows Docker Installation:
>>>>>>> upstream/master

Descarga el archivo zip del repositorio, descomprimirlo, y ejecuta `quickstart.bat` desde la Consola CMD en modo Administrador.

Otra alternativa es si tienes `git` instalado, en tu Consola CMD (Administrador) ejecuta los siguientes comandos:

```
git clone https://github.com/theJuan1112/nucc.git
cd nucc
quickstart.bat --docker
```
Esto instalara el administrador de paquetes [Chocolatey](https://chocolatey.org/), que a su vez instalara Docker Desktop.

Cuando Docker Desktop es abierto por primera vez, necesitaras cerrar sesión e iniciar sesión otra vez para que termine de comenzar.

- Click derecho en el icono de Docker en la barra de tareas
- Ir a Preferencias > Recursos > Compartir Archivos
- Habilita el C Drive
- Click en "Aplicar y Reiniciar"
- Esperar hasta que Docker termine *Completamente* de reiniciar.
- Ejecuta `quickstart.bat --docker` en tu consola CMD en modo Administrador, para comenzar a  procesar las cargas de trabajo inmediatamente.

*Cuando ejecutas por primera vez una imagen de Docker, Windows te preguntara para confirmar si Docker puede acceder a tu C: Drive.*

---

<<<<<<< HEAD
## Instalacion BSD Jail
=======
## Automated MacOS Native Installation

```
git clone https://github.com/phx/nucc
cd nucc
./quickstart.sh --native
```

---

## BSD Jail Installation
>>>>>>> upstream/master

**[Documentación para FreeBSD (específicamente, FreeNAS) se puede encontrar en el este blog post (INGLES)](https://bookandcode.com/nuccbsd)**

---

<<<<<<< HEAD
## Instalacion de Docker en Linux y MacOS

### Si NO tienes Docker Instalado:

- Debian 8+
- Raspbian 8+
- Ubuntu
- Fedora 30+
- Kali 2018+ (basado en Debian Stretch)
- Arch
- MacOS 10.8+
- CentOS/RHEL/Amazon Linux

```
git clone http://github.com/theJuan1112/nucc.git
cd nucc
./quickstart.sh
```

*Si el script crea un error despues de instalar Docker, ejecuta otra vez otro Shell que reconozca tu usuario como miembro del grupo `docker`*

### Si ya tienes Docker instalado:

```
git clone http://github.com/theJuan1112/nucc.git
cd nucc
./quickstart.sh
```
=======
## Manual Installation

Follow [the official instructions](https://boinc.berkeley.edu/wiki/Installing_BOINC) to install BOINC locally.

After starting BOINC, cancel out of the "Select a Project" window if it pops up, and run the command below to start choochin':

`boinccmd --project_attach http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec`

If running on Linux or MacOS, you may find it easier to go to `View > Advanced` to monitor things.

**Note:** `boinccmd` is typically only in your `$PATH` on Linux. 

---

## Docker Supported Architectures and Tags

Not all of the BOINC images below are compatible with the COVID-19 Rosetta@home workloads.  To be perfectly clear, Rosetta@home
is only handing out ***processor-focused*** workloads.  This means if you want to take advantage of your beefy GPU, you will be better off
focusing on something like [Folding@home](https://foldingathome.org/), which can take advantage of that.  Also, Rosetta@home is not currently
supporting ARM-based workloads.

The current issue with Folding@home is that the number of servers sending data back is causing a DDOS on their systems as they are receiving the folded results.
As a result of this, the work units aren't finishing, and no work can be handed out.  They have engaged several companies to help, but this is the primary reason
for NUCC choosing to work with Rosetta@home for the COVID-19 research in particular, as they are handing out 100% COVID-19-specific work units immediately and efficiently.
>>>>>>> upstream/master

NUCC will have additional projects in the future with [Folding@home](https://foldingathome.org/) and [GPUGRID](https://gpugrid.net/),
and we will continue to update this page with instructions on how to connect to those particular projects.

However, in the meantime, [Rosetta@home](https://boinc.bakerlab.org/) remains the best possible solution for continuously receiving
and processing workloads that specifically target COVID-19 in particular, which is why NUCC has chosen the current solution.   

<<<<<<< HEAD
#### Consideraciones del Firewall:

Si estas usando `firewalld` o `ufw` o algo parecido, necesitaras que crear una regla para la interfaz `docker0` en el puerto `31416`

Alternativamente puedes deshabilitar el servicio ejecutando `systemctl disable firewalld` (etc.), y reiniciando el systema.

Esto es necesario para resolver DNS dentro del contenedor

Si ya instalaste y tienes un contenedor usando `quickstart.sh`, solo implementa las reglas del firewall y ejecuta `docker restart boinc`

Si desabilitas el firewall completamente, el contenedor `boinc` deberia funcionar immediatamente despues de reiniciar y procesara las cargas de trabajo satisfactoriamente.
---

## Arquitecturas y Etiquetas compatibles

Puedes especializar la imagen de `boinc/client` con cualquiera de las siguientes etiquetas para usar una version de contenedor especializada.

Este se puede usar en el comando de Linux/MacOS al comienzo de este documento y pasarlo como la variable de entorno `$IMG` para `quickstart.sh`
=======
BOINC's default image is `baseimage-ubuntu` or `latest`, which uses `glibc`, however NUCC's default image from the quickstart scripts
is `baseimage-alpine`, which uses `musl` instead.  If this causes any issues with future projects, we will change to the Ubuntu base image,
but for now, Alpine is working perfectly with our Rosetta@home workloads, and the image itself is much leaner, which was our reason for choosing
it as our default. 

If you wish, you can specify the `boinc/client` image with any of the tags below in order to use one of the specialized versions instead of `baseimage-alpine`.

These can be used in the Linux/MacOS one-liner at the top of this page or passed as the `$IMG` environment variable to `quickstart.sh`:
- `IMG=boinc/client:[image-name] ./quickstart.sh`

They can also be passed as a command line argument to to `quickstart.bat`:
- `quickstart.bat --docker --image boinc/client:[image-name]`

---
>>>>>>> upstream/master

### x86-64
| Tag | Info |
| :--- | :--- |
| `latest`, `baseimage-ubuntu` | Cliente BOINC basado en Ubuntu. Todas la imagenes de BOINC son basadas en **x86-64** |
| `baseimage-alpine` | Cliente BOINC basado en Alpine, el cual es menos pesado y utilizado por defecto en [`quickstart.bat`](quickstart.bat) y [`quickstart.sh`](quickstart.sh) |
| `amd` | Cliente BOINC para AMD GPU. Revisar uso [abajo](#amd-gpu-savvy-boinc-client-usage). |
| `intel` | Cliente BOINC para Intel GPU. Soporta Broadwell (5th Generacion) CPUs y despues. Revisar uso [abajo](#intel-gpu-savvy-boinc-client-usage). |
| `intel-legacy` | Cliente BOINC para generacion anterior de Intel GPU (Sandybridge - 2nd Gen, Ivybridge - 3rd Gen, Haswell - 4th Gen). Revisar uso [abajo](#legacy-intel-gpu-savvy-boinc-client-usage). |
| `multi-gpu` | Cliente BOINC para Intel & Nvidia. Revisar uso [abajo](#multi-gpu-savvy-boinc-client-usage). |
| `nvidia` | Cliente BOINC para NVIDIA (CUDA & OpenCL). Revisar uso [abajo](#nvidia-savvy-boinc-client-usage). |
| `virtualbox` | Cliente BOINC para VirtualBox. Revisar uso [abajo](#virtualbox-savvy-boinc-client-usage). |

### ARM
| Tag | Info |
| :--- | :--- |
| `arm32v7` | Cliente BOINC para ARMv7 32-bit. Revisar uso [abajo](#armv7-32-bit-savvy-boinc-client-usage). |
| `arm64v8` | Cliente BOINC para ARMv8 64-bit. Revisar uso [abajo](#armv8-64-bit-savvy-boinc-client-usage). |


#### AMD GPU-savvy BOINC client usage
- Instalar el [ROCm Driver](https://rocm.github.io/ROCmInstall.html).
- Reiniciar tu sistema.
- Ejecuta el siguiente comando.
  - Linux: `IMG=boinc/client:amd ./quickstart.sh`
  - Windows: `quickstart.bat --docker --image boinc/client:amd`

#### Intel GPU-savvy BOINC client usage
- Instalar el Intel GPU Driver.
- Ejecuta el siguiente comando:
  - Linux: `IMG=boinc/client:intel ./quickstart.sh`
  - Windows: `quickstart.bat --docker --image boinc/client:intel`

#### Legacy Intel GPU-savvy BOINC client usage
- Instalar el Intel GPU Driver.
- Ejecuta el siguiente comando:
  - Linux: `IMG=boinc/client:intel-legacy ./quickstart.sh`
  - Windows: `quickstart.bat --docker --image boinc/client:intel-legacy`

#### Multi GPU-savvy BOINC client usage
- Revisa que tengas instalado el [NVIDIA driver](https://github.com/NVIDIA/nvidia-docker/wiki/Frequently-Asked-Questions#how-do-i-install-the-nvidia-driver).
- Instalar el NVIDIA-Docker version 2.0 siguiendo las siguientes instrucciones [aqui](https://github.com/NVIDIA/nvidia-docker/wiki/Installation-(version-2.0)).
- Ejecuta el siguiente comando:
  - Linux: `IMG=boinc/client:multi-gpu ./quickstart.sh`
  - Windows: `quickstart.bat --docker --image boinc/client:multi-gpu`
 
#### NVIDIA-savvy BOINC client usage
- Revisa que tengas instalado el [NVIDIA driver](https://github.com/NVIDIA/nvidia-docker/wiki/Frequently-Asked-Questions#how-do-i-install-the-nvidia-driver).
- Instalar el NVIDIA-Docker version 2.0 siguiendo las siguientes instrucciones [aqui](https://github.com/NVIDIA/nvidia-docker/wiki/Installation-(version-2.0)).
- Ejecuta el siguiente comando:
  - Linux: `IMG=boinc/client:nvidia ./quickstart.sh`
  - Windows: `quickstart.bat --docker --image boinc/client:nvidia`

#### VirtualBox-savvy BOINC client usage

- Instalar el paquete `virtualbox-dkms` en el host.
- Ejecuta el siguiente comando:
  - Linux: `IMG=boinc/client:virtualbox ./quickstart.sh`
  - Windows: `quickstart.bat --docker --image boinc/client:virtualbox`

#### ARMv7 32-bit savvy BOINC client usage
- Asegurate que tengas [Docker instalado en tu Raspberry Pi](https://www.raspberrypi.org/blog/docker-comes-to-raspberry-pi/) or si estas usando [Un sistema operativo amigable con Docker](https://blog.hypriot.com/).
- Ejecuta el siguiente comando:.
  - Linux: `IMG=boinc/client:arm32v7 ./quickstart.sh`
  - Windows: `quickstart.bat --docker --image boinc/client:arm32v7`

#### ARMv8 64-bit savvy BOINC client usage
- Asegurate que tengas [64-bit OS en tu Raspberry Pi](https://wiki.ubuntu.com/ARM/RaspberryPi#arm64) y tengas [Docker instalaod en tu Raspberry Pi](https://www.raspberrypi.org/blog/docker-comes-to-raspberry-pi/).
- Ejecuta el siguiente comando:.
  - Linux: `IMG=boinc/client:arm64v8 ./quickstart.sh`
  - Windows: `quickstart.bat --docker --image boinc/client:arm64v8`

---

<<<<<<< HEAD
## Modo Docker Swarm
=======
## Docker Swarm Mode
>>>>>>> upstream/master

Puedes utilizar Docker Swarm para lanzar una gran cantidad de clientes, por ejemplo atravez de un cluster que estes usando para computacion BOINC. Primero comienza el swarm para crear una red,

```sh
docker swarm init
docker network create -d overlay --attachable boinc
```

Si quieres, puedes conectar otros nodos a tu swarm ejecutando el comando apropiado `docker swarm join` on nodos trabajadores como se indico anteriormente.

Despues lanza tus clientes:

```sh
docker service create \
  --replicas <N> \
  --name boinc \
  --network=boinc \
  -p 31416 \
  -e BOINC_GUI_RPC_PASSWORD="123" \
  -e BOINC_CMD_LINE_OPTIONS="--allow_remote_gui_rpc --attach_project http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec" \
  boinc/client
```

Ahora tienes `<N>` clientes funcionando, distribuidos atravez de tu swarm. Puedes emitir comandos a todos tus clientes usando:

```sh
docker run --rm --network boinc boinc/client boinccmd_swarm --passwd 123 <args>
```

Nota: no tienes que especificar `--host`. El commando `boinccmd_swarm` se hace cargo de mandar un comando para cada host en tu swarm.

Docker Swarm no es compatible con el modo `pid=host`. Como resultado, las configuraciones del cliente relacionados con el no uso de la CPU de BOINC o exclusion de apps no tomara effecto.

---

## Ver y administrar cargas de trabajo

Tienes varias opciones aqui:

- Mejor Opcion: [BOINCTASKS](https://efmer.com/download-boinctasks/)
- Ver tareas desde el manejador nativo de BOINC

*Para BSD hay tambien `boinc_curses` TUI application, el cual permite ver las tareas locales y varias distribuciones de Linux. Tambien hay un paquete `boinctui`*

**Para las tareas basicas te puedes referir a [Comandos para BOINC](#comandos-para-boinc-y-atajos)**

### Manager nativo  de BOINC ([Official Installation Instructions](https://boinc.berkeley.edu/wiki/Installing_BOINC))

Si estas usando BOINC via Docker, es un poco redundante descargar nativamente BOINC, pero lo puedes hacer si quieres ver y manejar las tareas usando la interfaz GUI.

- lanza BOINC
- Si el "Select a Project" sale, solo cancelalo si estas conectando a un cliente remoto o un Contenedor de Docker.
- `Archivo > Seleccionar Computador`
  - Entra la direccion IP y el nombre del host de tu computador con la clave de `gui_rpc_auth.cfg` y haz click en "OK"

Si estas usando BOINC via Docker en tu maquina local, la direccion IP es `127.0.0.1`. De otro modo, ingresa el IP de **HOST** que Docker esta usando (No la direccion IP del contenedor del `docker0` interface). Especificando `-p 31416` en el comando `docker run`, nosotros mapeamos el puerto de comunicacion usado por el cliente BOINC en el contenedor de Docker en la maquina host.

`Boingmgr` deberia de no tener ningun problema contectandose a cualquier contenedor Docker en la red a no ser que este prohibida por las reglas del firewall en el sistema operativo como CentOS o Fedora.

---

## Comandos para BOINC y atajos

Referencias para `boinccmd`:
- [https://boinc.berkeley.edu/wiki/Boinccmd_tool](https://boinc.berkeley.edu/wiki/Boinccmd_tool)
- [https://www.systutorials.com/docs/linux/man/1-boinccmd/](https://www.systutorials.com/docs/linux/man/1-boinccmd/)

#### Acceder al shell desde el contenedor de Docker:

`docker exec -it boinc /bin/sh`

Esto te permitira estar en tu maquina y ejecutar comandos directos de `boinccmd`

#### Adjuntar a el proyecto de Rosseta@home de NUCC (Esto lo hace automaticamente el script quickstart):

**Windows:**

`boinccmd --project_attach http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec`

**Linux/MacOS/BSD:**

`boinccmd --attach_project http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec`

**Docker:**

`docker exec [container-name] boinccmd --attach_project http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec`

### Por simplicidad, los comandos abajo son comandos locales, esto significa 1 de 3 cosas:

- Debes ejecutarlos como estan si estas usando el cliente de BOINC en el host
- Debes ejecutarlos como estan si ya lo ejecutaste desde el contenedor de Docker.
- Debes poner al inicio `docker exec [container-name]` si estas usando en un contenedor Docker con el cliente BOINC ya instalado
  - Si BOINC fue instalado via Docker y uno de los scripts quickstart, el nombre del contenedor es `boinc`
  - Ejemplo: `docker exec -it boinc boinccmd --get_state`

#### Pedir no mas trabajo despues que tu tarea actual de Rosetta@home termine

`boinccmd --project http://boinc.bakerlab.org/rosetta/ nomorework`

Este es una parada "suave" y podria demorar unas 24hrs para que las cargas de trabajo terminen de procesar. 

Despues, puedes sustituir  `nomorework` con `allowmorework` para comenzar a pedir mas tareas otra vez.

#### Suspender todas las tareas para el proyecto de Rosetta@home:

`boinccmd --project http://boinc.bakerlab.org/rosetta/ suspend`

#### Renaudar todas las tareas de Rosetta@home:

`boinccmd --project http://boinc.bakerlab.org/rosetta/ resume`

#### Parar o comenzar el contenedor de BOINC Docker:

`docker stop boinc` y `docker start boinc`

Este no es recomendado, ya que tus tareas actuales seran abandonadas

**Mejores Practicas serian las siguientes**

```sh
docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ suspend
docker stop boinc
docker start boinc
docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ resume
```

---

<<<<<<< HEAD
## Actualizaciones:

- Documentacion para monitorear remotamente y manejar cargas de trabajo proximamente.
=======
## Viewing and Managing Workloads

You have a couple of good options here:

- Best Option: [BOINCTASKS](https://efmer.com/download-boinctasks/)
- View tasks from the native BOINC Manager

*For BSD, there is also the `boinc_curses` TUI application, which allows you to view local tasks, and for various Linux distros, there is the `boinctui` package, which I have personally never tried,
but imagine it is probably similar to `boinc_curses` for BSD.*

**For basic tasks, you can refer to [Boinc Commands and Shortcuts](#boinc-commands-and-shortcuts).**

### BOINCTASKS ([Download Here](https://efmer.com/download-boinctasks/))

This is honestly the best option, especially if you are running BOINC from multiple machines on the same network.  The thing I like most about it is that it doesn't require a native BOINC installation
if all you need is the **BOINC Manager**, like if you are running the *BOINC Client* via Docker or from a different machine on the network.  One of the best features is its ability to scan your network
for BOINC clients and automatically add them to the management interface.  BOINCTASKS is the only option if you want to manage multiple clients from a GUI interface without having to disconnect between
viewing each individual client.  It's a Windows program, but is FULLY-COMPATIBLE with *nix hosts via [Wine](https://www.winehq.org/).  It literally took me less than a minute to get it fully-installed
on my Ubuntu laptop, after which I was able to see all the clients on my local network running BOINC, and remotely manage their tasks.

### Native BOINC Manager ([Official Installation Instructions](https://boinc.berkeley.edu/wiki/Installing_BOINC))

If you are running BOINC via Docker, it's a little redundant to download BOINC natively, but you can do so if you want to view and manage the tasks running from a GUI interface.

- Launch BOINC
- If the "Select a Project" pops up, just cancel out of it if you're connecting to a remote BOINC client or Docker container.
- `File > Select Computer`
  - Enter the computer's IP/hostname and password from `gui_rpc_auth.cfg`, and Click "OK".

If you are running BOINC via Docker on your local machine, the IP address will be `127.0.0.1`.  Otherwise, enter the IP of the **HOST** that Docker is running on (not the IP of the container
from the `docker0` interface).  By specifying `-p 31416` in the `docker run` command, we mapped the communication port used by the BOINC client in the Docker container to the host machine.

`Boingmgr` should have no trouble connecting to any Docker container on the network unless prohibited by firewall rules on operating systems such as CentOS or Fedora,
in which case, you should consult the [#firewall-caveats](Firewall Caveats) mini-section for more information.

---

## BOINC Commands and Shortcuts

Two very good `boinccmd` references:

- [https://boinc.berkeley.edu/wiki/Boinccmd_tool](https://boinc.berkeley.edu/wiki/Boinccmd_tool)
- [https://www.systutorials.com/docs/linux/man/1-boinccmd/](https://www.systutorials.com/docs/linux/man/1-boinccmd/)

#### Acces the shell on the Docker container:

`docker exec -it boinc /bin/sh`

This will allow you to be on the machine and run `boinccmd` commands directly.

#### Execute a specific `boinccmd` command inside local docker container directly from the host:

`docker exec boinc boinccmd --command-arguments-here`

#### Attach to NUCC's Rosetta@home Project (this is done automatically in the quickstart scripts):

**Native Installation:**

`boinccmd --project_attach http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec`

**Docker Installation:**

`docker exec [container-name] boinccmd --attach_project http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec`

### For simplicity, the commands below will be listed as local commands. This means 1 of 3 things:

- You should execute them as-is if running the BOINC client on the host
- You should execute them as-is if you have already exec'd into the Docker container
- You should prepend them with `docker exec [container-name] ` if running them against the Docker container with the BOINC client installed.
  - If BOINC was installed via Docker and one of the quickstart scripts, the container name is `boinc`.
  - Example: `docker exec -it boinc boinccmd --get_state`

#### Request no more work after current Rosetta@home tasks finish:

`boinccmd --project http://boinc.bakerlab.org/rosetta/ nomorework`

This is a "graceful stop" and could take up to 24 hours for workloads to completely stop processing:

Later, you can substitue `nomorework` with `allowmorework` to start pulling tasks again

#### Suspend all tasks for the Rosetta@home project:

`boinccmd --project http://boinc.bakerlab.org/rosetta/ suspend`

#### Resume all tasks for the Rosetta@home project:

`boinccmd --project http://boinc.bakerlab.org/rosetta/ resume`

#### Stop or Start the BOINC Docker container:

`docker stop boinc` and `docker start boinc`

This is not recommended, as your current tasks will be abandoned.

**Best practices would be as follows:**

```sh
docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ suspend
docker stop boinc
docker start boinc
docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ resume
```

### Docker Shortcut Function (`nuccd`):

This will probably become part of the install script in the future, but as of now, this can make things much easier for Docker-based installations.

Just add this function to a dotfile like `~/.bash_functions` and source it in your `~/.bashrc` or `~/.bash_profile`:

```sh
nuccd() {
  if [[ $1 = "allowmorework" ]]; then
    docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ allowmorework
  elif [[ $1 = "nomorework" ]]; then
    docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ nomorework
  elif [[ $1 = "suspend" ]]; then
    docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ suspend
  elif [[ $1 = "resume" ]]; then
    docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ resume
  elif [[ $1 = "stop" ]]; then
    docker stop boinc
  elif [[ $1 = "start" ]]; then
    docker start boinc
  elif [[ $1 = "remove" ]]; then
    docker stop boinc 2>/dev/null
    docker rm boinc
  elif [[ $1 = "uninstall" ]]; then
    docker stop boinc 2>/dev/null
    docker rm boinc 2>/dev/null
    docker images | grep boinc | awk '{print $3}' | xargs docker rmi 2>/dev/null
  else
    echo '
USAGE: nuccd [OPTIONS]

allowmorework
nomorwork
suspend
resume
start
stop
remove
uninstall
'
  fi
}
```

Alternately, you can use it as a script and save it somewhere in your `$PATH` like `/usr/local/bin`:

- `sudo vi /usr/local/bin/nuccd`
- Add the following:

```sh
#!/bin/bash

if [[ $1 = "allowmorework" ]]; then
  docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ allowmorework
elif [[ $1 = "nomorework" ]]; then
  docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ nomorework
elif [[ $1 = "suspend" ]]; then
  docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ suspend
elif [[ $1 = "resume" ]]; then
  docker exec boinc boinccmd --project http://boinc.bakerlab.org/rosetta/ resume
elif [[ $1 = "stop" ]]; then
  docker stop boinc
elif [[ $1 = "start" ]]; then
  docker start boinc
elif [[ $1 = "remove" ]]; then
  docker stop boinc 2>/dev/null
  docker rm boinc
elif [[ $1 = "uninstall" ]]; then
  docker stop boinc 2>/dev/null
  docker rm boinc 2>/dev/null
  docker images | grep boinc | awk '{print $3}' | xargs docker rmi 2>/dev/null
else
  echo '
USAGE: nuccd [OPTIONS]

allowmorework
nomorwork
suspend
resume
start
stop
remove
uninstall
'
fi
```

- Save the file and figure out how to exit `vi`
- `sudo chmod +x /usr/local/bin/nuccd`

---

## Updates

- Added native installation support for MacOS in `quickstart.sh`
- Made some clarifications and edits to the [BSD Documentation](https://bookandcode.com/nuccbsd/)
- Made some clarifications on the Folding@home status and why NUCC is currently using Rosetta@home for COVID-19 research
- Working on adding `nuccd` support to quickstart scripts.
- Automated native installation for Linux coming soon.
>>>>>>> upstream/master

---

## Sobre el National Upcycled Computing Collective (NUCC)

[The National Upcycled Computing Collective, Inc.](http://nuccinc.org) es una Organizacion Sin Animo de Lucro (501(c)(3)) categorizada como un Instituto de Investigacion en las areas de Ciencias Computacionales, Tecnologia & Ingenieria(EIN 82-1177433), en California, USA, como lo determina el IRS (Internal Revenue Service). Nuestra mision es encontrar nuevos usos para la tecnologia, 
extendiendo así los ciclos de vida de estos con la intención de reutilizar los dispositivos electrónicos de manera responsable. Para mas informacion, visita [https://www.nuccinc.org/about/](https://www.nuccinc.org/about/).