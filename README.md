![Platform: ALL](https://img.shields.io/badge/platform-ALL-green)
![Follow @NUCC Inc. on Twitter](https://img.shields.io/twitter/follow/nucc_inc?label=follow&style=social)
![Tweet about this Project](https://img.shields.io/twitter/url?style=social&url=https%3A%2F%2Fgithub.com%2Fphx%2Fnucc)

![NUCC logo](./logo.png?raw=true)

# NUCC Computación Distribuida para la Ayuda en la Investigación del COVID-19

> Repositorio original creado por [Phoenix](https://github.com/phx/nucc)
> Traduccion por [theJuan](https://github.com/theJuan1112)
- [English Version](https://github.com/theJuan1112/nucc/blob/master/README.en.md)

**Ultima Actualización: Marzo 23, 2020**

Únete al [National Upcycled Computing Collective (NUCC)](https://www.nuccinc.org/) en un esfuerzo colaborativo para combinar nuestros recursos computacionales para ayudar en la investigación del COVID-19.
Este proyecto se basa en [la configuracion predeterminada de Docker creado por BOINC](https://github.com/BOINC/boinc-client-docker). La diferencia es que no hay que registrar ninguna cuenta y no comparte información personal. Solamente es utilizada para conectarse automáticamente al proyecto en curso de NUCC en [Rosseta@home](https://boinc.bakerlab.org/), que es un equipo de investigación el cual esta activamente procesando cargas especificas de el COVID-19.

---

## La forma mas rapida y facil de contribuir si ya tienes Docker instalado es la siguiente:

Copiar y pegar la siguiente linea en tu terminal para comenzar inmediatamente en MacOS o Linux:

`docker run -d --restart always --name boinc -p 31416 -v "${HOME}/.boinc:/var/lib/boinc" -e BOINC_GUI_RPC_PASSWORD="123" -e BOINC_CMD_LINE_OPTIONS="--allow_remote_gui_rpc --attach_project http://boinc.bakerlab.org/rosetta/ 2108683_fdd846588bee255b50901b8b678d52ec" boinc/client:baseimage-alpine`

---

## Contenido

- [Instalación Nativa de Windows](#instalaci%c3%b3n-nativa-de-windows)
- [Instalacion de Docker en Windows](#instalacion-de-docker-en-windows)
- [Instalacion en BSD Jail](#instalacion-bsd-jail)
- [Instalacion de Docker en MacOS/Linux](#instalacion-de-docker-en-linux-y-macos)
- [Arquitectura y Etiquetas Compatibles](#arquitecturas-y-etiquetas-compatibles)
- [Modo Docker Swarm](#modo-docker-swarm)
- [Actualizaciones](#actualizaciones)
- [Sobre NUCC](#sobre-el-national-upcycled-computing-collective-nucc)

---

## Instalación Nativa de Windows:

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

## Instalacion de Docker en Windows:

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

## Instalacion BSD Jail

Documentación en progreso. Funciona 100% correctamente y la documentacion va a incluir instrucciones para Free-NAS.

---

## Instalacion de Docker en Linux y MacOS

### Si NO tienes Docker Instalado:

- Debian
- Raspbian
- Ubuntu
- Kali 2018+ (basado en Debian Stretch)
- Arch
- MacOS

```
git clone http://github.com/theJuan1112/nucc.git
cd nucc
./quickstart.sh
```

*Si el script crea un error despues de instalar Docker, ejecuta otra vez otro Shell que reconozca tu usuario como miembro del grupo `docker`*

#### Plataformas basadas en RPM, por favor ver en la [Documentacion Oficial de Docker](https://docs.docker.com/install/) para instalaciones de Docker en tu sistema Operativo particular:

Estoy trabajando en estos momentos en construir estos distros en una[Instalacion Casi Universal de Docker](https://github.com/phx/dockerinstall) que es usada por [`quickstart.sh`](quickstart.sh).

- [CentOS](https://docs.docker.com/install/linux/docker-ce/centos/)
- [Fedora](https://docs.docker.com/install/linux/docker-ce/fedora/)

### Si ya tienes Docker instalado:

```
git clone http://github.com/theJuan1112/nucc.git
cd nucc
./quickstart.sh
```

---

## Arquitecturas y Etiquetas compatibles

Puedes especializar la imagen de `boinc/client` con cualquiera de las siguientes etiquetas para usar una version de contenedor especializada.

Este se puede usar en el comando de Linux/MacOS al comienzo de este documento y pasarlo como la variable de entorno `$IMG` para `quickstart.sh`

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

## Modo Docker Swarm

Puedes utilizar Docker Swarm to lanzar una gran cantidad de clientes, por ejemplo atravez de un cluster que estes usando para computacion BOINC. Primero comienza el swarm para crear una red,

```sh
docker swarm init
docker network create -d overlay --attachable boinc
```

Si quieres, puedes conectar otros nodos a tu swarm ejecutando el comando apropiado `docker swarm join` on nodos trabajadores como se indico anteriormente.

Despues lanza tu clientes:

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

## Actualizaciones:

- Documentacion para BSD/FreeNAS proximamente.
- Documentacion para monitorear remotamente y manejar cargas de trabajo proximamente.

---

## Sobre el National Upcycled Computing Collective (NUCC)

[The National Upcycled Computing Collective, Inc.](http://nuccinc.org) es una Organizacion Sin Animo de Lucro (501(c)(3)) categorizada como un Instituto de Investagacion en las areas de Ciencias Computacionales, Tecnologia & Ingenieria(EIN 82-1177433), en California, USA, como lo determina el IRS (Internal Revenue Service). Nuestra mision es encontrar nuevos usos para la tecnologia, 
extendiendo así los ciclos de vida de estos con la intención de reutilizar los dispositivos electrónicos de manera responsable. Para mas informacion, visita [https://www.nuccinc.org/about/](https://www.nuccinc.org/about/).