---
layout: single
title: "Archivos de Configuracion Bspwm"
excerpt: "El proyecto de mi entorno de Bspwm es una configuración personalizada y optimizada para el gestor de ventanas bspwm en sistemas basados en Debian. Está diseñado específicamente para pentesting y proporciona un entorno de trabajo eficiente y altamente personalizable para realizar tareas relacionadas con la seguridad informática. Con una configuración de atajos de teclado optimizados, esta es mi configuración que brinda un flujo de trabajo rápido y productivo, ayudándote a organizar y controlar tus ventanas de manera eficiente mientras llevas a cabo actividades de pentesting en tu máquina con Linux."
date: 2023-07-16
classes: wide
header:
  teaser: /assets/images/Dotfiles-en-bspwm/teaser.png
  teaser_home_page: true
categories:
  - Dotfiles
  - Utilidades
tags:
  - Bpwm
  - Polybar
  - Bash
  - PowerLevel10k
  - Sxhkd
  - Dotfiles
---

[//]: # (![](/assets/images/Bandit-Decompressor/decompressor.png))

## Configuración personal de entorno de trabajo bspwm.

Este es mi entorno de trabajo personalizado con Bspwm para máquinas con sistema operativo GNU/Linux y distribuciones basadas en Debian. Está enfocado en el pentesting y tiene una configuración con atajos de teclado.

Para este entorno utilizo el gestor de ventanas bspwm, que se basa en el concepto de **"ventanas flotantes"**. Es altamente personalizable, lo que me permite organizar y controlar las ventanas de forma efectiva.

He configurado atajos de teclado optimizados para agilizar el flujo de trabajo, y se asignan comandos a combinaciones de teclas para realizar acciones rápidas y sencillas.
> Estas son las especificaciones de mi sistema operativo:
```bash
liann@nk:~$
└──╼ $uname -a
Linux parrot 6.1.0-1parrot1-amd64 #1 SMP PREEMPT_DYNAMIC Parrot 6.1.15-1parrot1 (2023-04-25) x86_64 GNU/Linux
liann@nk:~$
└──╼ $lsb_release -a
No LSB modules are available.
Distributor ID:	Parrot
Description:	Parrot OS 5.3 (Electro Ara)
Release:	5.3
Codename:	ara
liann@nk:~$
└──╼ $
```

## Atajos de Teclado
```
Abrir terminal
    super + enter

Preselectores
    ctrl + super + alt + {Izquierda, Arriba, Derecha, Abajo}

Preselectores numericos
    ctrl + super + {1, 2, 3, 4, 5}

Tilling Window
    super + s

Mover tilling window
    ctrl + super + {Izquierda, Arriba, Derecha, Abajo}
   
Cambiar tamano tilling window
    super + alt + {Izquierda, Arriba, Derecha, Abajo}

Encasillar tilling window
    super + t
```
## Atajos de la terminal Kitty
```
Nueva terminal kitty
    ctrl + shift + enter

Cerrar terminal kitty
    ctrl + shift + w

Multiventanas kitty
    ctrl + shift + t

Cambiar nombre de la terminal kitty
    ctrl + alt + shift + t
```
> La guia de instalacion sera la siguiente:

## Instalamos los siguientes paquetes
```bash
1. Instalamos los siguientes paquetes
liann@nk:~$
└──╼ $apt install build-essential git vim xcb libxcb-util0-dev libxcb-ewmh-dev libxcb-randr0-dev
    libxcb-icccm4-dev libxcb-keysyms1-dev libxcb-xinerama0-dev libasound2-dev libxcb-xtest0-dev
    libxcb-shape0-dev

2. Instalamos bspwm y sxhkd:
liann@nk:~$
└──╼ $cd /home/{usuario}/Descargas/
liann@nk:~$   
└──╼ $git clone https://github.com/baskerville/bspwm.git
liann@nk:~$   
└──╼ $git clone https://github.com/baskerville/sxhkd.git
liann@nk:~$   
└──╼ $cd bspwm/
liann@nk:~$   
└──╼ $make
liann@nk:~$   
└──╼ $sudo make install
liann@nk:~$   
└──╼ $cd ../sxhkd/
liann@nk:~$   
└──╼ $make
liann@nk:~$   
└──╼ $sudo make install
liann@nk:~$
└──╼ $sudo apt install bspwm

3. Cargamos en bspwm y sxhkd ficheros de ejemplo:
liann@nk:~$
└──╼ $mkdir ~/.config/bspwm
liann@nk:~$   
└──╼ $mkdir ~/.config/sxhkd
liann@nk:~$   
└──╼ $cd /home/{usuario}/Descargas/bspwm/
liann@nk:~$   
└──╼ $cp examples/bspwmrc ~/.config/bspwm/
liann@nk:~$   
└──╼ $chmod +x ~/.config/bspwm/bspwmrc
liann@nk:~$   
└──╼ $cp examples/sxhkdrc ~/.config/sxhkd/
```

Abrimos el sxhkdrc y configuramos el tipo de terminal así como algunos shortcuts
## Archivo Sxhkdrc
```
terminal emulator
    super + Return
        kitty

program launcher
    super + d
        rofi -show run

make sxhkd reload its configuration files:
    super + Escape
        pkill -USR1 -x sxhkd

quit/restart bspwm
    super + alt + {q,r}
        bspc {quit,wm -r}

close and kill
    super + {_,shift + }w
        bspc node -{c,k}

alternate between the tiled and monocle layout
    super + m
        bspc desktop -l next

send the newest marked node to the newest preselected node
    super + y
        bspc node newest.marked.local -n newest.!automatic.local

swap the current node and the biggest node
    super + g
        bspc node -s biggest
   
set the window state
    super + {t,shift + t,s,f}
        bspc node -t {tiled,pseudo_tiled,floating,fullscreen}

set the node flags
    super + ctrl + {m,x,y,z}
        bspc node -g {marked,locked,sticky,private}

focus/swap
    super + {_,shift + }{Left,Down,Up,Right}
        bspc node -{f,s} {west,south,north,east}

focus the node for the given path jump
    super + {p,b,comma,period}
        bspc node -f @{parent,brother,first,second}

focus the next/previous node in the current desktop
    super + {_,shift + }c
        bspc node -f {next,prev}.local

focus the next/previous desktop in the current monitor
    super + bracket{left,right}
        bspc desktop -f {prev,next}.local

focus the last node/desktop
    super + {grave,Tab}
        bspc {node,desktop} -f last

focus the older or newer node in the focus history
    super + {o,i}
        bspc wm -h off; \
        bspc node {older,newer} -f; \
        bspc wm -h on

focus or send to the given desktop
    super + {_,shift + }{1-9,0}
        bspc {desktop -f,node -d} '^{1-9,10}'
   
preselect the direction
    super + ctrl + alt + {Left,Down,Up,Right}
        bspc node -p {west,south,north,east}

preselect the ratio
    super + ctrl + {1-9}
        bspc node -o 0.{1-9}

cancel the preselection for the focused node
    super + ctrl + space
        bspc node -p cancel

cancel the preselection for the focused desktop
    super + ctrl + alt + space
        bspc query -N -d | xargs -I id -n 1 bspc node id -p cancel
   
expand a window by moving one of its side outward
    super + alt + {h,j,k,l}
        bspc node -z {left -20 0,bottom 0 20,top 0 -20,right 20 0}

contract a window by moving one of its side inward
    super + alt + shift + {h,j,k,l}
        bspc node -z {right -20 0,top 0 20,bottom 0 -20,left 20 0}

move a floating window
    super + ctrl + {Left,Down,Up,Right}
        bspc node -v {-20 0,0 20,0 -20,20 0}

Custom move/resize
    alt + super + {Left,Down,Up,Right}
       /home/{usuario}/.config/bspwm/scripts/bspwm_resize {west,south,north,east}
```

## Creamos el archivo bspwm_resize
```bash
liann@nk:~$     
└──╼ $mkdir ~/.config/bspwm/scripts/
liann@nk:~$     
└──╼ $touch ~/.config/bspwm/scripts/bspwm_resize
liann@nk:~$     
└──╼ $chmod +x ~/.config/bspwm/scripts/bspwm_resize
```
> Mediante la siguiente configuración podremos en el futuro controlar las dimensiones y modificarlas con atajos de teclado:

## Archivo Bspwm_resize
```bash
#!/usr/bin/env dash

    if bspc query -N -n focused.floating > /dev/null; then
            step=20
    else
            step=100
    fi

    case "$1" in
            west) dir=right; falldir=left; x="-$step"; y=0;;
            east) dir=right; falldir=left; x="$step"; y=0;;
            north) dir=top; falldir=bottom; x=0; y="-$step";;
            south) dir=top; falldir=bottom; x=0; y="$step";;
    esac

    bspc node -z "$dir" "$x" "$y" || bspc node -z "$falldir" "$x" "$y"
```

## Instalamos los siguientes paquetes para Instalar Polybar.
> Pero antes, instalamos primero los siguientes paquetes:

```bash
liann@nk:~$
└──╼ $sudo apt install cmake cmake-data pkg-config python3-sphinx libcairo2-dev libxcb1-dev
     libxcb-util0-dev libxcb-randr0-dev libxcb-composite0-dev python3-xcbgen xcb-proto 
     libxcb-image0-dev libxcb-ewmh-dev libxcb-icccm4-dev libxcb-xkb-dev libxcb-xrm-dev
     libxcb-cursor-dev libasound2-dev libpulse-dev libjsoncpp-dev libmpdclient-dev
     libcurl4-openssl-dev libnl-genl-3-dev
liann@nk:~$
└──╼ $sudo apt install libuv1-dev
```
> Para instalar la Polybar:

```bash
liann@nk:~$  
└──╼ $cd /home/{usuario}/Descargas/
liann@nk:~$
└──╼ $git clone --recursive https://github.com/polybar/polybar
liann@nk:~$
└──╼ $cd polybar/
liann@nk:~$
└──╼ $mkdir build
liann@nk:~$
└──╼ $cd build/
liann@nk:~$
└──╼ $cmake ..
liann@nk:~$
└──╼ $make -j $(nproc)
liann@nk:~$
└──╼ $sudo make install
```
## Instalamos Picom para ajustar las transparencias.
> Primeramente, instalamos los siguientes paquetes, no sin antes actualizar el sistema:

```bash
liann@nk:~$ 
└──╼ $sudo apt update
liann@nk:~$ 
└──╼ $sudo apt install meson libxext-dev libxcb1-dev libxcb-damage0-dev libxcb-xfixes0-dev libxcb-shape0-dev
liann@nk:~$ 
└──╼ $sudo apt install libxcb-render-util0-dev libxcb-render0-dev libxcb-randr0-dev libxcb-composite0-dev libxcb-image0-dev
liann@nk:~$ 
└──╼ $sudo apt install libxcb-present-dev libxcb-xinerama0-dev libpixman-1-dev libdbus-1-dev libconfig-dev libgl1-mesa-dev
liann@nk:~$ 
└──╼ $sudo apt install libpcre2-dev libevdev-dev uthash-dev libev-dev libx11-xcb-dev libxcb-glx0-dev
```
Posteriormente, ejecutamos los siguientes comandos bajo el directorio `~/Descargas`:

> EN KALI, EJECUTAR UNO A UNO LOS -DEV O LA INSTALACION DE PICOM CON MESON NO FUNCIONARA, DARA ERROR
  INFORMANDO QUE FALTAN DEPENDENCIAS.
  SI NO, SERA DEPRECATED Y NO SERVIRA

```bash
liann@nk:~$ 
└──╼ $git clone https://github.com/ibhagwan/picom.git
liann@nk:~$ -     
└──╼ $cd picom/
liann@nk:~$      
└──╼ $git submodule update --init --recursive
     meson --buildtype=release . build -(DEPRECATED DO NOT USE)
liann@nk:~$ 
└──╼ $meson setup --buildtype=release . build
liann@nk:~$ 
└──╼ $ninja -C build
liann@nk:~$ 
└──╼ $sudo ninja -C build install
```
## Instalamos rofi (Posteriormente instalaremos el tema Nord para Rofi).
```bash
liann@nk:~$ 
└──╼ $sudo apt install rofi
```
En este punto, reiniciamos el equipo y seleccionamos **bspwm** `(Probamos que los shortcuts estén funcionando correctamente)`.

> Configuramos un poco la terminal e instalamos las `Hack Nerd Fonts`, además del Firefox (hay que descargarse la última versión,
también instalaremos `Firejail` con `apt install firejail` con el objetivo de lanzar firefox bajo este contexto enjaulado con **sxhkd**). 
[Las fuentes de **Hack Nerd Fonts** deben ir descomprimidas en `/usr/local/share/fonts/`, una vez hecho hay que ejecutar el comando `'fc-cache -v'`]

Instalamos el addon `'FoxyProxy'` para Firefox.

Configuramos la privacidad en Firefox y el directorio de descargas principal

Instalamos `'feh'` con `'apt install feh'` para poder agregar fondos de pantalla.

> Se agrega en el archivo bspwmrc justo al final la siguiente línea:

```bash
liann@nk:~$ 
└──╼ $feh --bg-fill /home/{usuario}/Desktop/Images/fondo.jpg
```
## Para configurar nuestra Polybar, clonaremos primeramente en 'Descargas' el siguiente repositorio.
```bash
liann@nk:~$
└──╼ $git clone https://github.com/VaughnValle/blue-sky.git
```
Posteriormente, ejecutaremos los siguientes comandos:
```bash
liann@nk:~$
└──╼ $mkdir ~/.config/polybar
liann@nk:~$
└──╼ $cd ~/Descargas/blue-sky/polybar/
liann@nk:~$
└──╼ $cp * -r ~/.config/polybar
liann@nk:~$
└──╼ $echo '~/.config/polybar/./launch.sh' >> ~/.config/bspwm/bspwmrc
liann@nk:~$
└──╼ $cd fonts
liann@nk:~$
└──╼ $sudo cp * /usr/share/fonts/truetype/
liann@nk:~$
└──╼ $fc-cache -v
```
> Hacemos `Windows + Shift + R` para cargar la configuración y deberíamos ver la **Polybar** por arriba.

## Para configurar Picom y ajustar las transparencias además de bordeados de ventana, ejecutamos los siguientes pasos.
```bash
liann@nk:~$
└──╼ $mkdir ~/.config/picom
liann@nk:~$
└──╼ $cd ~/.config/picom
liann@nk:~$
└──╼ $cp ~/Descargas/blue-sky/picom.conf .
```
> Editamos el archivo `picom.conf` y cambiamos `'backend = "glx"' por 'backend = "xrender"'`, comentando el de **glx**. 
Posteriormente, comentamos todas las líneas referentes a **glx** (En algunos ordenadores al dejar el **glx** puesto se puede llegar
a experimentar una lentitud muy molesta).

Antes de recargar la configuración, hacemos un seguimiento del ratón para saber en qué ventana estamos con la siguiente instrucción en el `'bspwm'``:
```bash
   bspc config focus_follows_pointer true
```
Posteriormente, ejecutamos los siguientes comandos para aplicar los bordeados:
```bash
liann@nk:~$
└──╼ $echo 'picom --experimental-backends &' >> ~/.config/bspwm/bspwmrc
liann@nk:~$
└──╼ $echo 'bspc config border_width 0' >> ~/.config/bspwm/bspwmrc
```
## Configuramos los colores de la polybar (paleta central), además de las paletas deseadas.
```
    Estructura de un nuevo módulo:

    Previamente tenemos que crear una carpeta en "~/.config/bin"

    [module/tumodulo]
        type = custom/script
        interval = 2
        exec = ~/.config/bin/binario.sh

   #Los modulos utilizados en estos dotfiles estan en la capeta bin de este repositorio
```
## Configuramos el tema Nord de Rofi:
```bash
liann@nk:~$
└──╼ $mkdir -p ~/.config/rofi/themes
liann@nk:~$
└──╼ $cp ~/Descargas/blue-sky/nord.rasi ~/.config/rofi/themes
```
> Posteriormente con 'rofi-theme-selector' seleccionamos el tema Nord.

## Instalamos slim y slimlock
```bash
1. Instalamos los siguientes paquetes, no sin antes hacer una actualización:
liann@nk:~$
└──╼ $sudo apt update
└──╼ $sudo apt install slim libpam0g-dev libxrandr-dev libfreetype6-dev libimlib2-dev libxft-dev

2. Posteriormente, ejecutamos los siguientes comandos:
liann@nk:~$
└──╼ $cd ~/Descargas/
liann@nk:~$
└──╼ $git clone https://github.com/joelburget/slimlock.git
liann@nk:~$
└──╼ $cd slimlock/
liann@nk:~$
└──╼ $sudo make
liann@nk:~$
└──╼ $sudo make install
liann@nk:~$
└──╼ $cd ~/Descargas/blue-sky/slim
liann@nk:~$
└──╼ $sudo cp slim.conf /etc/
liann@nk:~$
└──╼ $sudo cp slimlock.conf /etc
liann@nk:~$
└──╼ $sudo cp -r default /usr/share/slim/themes
```
> Si queremos cambiar la imagen del panel, nos vamos a la ruta `'/usr/share/slim/themes/default'` y retocamos el archivo `'panel.png'`.

Reiniciamos el sistema y una vez arrancado, incorporamos en el archivo `'bspwmrc'` la siguiente línea para arreglar el cursor:
```
    xsetroot -cursor_name left_ptr &
```
## Instalamos la powerlevel10k en zsh

Creamos enlace simbólico de la zshrc para root

## Cambiamos el tipo de shell por defecto tanto para root como para el usuario con bajos privilegios
```
    usermod --shell /usr/bin/zsh tuUsuario
    usermod --shell /usr/bin/zsh root
```
## Retocamos el archivo .p10k.zsh para adecuarlo a nuestro gusto

> Para el de root, podemos ir a `'POWERLEVEL9K_CONTEXT_ROOT_TEMPLATE'` para asignar el **Hashtag**.

   Comentamos la siguiente línea:
```
    POWERLEVEL9K_CONTEXT_PREFIX='%246Fwith '
```
   Para evitar un pequeño problema de permisos a la hora de desde el usuario root migrar con 'su' al usuario con bajos privilegios,
   ejecutamos los siguientes comandos:
```bash
    chown {usuario}:{usuario} /root
    chown {usuario}:{usuario} /root/.cache -R
    chown {usuario}:{usuario} /root/.local -R
```
Instalamos bat, lsd, fzf y ranger

## Instalar el plugin sudo

   Incorporamos posteriormente las siguientes líneas al final del zshrc para que
   al salir de vim el cursor recupere su aspecto de linea.

```bash
   Change cursor shape for different vi modes.
          function zle-keymap-select {
          if [[ $KEYMAP == vicmd ]] || [[ $1 = 'block' ]]; then
             echo -ne '\e[1 q'
          elif [[ $KEYMAP == main ]] || [[ $KEYMAP == viins ]] || [[ $KEYMAP = '' ]] || [[ $>
             echo -ne '\e[5 q'
          fi
         }
         zle -N zle-keymap-select

   #Start with beam shape cursor on zsh startup and after every command.
   -      zle-line-init() { zle-keymap-select 'beam'}
```
## Whichsystem.py, es un pequeno script que se ha hecho S4avitar en la maquina Blue de HackTheBox, todos los creditos de la creacion y por su tutorial para montar el     entorno de linux.

   -     https://github.com/Akronox/WichSystem.py

## fastTCPScan.go, es la herramienta creada por S4avitar, todos los creditos de esta herramienta para el.
> Con fastTCPScan podremos hacer descubrimiento de puertos TCP.

Todos los créditos a sus respectivos desarrolladores.
 
Lian