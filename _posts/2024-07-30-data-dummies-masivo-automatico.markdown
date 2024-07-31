---
title:  "Data dummy masivo automático en C++"
date:   2024-07-30 23:00:00 -0500
categories: [C++, Data dummy, Data dummy automática, Programación orientada a objetos, Nodo]
tags: [c++, header, h-file, data-dummy, poo, node] 
author: ok
---

En el artículo [Representación de datos, comprensión de estructuras y Nodo en C++](https://opraupe0017.github.io/EDBlog/posts/data-dummies/) vimos cómo generar una data dummy e integrarla en un objeto de la clase `Node`. Esto es funcional cuando se trata de generar una cantidad pequeña de Nodos, ya que requiere que a través de ya sea escritura en el script o por medio de inputs de consola, se construyan los datos.

*Pero en este blog se trata de trabajar sobre estructura de datos* y **no nos sirve para nada** estudiar una estructura de datos si sólo es para aplicarlo sobre 1, 2, 3, o hasta sólamente 10 datos (nodos).

**Debemos encontrar la manera de crear cientos de miles o hasta millones de datos y saberlos guardar en nodos de forma automática**.

En este artículo haremos un ejemplo práctico en el que generaremos la cantidad de datos de personas que deseemos de forma automática. Sólo necesitaremos que nos pregunte la consola cuántas personas deseamos generar.

---

## Archivo de datos dummies

Para generar información aleatoria podemos utilizar un archivo de texto plano cualquiera que contenga información. **Por ejemplo** generemos un archivo llamado `nombres.txt` aur contenga algunos nombres

```cpp
Hugo
Paco
Luis
Rosita
```
{: file="nombres.txt" .nolineno }

## Archivo de encabezado para leer archivos `archivo.h`

Este header no sólo servirá para leer el archivo `nombres.txt`. También sirve para leer cualquier archivo de texto plano con datos que tengan una disposición similar. **¡Esto es extremadamente útil para poder generar data dummies de cualquier tipo!**

```cpp
#ifndef ARCHIVOH
#define ARCHIVO_H

#include <string>   // Para trabajar con palabras
#include <vector>   // Para trabajar con arreglos dinámicos
#include <fstream>  // Para trabajar con archivos
#include <cstdlib>  // Para std::rand y std::srand
#include <ctime>    // Para std::time

class Archivo {
private:
    std::vector<std::string> items;

public:
    // Constructor
    Archivo();

    // Método para leer los items desde un archivo
    void leerDesdeArchivo(const std::string& nombreArchivo);

    // Método para imprimir los items
    void imprimirItems() const;

    // Método para retornar un item aleatorio
    std::string obtenerItemAleatorio() const;
};

#endif // ARCHIVO_H
```
{: file="archivo.h" }

## La clase `Archivo`: `archivo.cpp`

Con `archivo.cpp` instanciamos la clase `Archivo`, definiendo el constructor y los métodos del mismo.

```cpp
#include "archivo.h"
#include <iostream>

// Constructor
Archivo::Archivo() {
    // Inicializar el generador de números aleatorios con el tiempo actual
    std::srand(static_cast<unsigned int>(std::time(0)));
}

// Método para leer los textos desde un archivo
void Archivo::leerDesdeArchivo(const std::string& nombreArchivo) {
    std::ifstream archivo(nombreArchivo);
    if (archivo.is_open()) {
        std::string texto;
        while (std::getline(archivo, texto)) {
            items.push_back(texto);
        }
        archivo.close();
    } else {
        std::cerr << "No se pudo abrir el archivo: " << nombreArchivo << std::endl;
    }
}

// Método para imprimir los items
void Archivo::imprimirItems() const {
    int i=1;
    for (const auto& item : items) {
        std::cout << "[" << i << "]: " << item << std::endl;
        i=i+1;
    }
    std::cout << std::endl;
}

// Método para retornar un item aleatorio
std::string Archivo::obtenerItemAleatorio() const {
    if (items.empty()) {
        return "No hay nombres en la lista.";
    }
    int indiceAleatorio = std::rand() % items.size();
    return items[indiceAleatorio];
}
```
{: file="archivo.cpp" }

## Archivo `test.cpp` de prueba

En `test.cpp` haremos una prueba de la funcionalidad. Este consistirá en imprimir la lista de todos los nombres que están en `nombres.txt` y después imprimirá un nombre aleatorio de esa lista.

```cpp
#include <iostream>
#include "archivo.h"

int main() {
    Archivo lista;
    lista.leerDesdeArchivo("nombres.txt");

    std::cout << "Lista de items:" << std::endl;
    lista.imprimirItems();

    std::cout << "Item aleatorio de la lista: " << lista.obtenerItemAleatorio() << std::endl;

    return 0;
}
```
{: file="test.cpp" }

### Proceso de compilación y ejecución

Sólo basta con ejecutar estas instrucciones desde la terminal

```bash
g++ -c archivo.cpp
g++ -o test test.cpp archivo.o
./test
```
{: file="Terminal" }

> **Pregunta:** ¿Cómo uso esto para generar data de personas aleatorias?
{: .prompt-danger }

## Hagamos muchas personas y guardémolas en nodos

Para lograr esto sólo vasta con generar un archivo `main.cpp` adecuado el cual utilice las clases definidas en el otro artículo `persona.cpp`, `node.cpp` y la clase nueva `archivo.cpp`.

```cpp
#include "persona.h"  // Incluye el archivo de cabecera persona.h
#include "archivo.h"  // Incluye el archivo de cabecera archivo.h
#include "node.h"     // Incluye el archivo de cabecera node.h
#include <cstdlib>    // Para std::rand y std::srand
#include <ctime>      // Para std::time
#include <vector>     // Para trabajar con arreglos dinámicos

int main() {
    // Inicializar el generador de números aleatorios con el tiempo actual
    std::srand(static_cast<unsigned int>(std::time(0)));

    // Crear un objeto Archivo y leer los nombres desde el archivo "nombres.txt"
    Archivo archivo;
    archivo.leerDesdeArchivo("nombres.txt");

    // Crear un vector de objetos Node
    std::vector<Node> nodos;

    // Genera pregunta en consola de cuántas personas quiere generar
    int numPersonas;
    std::cout << "Ingrese el número de personas que desea generar: ";
    std::cin >> numPersonas;

    // Generar nodos con personas de nombres y edades aleatorias
    for (int i = 0; i < numPersonas; ++i) { // Generar numPersonas nodos como ejemplo
        std::string nombreAleatorio = archivo.obtenerItemAleatorio();
        int edadAleatoria = std::rand() % 100; // Edad aleatoria entre 0 y 99
        Persona personaAleatoria(nombreAleatorio, edadAleatoria);
        nodos.emplace_back(personaAleatoria);
    }

    // Imprimir los datos de cada nodo
    for (const auto& nodo : nodos) {
        std::cout << nodo.getData() << std::endl;
    }

    return 0;
}
```
{: file="main.cpp" }

### Proceso de compilación y ejecución

Sólo basta con ejecutar estas instrucciones desde la terminal

```bash
g++ -c archivo.cpp
g++ -c persona.cpp
g++ -c nodo.cpp
g++ -o main main.cpp persona.o node.o archivo.o
./main
```
{: file="Terminal" }

> **Actividades :**
> 1. Generar cédulas dummy para las personas que estamos generando.
> 1. Generar género dummy para las personas que estamos generando.
> 1. Generar estatura dummy para las personas que estamos generando.
> 1. Generar peso dummy para las personas que estamos generando.
> 1. Generar 200 data dummies de automobiles con varias marcas (Ferrary, Renault, Suzuki, ...), colores (rojo, blanco, morado, ...), modelos (1999, 1975, 2007, ...).
{: .prompt-tip }
