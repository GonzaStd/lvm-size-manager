## 📌 ➖ Reducir Volúmen Lógico (LV)

Primero hay que **reducir el sistema de archivos** y luego el *LV*:

1️⃣ Verificar volúmen: `e2fsck -f /dev/mapper/<nombre-vg>--vg-<lv>
> *vg* significa *Volume Group*

2️⃣ Reducir el sistema de archivos: `resize2fs /dev/mapper/<nombre-vg>--vg-<lv> XG`

>`X`es el número de GB para el tamaño FINAL al que queremos reducir el *filesystem*.

3️⃣ Reducir el volúmen lógico `lvreduce -L XG /dev/mapper/<nombre-vg>--vg-<lv>

> `X` es el número de GB para el tamaño FINAL al que queremos reducir el volúmen, pero también podemos usar `-X` para indicar el tamaño al que se RESTA o REDUCE.

Ejemplo: Si el volúmen tiene **150GB** y queremos sacarle **50GB**
`sudo lvreduce -L -50G /dev/mapper/<nombre-vg>--vg-<lv>`

## 📌 ➕ Extender Volúmen Lógico (LV)

Primero hay que **extender el volumen** y luego el fs:

1️⃣ Verificar volúmen: `e2fsck -f /dev/mapper/<nombre-vg>--vg-<lv>

2️⃣ Extender el volúmen lógico `lvextend -L XG /dev/mapper/<nombre-vg>--vg-<lv>

> `X` es el número de GB para el tamaño FINAL al que queremos extender el volúmen, pero también podemos usar `+X` para indicar el tamaño al que se SUMA o EXTIENDE.

Ejemplo: Si el volúmen tiene **150GB** y queremos agregarle **50GB**
`sudo lvreduce -L +50G /dev/mapper/<nombre-vg>--vg-<lv>`

3️⃣ Extender el sistema de archivos: `resize2fs /dev/mapper/<nombre-vg>--vg-<lv>

>El fs se acomoda automáticamente al tamaño del volúmen.

## ✅ Comandos Extra

- **Ver el tamaño de nuestro grupo de volúmenes y su espacio libre**: `vgs`
- **Ver el tamaño de nuestros volúmenes**: `lvs`
- **Ver el tamaño de los sistemas de archivos**: `df -h`

