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

```console
cd [-L | -P [-e]] directorio #directorio hacia donde quieres apuntar
```
```console
cd /usr/local/lib #por ejemplo
```
Ahora bien, algunas veces es necesario regresar a un directorio atrás, esto se realiza con el siguiente comando:

```console
cd .. #se mueve un directorio parent (principal) atrás (este quizá es más usado)
```

Ahora bien, podemos listar los elementos de una carpeta con el comando ls:

```console
cd Desktop/ #por ejemplo
ls
#muestra elementos o carpetas dentro del escritorio
```


## Compilación de código via shell o terminal

Una vez se entiende como funciona moverse entre directorios, podemos hablar un poco de la compilación de los programas. Por defecto, la mayoría de sistemas Linux (o basados en Linux como MacOS) tienen el motor de compilación **gcc**

No entraré en detalles con respecto a gcc, pero para el conocimiento básico, cuando uno descarga un IDE (como Eclipse, Netbeans entre otros) en linker compiler es gcc, es decir, es lo que permite interpretar el código y llevarlo a su ejecucion (básicamente)

Aunque con la experiencia y gusto, es posible utilizar la terminal y para eso se debe hacer lo siguiente:

1. Moverse al directorio donde se encuentre el archivo vía los comandos ya explicados.
2. Utilizar el comando gcc de la siguiente forma:

    ```bash
    gcc [nombre_de_tu_programa.c] -o el_nombre_de_tu_programa_compilado
    ```

    **gcc** sirve para mandar a llamar al compilador de C (en el caso de C++ se puede usar **gpp**) y el argumento *-o* se usa para nombrar al archivo ya compilado que es el que se va a correr.

3. Finalmente, al momento de compilar, es necesario correr el programa utilizando el comando siguiente:

    ```console
    ./el_nombre_de_tu_programa_compilado
    ```
## Github y sus comandos

Finalmente, para los amantes de Github, también hay comandos útiles.
En lo personal yo uso la aplicación de Github Desktop, pero estos comandos sirven cuando se tienen muchos archivos. La aplicación de escritorio permite solamente ir añadiendo un archivo a la vez, lo cual, si se tiene 50, 100 o más commits, puede ser tedioso.

```bash
git add --all
git commit -m "Comment";
git push
```
