---
title:  "Entrada y salida estándar en C++"
date:   2024-07-18 21:43:00 -0500
categories: [Biblioteca estándar, entrada estándar, salida estándar, C++]
tags: [iostream, std, cin, cout, c++] 
author: ok
---

Practiquemos la lectura de entradas desde stdin y la impresión de salidas en stdout. Para ello debemos importar la biblioteca `iostream` usando esta sintaxis:

```cpp
#include <iostream>
```

En C++, puedes leer un único token separado por espacios usando `std::cin` y puedes imprimir salidas en stdout usando `std::cout`. Por ejemplo, supongamos que declaramos las siguientes variables:

```cpp
std::string s;
int n;
```

y queremos usar `cin` para leer la entrada "High 5" desde stdin. Podemos hacerlo con el siguiente código:

```cpp
std::cin >> s >> n;
```

Esto lee la primera palabra ("High") desde stdin y la guarda como `std::string s`, luego lee la segunda palabra ("$5$") desde stdin y la guarda como `int n`. Si queremos imprimir estos valores en stdout, separados por un espacio, escribimos el siguiente código:

```cpp
std::cout << s << " " << n << std::endl;
```

Este código imprime el contenido de la `std::string s`, un espacio (`" "`), y luego el `int n`. Terminamos nuestra línea de salida con un salto de línea usando `endl`. Esto da como resultado la siguiente salida:

```sh
High 5
```

## Actividad 1

Lee $3$ números desde stdin y imprime su suma en stdout.

**Formato de Entrada**

Una línea que contiene $3$ enteros separados por espacios: `a`, `b` y `c`.

**Restricciones**

Ninguna restricción específica.

**Formato de Salida**

Imprime la suma de los $3$ números en una sola línea.

**Entrada de Muestra**

```sh
1 2 7
```

**Salida de Muestra**

```sh
10
```

**Explicación**

La suma de los $3$ números es `1 + 2 + 7 = 10`.

## Actividad 2

Para practicar sintaxis. solucionar los problemas de introducción a programación en `C++` en este [link de HackerRank](https://www.hackerrank.com/domains/cpp?filters%5Bsubdomains%5D%5B%5D=cpp-introduction).

## Referencias

- [Hackerrank, problema Input and Output](https://www.hackerrank.com/challenges/cpp-input-and-output?isFullScreen=true).

**¡Gracias por leer este post!**
