---
title:  "Qué es data dummy y estructuras de datos estática-dinámica"
date:   2024-08-01 20:36:00 -0500
categories: [Data dummy, Estructura de datos estática, Estructura de datos dinámica]
tags: [data-dummy, estatica, dinamica] 
author: ok
---

## Definición de data dummy

> **Definición:** Un *data dummy* es un término utilizado en el ámbito de la informática y la ciencia de datos para referirse a un conjunto de datos ficticio o simulado. Estos datos son creados con el propósito de representar una estructura similar a la de datos reales, pero no contienen información genuina o significativa.
{: .prompt-warning }

### ¿Para qué sirve generar data dummy?

- **Son útiles en pruebas y experimentos**, ya que permiten probar algoritmos y modelos sin exponer datos reales.
- Pueden ser generados aleatoriamente o diseñados específicamente para ciertos escenarios.
- No deben utilizarse en situaciones donde se requiere información real y precisa, ya que su contenido carece de significado y validez fuera del contexto de pruebas y experimentos.

---

## Estructuras de datos estáticas y dinámicas

### Introducción

Las estructuras de datos son un concepto fundamental en la programación y se utilizan para almacenar y organizar datos de manera eficiente. Hay dos tipos principales de estructuras de datos: *estáticas* y *dinámicas*.

---

### Definición de estructuras de datos estáticas

> **Definición:** Una estructura de datos se considera *estática* si cumple con los siguientes requisitos:
>
> - Tener un **tamaño fijo y predefinido** en tiempo de compilación.
> - Su tamaño **no puede ser modificado** en tiempo de ejecución.
> - Los elementos se almacenan en **posiciones contiguas** de memoria, y los elementos son estructuras de datos estáticas también.
{: .prompt-warning }

---

### Ventajas y desventajas de las estructuras de datos estáticas**

> **Ventajas:**
> 
> - Acceso más rápido a los elementos, ya que su posición en memoria es conocida.
> - Menor consumo de memoria, ya que su tamaño es fijo y conocido en tiempo de compilación.
{: .prompt-info }

> **Desventajas:**
> 
> - No se puede modificar su tamaño durante la ejecución del programa.
> - Puede haber desperdicio de memoria si no se utiliza todo el espacio reservado.
{: .prompt-danger }

---

### Estructuras de datos dinámicas

> **Definición:** Una estructura de datos se considera *dinámica* si cumple con los siguientes requisitos:
> 
> - No tener un **tamaño fijo y predefinido** en tiempo de compilación.
> - Su tamaño **puede ser modificado** en tiempo de ejecución.
> - Los elementos **no necesariamente se almacenan en posiciones contiguas** de memoria.
{: .prompt-warning }

---

### Ventajas y desventajas de las estructuras de datos dinámicas

> **Ventajas:**
> 
> - Flexibilidad para cambiar su tamaño durante la ejecución del programa.
> - No hay desperdicio de memoria, ya que se utiliza solo el espacio necesario.
{: .prompt-info }

> **Desventajas:**
> 
> - Acceso más lento a los elementos, ya que su posición en memoria no es conocida.
> - Mayor consumo de memoria, ya que se necesita espacio adicional para los punteros que enlazan los elementos.
{: .prompt-danger }

### Conclusiones

- No hay una estructura de datos que sea superior por completo a otra.
- Dependiendo del problema propuesto, se debe analizar cuál es la estructura de datos más adecuada para la implementación de una solución.

---

¡Gracias por leer este artículo!
