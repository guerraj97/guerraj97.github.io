---
title: "Comandos básicos en la terminal y otros"
date: 2020-07-30
tags: [Commands,Linux, programming]
excerpt: "bash-commands, Linux, terminal"
mathjax: "true"
---

# Introducción a los comandos básicos en Linux

Aunque Linux es una herramienta que pocos conocen, el potencial que aporta es inigualable. El objetivo de este post (que por cierto es mi primer post) es mostrar un poco de los comandos básicos que Linux tiene para usarse en la terminal, algo que, cuando se le toma el gusto a este tipo de interfaces, son muy útiles y permiten acceder de manera rápida a las funciones.

## Búsqueda de archivos y acceso a directorios
Normalmente, estamos acostumbrados a la búsqueda de archivos dando click en las respectivas carpetas.
Aunque común, Linux ofrece muchas herramientas (como gcc, por ejemplo) de compilación de programas, que no requieren un IDE o interfaz para crear y probar código.

Aunque, si bien es cierto, alguien que ya ha probado estas herramientas conozca los comandos que se denotan a continuación, la intención radica en mostrarles a los *novatos* como utilizar y que comandos básicos hay para esto.

El primero es el ***cambiar directorio*** o **change directory** y, tal como su nombre lo indica, sirve para poder moverse entre los directorios del sistema. La sintaxis sería algo así:

```zsh
cd [-L | -P [-e]] directorio #directorio hacia donde quieres apuntar
```
```zsh
cd /usr/local/lib #por ejemplo
```
Ahora bien, algunas veces es necesario regresar a un directorio atrás, esto se realiza con el siguiente comando:

```zsh
cd .. #se mueve un directorio parent (principal) atrás (este quizá es más usado)
```

Ahora bien, podemos listar los elementos de una carpeta con el comando ls:

```zsh
cd Desktop/ #por ejemplo
ls
#muestra elementos o carpetas dentro del escritorio
```


###Encabezado 3

*italics*

**bold**

bullet list:
* 1
* 2

number List:
1 a
2 b

Python code block:

```python
import numpy as np
np.sum(x,y)
```

otras lineas `c+y`

Algo de mate:

$$z = x + y $$

prueba de bash

```bash
git add --all
git commit -m "Comment";
git push
```
