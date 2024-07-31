---
title:  "Representación de datos, comprensión de estructuras y Nodo en C++"
date:   2024-07-23 7:00:00 -0500
categories: [C++, Archivos de encabezado, Data dummy, Data dummy manual, Programación orientada a objetos, Nodo]
tags: [c++, header, h-file, data-dummy, poo, node] 
author: ok
---

El contenido de este artículo le contiene aportes de los Profesores **Édison Valencia** y **Mauricio Árias**, quienes me han permitido compartirlo por este medio.

En este artículo conoceremos un poco sobre **programación orientada a objetos** (**POO**) y cómo generar data dummy en `C++` y almacenar la información en nodos.

---

## Los archivos de encabezado (los de extensión `.h`)

Un archivo `.h` en `C` y `C++` es un archivo de encabezado (header file) que contiene declaraciones de funciones, macros, constantes, tipos de datos, y clases. Estos archivos son utilizados para permitir la reutilización de código y para separar la interfaz de la implementación en programas grandes. Aquí están algunos de los principales usos y características de los archivos `.h`:

1. **Declaraciones de Funciones**: Contienen declaraciones de funciones que serán implementadas en archivos `.c` o `.cpp`. Esto permite que otras partes del programa puedan llamar a estas funciones sin conocer su implementación detallada.

    ```cpp
    // archivo.h
    void miFuncion(int a);
    ```

2. **Definiciones de Tipos y Estructuras**: Permiten definir tipos de datos personalizados y estructuras que pueden ser utilizados en múltiples archivos.

    ```cpp
    // archivo.h
    typedef struct {
        int x;
        int y;
    } Punto;
    ```

3. **Declaraciones de Clases**: En C++, los archivos de encabezado se utilizan para declarar clases, incluyendo sus atributos y métodos, pero sin proporcionar las implementaciones de los métodos.

    ```cpp
    // Persona.h
    class Persona {
    private:
        std::string nombre;
        int edad;

    public:
        Persona(const std::string &nombre, int edad);
        std::string getNombre() const;
        int getEdad() const;
        void setNombre(const std::string &nombre);
        void setEdad(int edad);
    };
    ```

4. **Macros y Constantes**: Los archivos de encabezado también pueden contener definiciones de macros y constantes que pueden ser utilizadas en varias partes del programa.

    ```cpp
    // archivo.h
    #define PI 3.14159265359
    #define SQUARE(x) ((x) * (x))
    ```

5. **Incluir Archivos**: Se pueden incluir en otros archivos fuente (.c, .cpp) o en otros archivos de encabezado utilizando la directiva `#include`.

    ```cpp
    // main.cpp
    #include "archivo.h"

    int main() {
        miFuncion(5);
        return 0;
    }
    ```

6. **Guardias de Inclusión**: Para evitar inclusiones múltiples del mismo archivo de encabezado, se utilizan guardias de inclusión. Estas son preprocesadores que aseguran que el contenido del archivo solo se incluya una vez durante la compilación.

    ```cpp
    // archivo.h
    #ifndef ARCHIVO_H
    #define ARCHIVO_H

    void miFuncion(int a);

    #endif // ARCHIVO_H
    ```

En resumen, los archivos `.h` son fundamentales para la organización y modularización del código en C y C++. Ayudan a mantener el código limpio, reutilizable y fácil de mantener, separando la interfaz (declaraciones) de la implementación (definiciones).

---

## Elementos funcionales para representar datos y componer estructuras

En computación, el orden y escalabilidad de las líneas de código, es una estrategia clave para disminuir los errores y lograr una eficiencia en la creación de aplicaciones informáticas. Las estructuras de datos van más allá de componer una conjunto de variables que identifican el tipo de datos y las relación entre las variables. Requieren de diseñar algoritmos para representar los valores de las variables, las relación entre ellas y la eficiencia para custodiar, buscar, actualizar y limpiar información compuesta de variables.

Esta es la razón para estudiar las estructuras de datos en los cursos de programación. Iniciando con las diversas estrategias computacionales que favorecen la relación entre las variables según el problema y favoreciendo la búsqueda, la relación y la selección de los valores de la variables, que conforman información a partir de datos.

Desde esta idea, consideremos una estructura inspirada en la programación orientada por objetos, que separe los algoritmos de relacionados con las estructuras con los algoritmos que manejan los datos como valor de variables.
El primer conjunto de variables la **definimos como objetos**.

### Ejemplo 1. Data dummy de una persona ¨hecha a mano¨

#### Script de `persona.h`

```cpp
#ifndef PERSONA_H  // Comienza una guardia de inclusión para evitar inclusiones múltiples del archivo
#define PERSONA_H

#include <iostream>  // Incluye la librería iostream para la entrada y salida estándar
#include <string>    // Incluye la librería string para usar el tipo std::string

// Definición de la clase Persona
class Persona {
private:
    std::string nombre;  // Atributo para almacenar el nombre de la persona
    int edad;            // Atributo para almacenar la edad de la persona

public:
    // Constructor
    Persona(const std::string &nombre, int edad);  // Constructor que inicializa los atributos nombre y edad

    // Métodos getter (accesores)
    std::string getNombre() const;  // Método para obtener el nombre de la persona
    int getEdad() const;            // Método para obtener la edad de la persona

    // Métodos setter (mutadores)
    void setNombre(const std::string &nombre);  // Método para establecer el nombre de la persona
    void setEdad(int edad);                     // Método para establecer la edad de la persona

    // Sobrecarga del operador << para imprimir el objeto Persona
    friend std::ostream& operator<<(std::ostream &out, const Persona &persona);
};

#endif // PERSONA_H
```

**`persona.h`:**

- **Guardas de inclusión** (`#ifndef`, `#define`, `#endif`): Estas directivas aseguran que el archivo de encabezado no se incluya múltiples veces, evitando problemas de redefinición.
- **Definición de la clase Persona:** Incluye atributos privados, un constructor, y métodos públicos.

#### Script de `persona.cpp`

```cpp
#include "persona.h"  // Incluye el archivo de cabecera persona.h

// Definición del constructor
Persona::Persona(const std::string &nombre, int edad) : nombre(nombre), edad(edad) {}

// Definición de los métodos getter
std::string Persona::getNombre() const {
    return nombre;
}

int Persona::getEdad() const {
    return edad;
}

// Definición de los métodos setter
void Persona::setNombre(const std::string &nombre) {
    this->nombre = nombre;
}

void Persona::setEdad(int edad) {
    this->edad = edad;
}

// Definición de la sobrecarga del operador <<
std::ostream& operator<<(std::ostream &out, const Persona &persona) {
    out << "Nombre: " << persona.nombre << ", Edad: " << persona.edad;
    return out;
}
```

**`persona.cpp`:**

- **Constructor:** Inicializa los atributos `nombre` y `edad`.
- **Métodos `getNombre` y `getEdad`:** Devuelven los valores de los atributos privados.
- **Método operator `<<`:** Imprime la información de la persona en la consola, sobre carga del operador `<<` que se emplea en `cout <<`.

#### Script de `main.cpp`

```cpp
#include <iostream>  // Incluye la librería iostream para la entrada y salida estándar
#include "persona.h" // Incluye el archivo de cabecera persona.h

int main() {
    // Crear un objeto Persona usando el constructor
    Persona p1("Juan", 25);

    // Imprimir el objeto Persona usando el operador sobrecargado <<
    std::cout << p1 << std::endl;

    // Cambiar los atributos usando los métodos setter
    p1.setNombre("Carlos");
    p1.setEdad(30);

    // Imprimir el objeto Persona nuevamente usando el operador sobrecargado <<
    std::cout << p1 << std::endl;

    return 0;  // Indica que el programa terminó correctamente
}
```

**`main.cpp`:**

- **Inclusión de `persona.h`:** Permite usar la clase `Persona` definida en ese archivo.
- **Función `main`:** Crea un **objeto** `persona1` de la clase `Persona` y utiliza sus métodos para mostrar información y obtener los atributos.

#### Proceso de compilación y ejecución

```cpp
se compila la objeto Persona (persona.h y persona.cpp)
g++ -c persona.cpp
se genera el archivo de objeto para enlazar persona.o
g++ -o programa main.cpp persona.o
y para ejecutar
./programa.exe
```

---

## Nodo

Un **nodo** es un objeto que sirve como un contenedor para un dato y que al contar con varios **nodos** podamos utilizar una **estructura de datos** adecuada para almacenarlos y hacer una tarea determinada.

### Ejemplo 2. Clase nodo para almacenar una persona

El objeto que ilustramos [arriba](#ejemplo-1-data-dummy-de-una-persona-hecha-a-mano), que para el ejemplo se llama Persona, lo adjuntamos en una clase Node, que nos permitirá separar la información de la estructura.

<img src="/EDBlog/assets/0004_nodo_persona.png" alt="img: nodo persona">

#### Script de `node.h`:

```cpp
#ifndef NODE_H
#define NODE_H

#include "persona.h"

class Node {
private:
    Persona data; // Objeto Persona almacenado en el nodo
    
public:
    // Constructor que inicializa el nodo con un objeto Persona
    Node(const Persona &data);

    // Método getter para obtener el objeto Persona almacenado
    Persona getData() const;

    // Método setter para modificar el objeto Persona almacenado
    void setData(const Persona &data);

};

#endif // NODE_H
```

#### Script de `node.cpp`:

```cpp
#include "node.h"

// Constructor de Node que inicializa el nodo con un objeto Persona
Node::Node(const Persona &data) : data(data) {}

// Método getter para obtener el objeto Persona almacenado en el nodo
Persona Node::getData() const {
    return data;
}

// Método setter para modificar el objeto Persona almacenado en el nodo
void Node::setData(const Persona &data) {
    this->data = data;
}
```

#### Script de `main.cpp` ahora usando el objeto Nodo

```cpp
#include <iostream>  // Incluye la librería iostream para la entrada y salida estándar
#include "persona.h" // Incluye el archivo de cabecera persona.h
#include "node.h"    // Incluye el archivo de cabecera node.h

int main() {
    // Crear un objeto Persona usando el constructor
    Persona p1("Juan", 25);

    // Crear un nodo que contiene el objeto Persona
    Node node1(p1);

    // Imprimir los datos del nodo usando el operador sobrecargado <<
    std::cout << "Nodo 1 data: " << node1.getData() << std::endl;

    // Cambiar los atributos de Persona usando los métodos setter
    p1.setNombre("Carlos");
    p1.setEdad(30);
    node1.setData(p1);

    // Imprimir los datos del nodo nuevamente usando el operador sobrecargado <<
    std::cout << "Nodo 1 data despues de cambios: " << node1.getData() <<    
                 std::endl;

    return 0;  // Indica que el programa terminó correctamente
}
```

#### Proceso de compilación y ejecución

```cpp
Compilar
g++ -c persona.cpp
g++ -c node.cpp
g++ -o demostracion main.cpp persona.o node.o

Ejecutar
.\demostracion
```

---

**¡Gracias por leer este post!**