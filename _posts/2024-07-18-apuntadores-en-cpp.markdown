---
layout: post
title:  "Apuntadores en C++"
date:   2024-07-18 22:49:00 -0500
categories: cpp
author: Oscar García
---

Un apuntador en C++ se usa para compartir una dirección de memoria entre diferentes contextos (principalmente funciones). Se utilizan cuando una función necesita modificar el contenido de una variable, pero no tiene propiedad de la misma.

Para acceder a la dirección de memoria de una variable, precede el nombre de la variable con el símbolo `&`. Por ejemplo, `&val` devuelve la dirección de memoria de `val`.

Esta dirección de memoria se asigna a un apuntador y se puede compartir entre funciones. Por ejemplo, `int *p = &val` asigna la dirección de memoria de `val` al apuntador `p`. Para acceder al contenido de la memoria apuntada, precede el nombre de la variable con un `*`. Por ejemplo, `*p` devolverá el valor almacenado en `val` y cualquier modificación se realizará en `val`.

**Ejemplo:** ¿Qué hace este código?

```cpp
#include <stdio.h>

void incrementar(int *v) {
    (*v)++;
}

int main() {
    int a;
    scanf("%d", &a);
    incrementar(&a);
    printf("%d\n", a);
    return 0;
}
```

## Actividad

Solucionar el problema de [HackerRank Pointer](https://www.hackerrank.com/challenges/c-tutorial-pointer/problem?isFullScreen=true).

**¡Gracias por leer este post!**
