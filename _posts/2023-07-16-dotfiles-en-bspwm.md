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
```
liann@nk:~$
└──╼ $uname -a
Linux parrot 5.2.0-2parrot1-amd64 #1 SMP Debian 5.2.9-2parrot1 (2019-08-25) x86_64 GNU/Linux
liann@nk:~$
└──╼ $lsb_release -a
No LSB modules are available.
Distributor ID:	Parrot
Description:	Parrot GNU/Linux 4.7
Release:	4.7
Codename:	n/a
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

La guia de instalacion sera la siguiente:

## 1. Instalamos los siguientes paquetes:
```
liann@nk:~$
└──╼apt install build-essential git vim xcb libxcb-util0-dev libxcb-ewmh-dev libxcb-randr0-dev libxcb-icccm4-dev libxcb-keysyms1-dev libxcb-xinerama0-dev libasound2-dev libxcb-xtest0-dev libxcb-shape0-dev

2. Instalamos bspwm y sxhkd:

   -     cd /home/{usuario}/Descargas/
   
   -     git clone https://github.com/baskerville/bspwm.git
   
   -     git clone https://github.com/baskerville/sxhkd.git
   
   -     cd bspwm/
   
   -     make
   
   -     sudo make install
   
   -     cd ../sxhkd/
   
   -     make
   
   -     sudo make install

   -     sudo apt install bspwm

3. Cargamos en bspwm y sxhkd ficheros de ejemplo:

   -     mkdir ~/.config/bspwm
   
   -     mkdir ~/.config/sxhkd
   
   -     cd /home/{usuario}/Descargas/bspwm/
   
   -     cp examples/bspwmrc ~/.config/bspwm/
   
   -     chmod +x ~/.config/bspwm/bspwmrc
   
   -     cp examples/sxhkdrc ~/.config/sxhkd/

4. Abrimos el sxhkdrc y configuramos el tipo de terminal así como algunos shortcuts

## Archivo Sxhkd
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

5. Creamos el archivo bspwm_resize:

   -     mkdir ~/.config/bspwm/scripts/
   -     touch ~/.config/bspwm/scripts/bspwm_resize
   -     chmod +x ~/.config/bspwm/scripts/bspwm_resize

> Mediante la siguiente configuración podremos en el futuro controlar las dimensiones y modificarlas con atajos de teclado:
## Archivo Bspwm_resize
```
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

6. Instalamos Polybar. Pero antes, instalamos primero los siguientes paquetes

   -     sudo apt install cmake cmake-data pkg-config python3-sphinx libcairo2-dev libxcb1-dev libxcb-util0-dev libxcb-randr0-dev libxcb-composite0-dev python3-xcbgen xcb-proto libxcb-image0-dev libxcb-ewmh-dev libxcb-icccm4-dev libxcb-xkb-dev libxcb-xrm-dev libxcb-cursor-dev libasound2-dev libpulse-dev libjsoncpp-dev libmpdclient-dev libcurl4-openssl-dev libnl-genl-3-dev
6.1. Instalar libuv1-dev
   -     sudo apt install libuv1-dev
   Para instalar la Polybar:
   
   -     cd /home/{usuario}/Descargas/
   -     git clone --recursive https://github.com/polybar/polybar
   -     cd polybar/
   -     mkdir build
   -     cd build/
   -     cmake ..
   -     make -j $(nproc)
   -     sudo make install

7. Instalamos Picom para ajustar las transparencias.

   Primeramente, instalamos los siguientes paquetes, no sin antes actualizar el sistema:

   -     sudo apt update
         sudo apt install meson libxext-dev libxcb1-dev libxcb-damage0-dev libxcb-xfixes0-dev libxcb-shape0-dev
         libxcb-render-util0-dev libxcb-render0-dev libxcb-randr0-dev libxcb-composite0-dev libxcb-image0-dev
         libxcb-present-dev libxcb-xinerama0-dev libpixman-1-dev libdbus-1-dev libconfig-dev libgl1-mesa-dev
         libpcre2-dev libevdev-dev uthash-dev libev-dev libx11-xcb-dev libxcb-glx0-dev

   Posteriormente, ejecutamos los siguientes comandos bajo el directorio ~/Descargas:

7.1 EN KALI, EJECUTAR UNO A UNO LOS -DEV O LA INSTALACION DE PICOM CON MESON NO FUNCIONARA, DARA ERROR
    INFORMANDO QUE FALTAN DEPENDENCIAS.
    SI NO, SERA DEPRECATED Y NO SERVIRA

   -     git clone https://github.com/ibhagwan/picom.git
   -     cd picom/
   -     git submodule update --init --recursive
   -     meson --buildtype=release . build(DEPRECATED DO NOT USE)
   -     meson setup --buildtype=release . build
   -     ninja -C build
   -     sudo ninja -C build install

8. Instalamos rofi (Posteriormente instalaremos el tema Nord para Rofi):

   -     sudo apt install rofi

9. En este punto, reiniciamos el equipo y seleccionamos bspwm (Probamos que los shortcuts estén funcionando correctamente).

10. Configuramos un poco la terminal e instalamos las Hack Nerd Fonts, además del Firefox (hay que descargarse la última versión,
    también instalaremos firejail con 'apt install firejail con el objetivo de lanzar firefox bajo este contexto enjaulado con sxhkd). 
    [Las fuentes de Hack Nerd Fonts deben ir descomprimidas en /usr/local/share/fonts/, una vez hecho hay que ejecutar el comando 'fc-cache -v']

11. Instalamos el addon 'FoxyProxy' para Firefox.

12. Configuramos la privacidad en Firefox y el directorio de descargas principal

13. Instalamos 'feh' con 'apt install feh' para poder agregar fondos de pantalla.

14. Se agrega en el archivo bspwmrc justo al final la siguiente línea:

   -     feh --bg-fill /home/{usuario}/Desktop/Images/fondo.jpg

15. Para configurar nuestra Polybar, clonaremos primeramente en 'Descargas' el siguiente repositorio:

   -     git clone https://github.com/VaughnValle/blue-sky.git

   Posteriormente, ejecutaremos los siguientes comandos:

   -     mkdir ~/.config/polybar
   -     cd ~/Descargas/blue-sky/polybar/
   -     cp * -r ~/.config/polybar
   -     echo '~/.config/polybar/./launch.sh' >> ~/.config/bspwm/bspwmrc
   -     cd fonts
   -     sudo cp * /usr/share/fonts/truetype/
   -     fc-cache -v

15.1 Hacemos Windows + Shift + R para cargar la configuración y deberíamos ver la Polybar por arriba.

16. Para configurar Picom y ajustar las transparencias además de bordeados de ventana, ejecutamos los siguientes pasos:

   -     mkdir ~/.config/picom
   -     cd ~/.config/picom
   -     cp ~/Descargas/blue-sky/picom.conf .

   Editamos el archivo picom.conf y cambiamos 'backend = "glx"' por 'backend = "xrender"', comentando el de glx. 
   Posteriormente, comentamos todas las líneas referentes a glx (En algunos ordenadores al dejar el glx puesto se puede llegar
   a experimentar una lentitud muy molesta).

   Antes de recargar la configuración, hacemos un seguimiento del ratón para saber en qué ventana estamos con la siguiente instrucción en el 'bspwm':

   -     bspc config focus_follows_pointer true

   Posteriormente, ejecutamos los siguientes comandos para aplicar los bordeados:

   -     echo 'picom --experimental-backends &' >> ~/.config/bspwm/bspwmrc
         echo 'bspc config border_width 0' >> ~/.config/bspwm/bspwmrc

17. Configuramos los colores de la polybar (paleta central), además de las paletas deseadas.

   Estructura de un nuevo módulo:

   Previamente tenemos que crear una carpeta en "~/.config/bin"

   -     [module/tumodulo]
         type = custom/script
         interval = 2
         exec = ~/.config/bin/binario.sh

   #Los modulos utilizados en estos dotfiles estan en la capeta bin de este repositorio

18. Configuramos el tema Nord de Rofi:

   -     mkdir -p ~/.config/rofi/themes
   -     cp ~/Descargas/blue-sky/nord.rasi ~/.config/rofi/themes

   Posteriormente con 'rofi-theme-selector' seleccionamos el tema Nord.

19. Instalamos slim y slimlock

   Instalamos los siguientes paquetes, no sin antes hacer una actualización:

   -     sudo apt update
   -     sudo apt install slim libpam0g-dev libxrandr-dev libfreetype6-dev libimlib2-dev libxft-dev

   Posteriormente, ejecutamos los siguientes comandos:

   -     cd ~/Descargas/
   -     git clone https://github.com/joelburget/slimlock.git
   -     cd slimlock/
   -     sudo make
   -     sudo make install
   -     cd ~/Descargas/blue-sky/slim
   -     sudo cp slim.conf /etc/
   -     sudo cp slimlock.conf /etc
   -     sudo cp -r default /usr/share/slim/themes

   Si queremos cambiar la imagen del panel, nos vamos a la ruta '/usr/share/slim/themes/default' y retocamos el archivo 'panel.png'.

20. Reiniciamos el sistema y una vez arrancado, incorporamos en el archivo 'bspwmrc' la siguiente línea para arreglar el cursor:

   -     xsetroot -cursor_name left_ptr &

21. Instalamos la powerlevel10k en zsh

22. Creamos enlace simbólico de la zshrc para root

23. Cambiamos el tipo de shell por defecto tanto para root como para el usuario con bajos privilegios

   -     usermod --shell /usr/bin/zsh tuUsuario
   -     usermod --shell /usr/bin/zsh root

24. Retocamos el archivo .p10k.zsh para adecuarlo a nuestro gusto

   Para el de root, podemos ir a 'POWERLEVEL9K_CONTEXT_ROOT_TEMPLATE' para asignar el Hashtag.

   Comentamos la siguiente línea:

   -     POWERLEVEL9K_CONTEXT_PREFIX='%246Fwith '

   Para evitar un pequeño problema de permisos a la hora de desde el usuario root migrar con 'su' al usuario con bajos privilegios,
   ejecutamos los siguientes comandos:

   -     chown {usuario}:{usuario} /root
         chown {usuario}:{usuario} /root/.cache -R
         chown {usuario}:{usuario} /root/.local -R

25. Instalamos bat, lsd, fzf y ranger

26. Instalar el plugin sudo

   Incorporamos posteriormente las siguientes líneas al final del zshrc para que
   al salir de vim el cursor recupere su aspecto de linea.

```
   Change cursor shape for different vi modes.
          function zle-keymap-select {
          if [[ $KEYMAP == vicmd ]] || [[ $1 = 'block' ]]; then
             echo -ne '\e[1 q'
          elif [[ $KEYMAP == main ]] || [[ $KEYMAP == viins ]] || [[ $KEYMAP = '' ]] || [[ $>
             echo -ne '\e[5 q'
          fi
         }
         zle -N zle-keymap-select

   Start with beam shape cursor on zsh startup and after every command.
   -      zle-line-init() { zle-keymap-select 'beam'}
```
27. Whichsystem.py, es un pequeno script que se ha hecho S4avitar en la maquina Blue de HackTheBox, todos los creditos de la creacion y por su tutorial para montar el     entorno de linux.

   -     https://github.com/Akronox/WichSystem.py

28. fastTCPScan.go, es la herramienta creada por S4avitar, todos los creditos de esta herramienta para el.
    Con fastTCPScan podremos hacer descubrimiento de puertos TCP.

Todos los créditos a sus respectivos desarrolladores.
 
Lian