---
title:  "Arreglos unidimensionales en C++"
date:   2024-08-01 20:36:00 -0500
categories: [C++, Arreglo unidimensional, Programación orientada a objetos, Nodo, Data dummy]
tags: [c++, header, h-file, arreglo-unidimensional, poo, node, data-dummy] 
author: ok
---

En este artículo exploraremos la del tipo estática con la primera estructura de datos que debemos conocer el **arreglo unidimensional** `Array`.

## Definición Arreglo unidimensional estático

> **Definición:** Un **arreglo unidimensional estático de tamaño $n$** es una estructura de datos estática lineal que:
> 
> - Se debe definir previamente la longitud $n$.
> - Almacena una colección de $n$ elementos del *mismo tipo*.
> - Cada elemento se identifica mediante un *índice entero no negativo*.
{: .prompt-warning }

![arreglo entero](/assets/img/0005_arreglo_entero.png)
_Arreglo unidimensional de longitud 7 de enteros._

![arreglo cadena](/assets/img/0006_arreglo_cadena.png)
_Arreglo unidimensional de longitud 6 de cadenas de caracteres._

![arreglo persona](/assets/img/0007_arreglo_objeto.png)
_Arreglo unidimensional de longitud 5 de estructuras estáticas del mismo tipo Persona._

---

## Clase `Array` en `C++` para arreglo de personas

> Cuando sea requerido manipular información que requiera un arreglo unidimensional, **se deberá utilizar esta clase**. No se permite utilizar `vector` u otras estructuras similares de bibliotecas que no sean parte de su invención.
{: .prompt-danger }

### Código y encabezado `array.h` y `array.cpp`

```cpp
#ifndef ARRAY_H
#define ARRAY_H

#include "node.h"
#include <iostream>                  // Para std::ostream

class Array {
private:
    int MAX_SIZE;                    // Tamaño máximo del arreglo de nodos
    Node *elements;                  // Puntero a un arreglo de nodos
    int size;                        // Tamaño actual del arreglo

public:
    Array();                         // Constructor por defecto
    Array(int n);                    // Constructor para construir un arreglo de tamaño n
    ~Array();                        // Destructor para liberar la memoria

    // Métodos para manipular el arreglo
    void insert(const Persona &data, int index); // inserta un nodo en el Array        
    bool isEmpty() const;               // verifica si el array está vacío
    void remove(int index);             // elimina un nodo según la posición en el index
    void swap(int index1, int index2);  // intercambio de nodos según las posiciones
    int getSize() const;                // retorna el tamaño del Array
    Node get(int index) const;          // obtener el nodo según la posición index

    // Método para listar los elementos del arreglo
    void listar() const;
};

#endif // ARRAY_H
```
{: file="array.h" }

```cpp
#include "array.h"
#include <stdexcept> // Para std::invalid_argument

Array::Array() : size(0) {
    MAX_SIZE = 100;
    elements = new Node[MAX_SIZE]; // Asigna memoria para el arreglo de tamaño MAX_SIZE
}

Array::Array(int n) : size(0) {
    MAX_SIZE = n;
    if (n <= 0 || n > MAX_SIZE) {
        throw std::invalid_argument("Tamaño inválido especificado para el arreglo");
    }
    elements = new Node[n]; // Asigna memoria para el arreglo de tamaño n
}

Array::~Array() {
    delete[] elements; // Libera la memoria asignada al arreglo
}

void Array::insert(const Persona &data, int index) {
    if (index < 0 || index > size) {
        throw std::out_of_range("Índice fuera de rango al insertar en el arreglo");
    }
    if (size >= MAX_SIZE) {
        throw std::overflow_error("El arreglo está lleno, no se puede insertar más elementos");
    }

    // Desplaza los elementos hacia la derecha para hacer espacio para el nuevo nodo
    for (int i = size; i > index; --i) {
        elements[i] = elements[i - 1];
    }

    // Inserta el nuevo nodo en la posición index
    elements[index] = Node(data);
    size++;
}

bool Array::isEmpty() const {
    return size == 0;
}

void Array::remove(int index) {
    if (index < 0 || index >= size) {
        throw std::out_of_range("Índice fuera de rango al eliminar del arreglo");
    }

    // Desplaza los elementos hacia la izquierda para eliminar el nodo en la posición index
    for (int i = index; i < size - 1; ++i) {
        elements[i] = elements[i + 1];
    }

    // Reducción del tamaño del arreglo
    size--;

    // Elimina el último nodo
    elements[size] = Node();
}

void Array::swap(int index1, int index2) {
    if (index1 < 0 || index1 >= size || index2 < 0 || index2 >= size) {
        throw std::out_of_range("Índice fuera de rango al intercambiar elementos del arreglo");
    }

    // Intercambia los nodos en las posiciones index1 y index2
    Node temp = elements[index1];
    elements[index1] = elements[index2];
    elements[index2] = temp;
}

int Array::getSize() const {
    return size;
}

Node Array::get(int index) const {
    if (index < 0 || index >= size) {
        throw std::out_of_range("Índice fuera de rango al obtener elemento del arreglo");
    }

    return elements[index];
}

void Array::listar() const {
    //std::cout << "Elementos del arreglo:" << std::endl;
    std::cout << "[ARRAY ("<< MAX_SIZE <<")]" << std::endl;
    for (int i = 0; i < MAX_SIZE; ++i) {
        std::cout << " \u251C ARRAY[" << i << "] : " << elements[i].getData() << std::endl;
        // el texto \u251C es el carácter ├
    }
    std::cout << " └ FIN" << std::endl;
}
```
{: file="array.cpp" }


## Ejemplo práctico: arreglo de personas

Consideremos el siguiente archivo `main.cpp` el cual tiene como dependencias los encabezados 

- `persona.h` y `persona.cpp`: Clase `Persona` adaptada para que tenga información de:
  - `nombre`: Nombre de la persona,
  - `edad`: Número entre $0$ y $100$,
  - `id`: Número entero entre $1000000000$ y $1999999999$,
  - `genero`: Booleano `true` y `false` para mujer y hombre respectivamente,
- `node.h` y `node.cpp`: Clase `Nodo`,
- `archivo.h` y `archivo.cpp`: Clase `Archivo.`
- `array.h` y `array.cpp`: Clase `Array`.

```cpp
#include "persona.h"  // Incluye el archivo de cabecera persona.h
#include "archivo.h"  // Incluye el archivo de cabecera archivo.h
#include "array.h"    // Incluye el archivo de cabecera array.h
#include <cstdlib>    // Para std::rand y std::srand
#include <ctime>      // Para std::time
//#include <vector>   // Usaremos Array en su lugar

int main() {
    // Inicializar el generador de números aleatorios con el tiempo actual
    std::srand(static_cast<unsigned int>(std::time(0)));

    // Crear un objeto Archivo y leer los nombres desde el archivo "nombres.txt"
    Archivo archivo;
    archivo.leerDesdeArchivo("nombres.txt");

    // Genera pregunta en consola de cuántas personas quiere generar
    int numPersonas;
    std::cout << "Ingrese el número de personas que desea generar: ";
    std::cin >> numPersonas;

    // Crear un objeto Array
    Array nodos(numPersonas);

    // Verificar si el arreglo está vacío
    if (nodos.isEmpty()) {
        std::cout << "El arreglo está vacío." << std::endl;
    }
    else {
        std::cout << "El arreglo no está vacío." << std::endl;
    }

    // Obtener el tamaño del arreglo
    int tam = nodos.getSize();
    std::cout << "Tamaño del arreglo: " << tam << std::endl;

    // Generar nodos con personas de nombres y edades aleatorias
    for (int i = 0; i < numPersonas; ++i) { // Generar numPersonas nodos como ejemplo
        std::string nombreAleatorio = archivo.obtenerItemAleatorio();
        int edadAleatoria = std::rand() % 101; // Edad aleatoria entre 0 y 100
        int idAleatorio = 1000000000 + (std::rand() % 1000000000); // ID aleatorio entre 1000000000 y 1999999999
        
        bool generoAleatorio;
        if (std::rand() % 2 == 0) {
            generoAleatorio = true;
        }
        else {
            generoAleatorio = false;
        }

        Persona personaAleatoria(nombreAleatorio, edadAleatoria, idAleatorio, generoAleatorio);

        // Insertar el nodo en el arreglo
        nodos.insert(personaAleatoria, i);
    }

    // Imprimir los datos de cada nodo
    nodos.listar();

    // Ejemplo de eliminar
    std::cout << "Inserta posición a eliminar: ";
    int pos;
    std::cin >> pos;
    nodos.remove(pos);
    nodos.listar();

    // Ejemplo de intercambiar
    std::cout << "Inserta dos posiciones a intercambiar: ";
    int pos1, pos2;
    std::cin >> pos1 >> pos2;
    nodos.swap(pos1, pos2);
    nodos.listar();

    // Obtener el tamaño del arreglo
    tam = nodos.getSize();
    std::cout << "Tamaño del arreglo: " << tam << std::endl;

    // Obtener un nodo específico
    std::cout << "Inserta posición a obtener: ";
    std::cin >> pos;
    Node nodoObtenido = nodos.get(pos);
    std::cout << "Nodo obtenido: " << nodoObtenido.getData() << std::endl;

    // Comparar edades de dos personas por índice
    std::cout << "Inserta dos posiciones a comparar: ";
    int pos1, pos2;
    std::cin >> pos1 >> pos2;
    if (nodos.get(pos1).getData() > nodos.get(pos2).getData()) {
        std::cout << "La persona en la posición " << pos1 << " es mayor que la persona en la posición " << pos2 << std::endl;
    }
    else if (nodos.get(pos1).getData() < nodos.get(pos2).getData()) {
        std::cout << "La persona en la posición " << pos1 << " es menor que la persona en la posición " << pos2 << std::endl;
    }
    else {
        std::cout << "Las personas tienen la misma edad." << std::endl;
    }

    return 0;
}
```
{: file="main.cpp" }

---

## Actividad

> 1. Completar la clase `Persona` con la información de `id` y `género` para que el archivo `main.cpp` pueda compilarse.
> 2. Implementar método `update(Persona &data, int index)` en `Array`, el cual permita ingresar la información de una persona en una posición, sobreescribiendo lo que esté en dicha posición.
> 3. Implementar método `searchById(int id)` en `Array`, el cuál entregue la posición del arreglo cuya persona coincida con el valor del `id`.
{: .prompt-warning }

---

### Compilación y ejecución de la prueba `main.cpp`

```cpp
g++ -c persona.cpp
g++ -c node.cpp
g++ -c archivo.cpp
g++ -c array.cpp
g++ -o main main.cpp persona.o node.o archivo.o array.o
./main
```
{: file="Terminal" }

---

¡Gracias por leer este artículo!
