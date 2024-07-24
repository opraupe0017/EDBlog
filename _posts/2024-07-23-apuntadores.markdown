---
layout: post
title:  "Apuntadores"
date:   2024-07-23 6:00:00 -0500
categories: cpp
author: Oscar García
---

El contenido de este artículo le pertenece al los Profesores **Édison Valencia** y **Mauricio Árias**, quienes me han permitido compartirlo por este medio.

## Contenidos
{:.no_toc}

* TOC
{:toc}

---

En este artículo podremos encontrar información básica acerca de los apuntadores.

Un **apuntador** es un concepto fundamental en la informática que se refiere a una **variable que almacena la dirección de memoria de otra variable**. Este concepto permite un manejo más *eficiente* y *flexible* de la memoria, ya que se puede acceder y manipular datos de manera directa.

## Definición de apuntador

> **Definición:** Un **apuntador** es una variable cuyo valor es una dirección de memoria. En lugar de contener datos como enteros o caracteres, contiene la ubicación en memoria donde se encuentran esos datos.

> **Observación:** Puedes pensar en un apuntador como un "indicador" que señala la ubicación de otra variable, similar a cómo una dirección postal señala la ubicación de una casa.

---

## Beneficios de los apuntadores

1. **Eficiencia de memoria:** Reducen la necesidad de copias de datos, optimizando el uso de memoria.
1. **Flexibilidad:** Facilitan la creación y manipulación de estructuras de datos complejas y dinámicas.
1. **Rendimiento:** Mejoran el rendimiento del programa al permitir un acceso más rápido y directo a los datos.
1. **Consumo de energía:** Al reducir la necesidad de copias de datos, se optimiza el consumo de energía al disminuir el consumo de memoria.

---

## Propiedades de los apuntadores

1. **Dirección de Memoria:** Un apuntador almacena la dirección de otra variable.
1. **Acceso Indirecto:** Se puede acceder a los datos almacenados en la dirección a la que apunta.
1. **Asignación y Desasignación Dinámica:** Permiten la asignación dinámica de memoria, es decir, reservar y liberar memoria durante la ejecución del programa.

---

## Tipos de apuntadores

1. **Apuntadores Nulos:** Apuntadores que no apuntan a ninguna dirección válida. En muchos lenguajes, se representan por un valor especial (por ejemplo, nullptr en C++).
Apuntadores a Datos: Apuntadores que almacenan la dirección de variables de datos (como enteros, caracteres, etc.).
1. **Apuntadores a Apuntadores:** Apuntadores que almacenan la dirección de otros apuntadores, permitiendo múltiples niveles de indirección.
1. **Apuntadores a Funciones:** Apuntadores que almacenan la dirección de funciones, permitiendo llamar a funciones a través de apuntadores.
1. **Apuntadores a Miembros de Clases:** En lenguajes orientados a objetos, apuntadores que almacenan la dirección de miembros de clases (como datos miembro o funciones miembro).

---

## Uso de los Apuntadores

1. **Acceso y Manipulación de Datos:** Permiten acceder y modificar datos en ubicaciones de memoria específicas.
1. **Paso de Parámetros por Referencia:** Permiten pasar argumentos a funciones por referencia, evitando copias innecesarias y permitiendo la modificación de los datos originales.
1. **Asignación Dinámica de Memoria:** Facilitan la gestión de memoria durante la ejecución del programa, permitiendo reservar y liberar memoria según sea necesario.
1. **Estructuras de Datos Dinámicas:** Son esenciales para implementar estructuras de datos dinámicas como listas enlazadas, árboles y grafos.
1. **Interacción con el Sistema y el Hardware:** En programación de bajo nivel, los apuntadores son esenciales para interactuar directamente con el hardware y el sistema operativo.

---

## Ejemplos conceptuales

Veamos algunos ejemplos que ilustran cómo los **apuntadores** pueden utilizarse para el paso de parámetros por referencia, permitiendo que las funciones modifiquen los valores originales de las variables. El lenguaje utilizado es `C++` debido a su claridad para la enseñanza de conceptos de memoria y apuntadores.

### Ejemplo 1. Paso de Parámetros por Valor (Sin Apuntadores)

En el **paso de parámetros por valor**, se pasa una **copia de la variable** a la función. Cualquier cambio realizado dentro de la función **no afecta** la variable original. Le suelo decir a esto *"lo que se hace en las Vegas, se queda en las Vegas"*.

```cpp
#include <iostream>
using namespace std;

void incrementarPorValor(int num) {
    num += 1; // Incrementa la copia local de num
}

int main() {
    int numero = 5;
    incrementarPorValor(numero);
    cout << "Valor después de incrementarPorValor: " << numero << endl; // Output: 5
    return 0;
}
```

**Explicación Detallada:**
1. **Definición de la Función:**
   - `void incrementarPorValor(int num)`: La función toma un entero `num` como argumento.
   - Dentro de la función, se incrementa `num` en `1`.
1. **Llamada a la Función:**
   - En `main()`, se define una variable `numero` y se inicializa a `5`.
   - Se llama a `incrementarPorValor(numero)`, pasando `numero` por **valor**.
   - El valor de `numero` en `main()` **no se modifica**, ya que la función trabaja con una **copia local**.

### Ejemplo 2. Paso de Parámetros por Referencia (Con Apuntadores)

En el **paso de parámetros por referencia**, se pasa la **dirección de la variable** a la función. Esto permite que la función **modifique** el valor original de la variable.

```cpp
#include <iostream>
using namespace std;

void incrementarPorReferencia(int* numPtr) {
    *numPtr += 1; // Incrementa el valor al que apunta numPtr
}

int main() {
    int numero = 5;
    incrementarPorReferencia(&numero); // Pasa la dirección de 'numero' a la función
    cout << "Valor después de incrementarPorReferencia: " << numero << endl; // Output: 6
    return 0;
}
```

**Explicación Detallada:**
1. **Definición de la Función:**
   - `void incrementarPorReferencia(int* numPtr)`: La función toma un **apuntador** a entero `numPtr` como argumento.
   - Dentro de la función, se incrementa el valor al que apunta `numPtr` en `1`.
1. **Llamada a la Función:**
   - En `main()`, se define una variable `numero` y se inicializa a `5`.
   - Se llama a `incrementarPorReferencia(&numero)`, pasando la **dirección** de `numero` a la función.
   - La función modifica el valor original de `numero`, incrementándolo en `1`.

---

## Actividad 1

Solucionar el problema de [HackerRank Pointer](https://www.hackerrank.com/challenges/c-tutorial-pointer/problem?isFullScreen=true).

---

## Referencias

- _Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C._ (2009). **Introduction to Algorithms** (3.a ed.). MIT Press.

- _Riordan, M., & Hoddeson, L._ (1997). **Crystal Fire: The Birth of the Information Age**. W.W. Norton & Company.

- _Sedra, A. S., & Smith, K. C._ (2015). **Microelectronic Circuits** (7.a ed.). Oxford University Press.

---

**¡Gracias por leer este post!**
