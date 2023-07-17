---
layout: single
title: Bandit Decompressor
date: 2023-02-12
classes: wide
header:
  teaser: /assets/images/slae32.png
categories:
  - Bandit
  - Scripts
tags:
  - Bandit
  - Scripting
  - Bash
  - Bandit Decompressor
---
Hace un tiempo he venido obteniendo soltura en Bash, y para practicar un poco scripting con bandit he terminado desarrollando un pequeño script en bash para descomprimir un archivo que tiene una cantidad desconocida de archivos comprimidos en su interior, específicamente para bandit14, el script es útil porque no tienes que estar mirando y descomprimiendo uno por uno los archivos que tiene el archivo en su interior. Una vez descomprimido el archivo de bandit14 llamado **content.gzip**, por lo que no hay necesidad de saber si el nuevo archivo esta comprimido de nuevo y hacer el mismo proceso repetitivo.

El Script de Decompressor hace lo siguiente:
1. Teniendo el archivo **content.gzip**, el script leerá el último argumento del archivo adentro del comprimido.
2. Entrará en un bucle, siempre y cuando el último argumento sea también de tipo comprimido.
3. De ser así, seguirá descomprimiéndose hasta que ya no quede un archivo de tipo comprimido.
4. Decompressor sabra cuando el ultimo argumento no sea un archivo comprimido, asi que aplica un `/bin/cat` al archivo resultante.
5. Decompressor ayuda a acceder al contenido mucho mas rapido que si lo hicieramos descomprimiendo archivo por archivo.

1. El Script hace uso de sentencias de selección (if, else).
2. Usando `7z l **content.gzip**`, lo que haremos es listar el contenido del archivo sin extraerlo.
3. El uso de' grep `"Name" -A 2`, significa que grep buscará un patron en el stdout del comando `7z l al archivo content.gzip` y lo mostrara en pantalla.
4. Al hacer uso de `tail -n 1`, grep solo mostrara la ultima coincidencia con el patron "Name".
5. El comando `awk 'NF{print NF}'` Esto nos permite obtener únicamente el nombre del archivo descomprimido.
Finalmente, el nombre del archivo descomprimido se asigna a la variable `name_decompressed`.
### Codigo del Script
---------------
> Para mayor entendimiento del script y lo que hace, recomiendo probar un poco experimentar con los comandos grep, tail, awk y sus parámetros:
```bash
#!/bin/bash

name_decompressed=$(7z l content.gzip | grep "Name" -A 2 | tail -n 1 | awk 'NF{print $NF}')
7z x  content.gzip > /dev/null 2>&1

while true; do
	7z l $name_decompressed > /dev/null 2>&1
	if [ "$(echo $?)" == "0" ]; then
		decompressed_next=$(7z l $name_decompressed | grep "Name" -A 2 | tail -n 1 | awk 'NF{print $NF}')
		7z x $name_decompressed > /dev/null 2>&1 && name_decompressed=$decompressed_next
	else
		cat $name_decompressed; rm data* 2>/dev/null
		exit 1
	fi
done
```

Para usar correctamente Decompressor, al estar en el bandit14, hay que cambiar el nombre del archivo a **content.gzip**, de esta forma funcionara sin problemas.

Para conseguir el **content.gzip**, hacemos lo siguiente:
```
liann@nk:~/bandit14$ ls
data.hex
liann@nk:~/bandit14$ xxd -r data.hex > data
liann@nk:~/bandit14$ file data
data: gzip compressed data, was 'data2.bin' .......
liann@nk:~/bandit14$ mv data content.gzip
liann@nk:~/bandit14$ ./decompressor content.gzip
The password is .....
```

El Script es compilado y funciona correctamente:

<video controls>
  <source src="/assets/videos/Bandit%20Decompressor/decompressor.mp4" type="video/mp4">
  Tu navegador no admite la reproducción de video.
</video>

Esta publicacion ha sido creada como soporte en el aprendizaje de OverTheWire:

[https://overthewire.org/wargames/bandit/](https://overthewire.org/wargames/bandit/)

Lian
