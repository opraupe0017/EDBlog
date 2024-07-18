---
layout: post
title:  "Hello World! en C++"
date:   2024-07-16 12:00:00 -0500
categories: cpp
author: Oscar García
---

## Contenidos
{:.no_toc}

* TOC
{:toc}

En esta publicación, aprenderemos a crear un programa en **C++** que imprima en consola el mensaje **"Hello World!"**. Este es el clásico primer programa que se escribe al aprender un nuevo lenguaje de programación. ¡Vamos a empezar!

## Paso 1: Escribir el programa

Abre tu **IDE** o editor de texto preferido y crea un nuevo archivo llamado `hello_world.cpp`. Escribe el siguiente código en el archivo:

```cpp
#include <iostream>

int main() {
    std::cout << "Hello World!" << std::endl;
    return 0;
}
```

### Explicación del código

- `#include <iostream>`: Esta línea incluye la librería de entrada/salida estándar de **C++** que nos permite usar `std::cout`.
- `int main() { ... }`: Esta es la función principal del programa. Todo el código dentro de estas llaves `{}` se ejecutará al iniciar el programa.
- `std::cout << "Hello World!" << std::endl;`: Esta línea imprime el mensaje **"Hello World!"** en la consola.
- `return 0;`: Esta línea indica que el programa terminó exitosamente.

## Paso 2: Compilar el programa usando GCC

Una vez que hayas escrito el código, necesitas **compilarlo** para convertirlo en un programa ejecutable.

1. Abre la terminal o línea de comandos.
2. Navega hasta el directorio donde guardaste `hello_world.cpp`.
3. Ejecuta el siguiente comando para compilar el programa:

   ```sh
   g++ -o hello_world hello_world.cpp
   ```

   Este comando crea un archivo ejecutable llamado `hello_world`.

## Paso 3: Ejecutar el programa

Finalmente, ejecuta el programa compilado para ver el resultado.

En la línea de comandos, escribe:

```sh
./hello_world
```

Deberías ver el mensaje **"Hello World!"** impreso en la consola.

**¡Felicitaciones!** Has creado y ejecutado tu primer programa en **C++**. Este es solo el comienzo de tu viaje en la programación con **C++**. ¡Sigue practicando y explorando más conceptos y funcionalidades del lenguaje!

**¡Gracias por leer este post!**
