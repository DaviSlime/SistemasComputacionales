# Bitácora de aprendizaje de la unidad 4: estructuras de datos


## Actividad 1

**ofApp.h:**
```
#pragma once

#include "ofMain.h"

class Node {
public:
    float x, y;
    Node* next;

    Node(float _x, float _y) {
        x = _x;
        y = _y;
        next = nullptr;
    }

    ~Node() {
        // Destructor para Node (si hay recursos adicionales)
    }
};

class LinkedList {
public:
    Node* head;
    Node* tail;
    int size;

    LinkedList() {
        head = new Node(ofGetWidth() / 2, ofGetHeight() / 2);
        tail = head;
        size = 1;
    }

    ~LinkedList() {
        clear();
    }

    void clear() {
        // Liberar toda la memoria de los nodos
        Node* current = head;
        while (current != nullptr) {
            Node* nextNode = current->next;
            delete current;
            current = nextNode;
        }
        head = nullptr;
        tail = nullptr;
        size = 0;
    }

    void addNode(float x, float y) {
        Node* newNode = new Node(x, y);
        if (tail != nullptr) {
            tail->next = newNode;
            tail = newNode;
        }
        else {
            // Si la lista estaba vacía, inicializa head y tail con el nuevo nodo
            head = tail = newNode;
        }
        size++;
    }

    void update(float x, float y) {
        Node* current = head;
        float prevX = x;
        float prevY = y;

        while (current != nullptr) {
            float tempX = current->x;
            float tempY = current->y;
            current->x = prevX;
            current->y = prevY;
            prevX = tempX;
            prevY = tempY;
            current = current->next;
        }
    }

    void display() {
        Node* current = head;
        while (current != nullptr) {
            ofDrawCircle(current->x, current->y, 10);
            current = current->next;
        }
    }
};

class ofApp : public ofBaseApp {

public:
    LinkedList snake;

    void setup();
    void update();
    void draw();
    void keyPressed(int key);  // Nueva función para manejar el teclado
};
```

**ofApp.cpp**

```
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    // Añadir nodos a la serpiente
    for (int i = 0; i < 10; i++) {
        snake.addNode(ofGetWidth() / 2, ofGetHeight() / 2);
    }
}

//--------------------------------------------------------------
void ofApp::update() {
    // Actualizar la posición de la serpiente
    snake.update(ofGetMouseX(), ofGetMouseY());
}

//--------------------------------------------------------------
void ofApp::draw() {
    ofBackground(220);
    // Dibujar la serpiente
    snake.display();
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'c') {
        snake.clear();  // Limpiar explícitamente la lista cuando se presiona la tecla 'c'
    }
}
```

**Entendiendo la aplicación**

Primero, el código presenta una implementación básica de una lista enlazada en C++ utilizando OpenFrameworks. La lista enlazada almacena nodos que representan puntos en la pantalla, formando una "serpiente" que sigue el mouse. 

1. **Clase `Node`**: Define los puntos con coordenadas `(x, y)` y un puntero al siguiente nodo.
2. **Clase `LinkedList`**: Maneja los nodos, permitiendo añadir nuevos nodos, actualizar posiciones y mostrar los nodos en la pantalla.
3. **Método `clear()`**: Libera la memoria de todos los nodos al eliminar la lista.
4. **Clase `ofApp`**: Controla la configuración y el flujo de la aplicación, gestionando la entrada del usuario y actualizando la visualización.

**Evaluaciones formativas**


1. **¿Qué es una lista enlazada y cómo se diferencia de un arreglo?**
   - Las listas enlazadas almacenan elementos como nodos que contienen un puntero al siguiente nodo, mientras que los arreglos almacenan elementos de manera contigua en la memoria. Esto permite que las listas enlazadas crezcan y se reduzcan dinámicamente sin necesidad de reasignar memoria.

2. **¿Cómo se vinculan los nodos entre sí?**
   - Los nodos se vinculan a través del puntero `next`, que apunta al siguiente nodo en la secuencia. Este es un enfoque común en las listas enlazadas.

3. **¿Cómo se gestiona la memoria en una lista enlazada?**
   - La memoria se gestiona utilizando `new` para crear nodos y `delete` para liberarlos cuando ya no son necesarios. El destructor de la lista se asegura de liberar todos los nodos al destruirse la lista.

4. **Ventajas sobre un arreglo para insertar o eliminar elementos en posiciones intermedias:**
   - En una lista enlazada, se pueden insertar o eliminar nodos sin mover otros elementos, lo que puede ser más eficiente en comparación con un arreglo, donde es necesario desplazar elementos.

5. **¿Cómo se evita fugas de memoria?**
   - El destructor de la clase `LinkedList` llama al método `clear()`, que elimina todos los nodos y libera la memoria ocupada.

6. **¿Qué sucede en la memoria al invocar `clear()`?**
   - `clear()` itera sobre la lista, eliminando cada nodo y liberando su memoria. Al final, se asegura de que `head`, `tail` y `size` estén en un estado consistente.

7. **Estructura en memoria al agregar un nodo:**
   - Cuando se agrega un nuevo nodo, se asigna memoria para el nuevo nodo con `new`, y se actualiza el puntero `next` del nodo anterior para que apunte al nuevo nodo. Esto no afecta el rendimiento de la lista enlazada de manera significativa, ya que la inserción al final puede ser O(1) si se mantiene un puntero a `tail`.

8. **Situación donde una lista enlazada es ventajosa:**
   - En aplicaciones donde hay muchas inserciones y eliminaciones, como en un sistema de gestión de tareas donde se añaden y eliminan tareas frecuentemente.

9. **Diseño de una estructura de datos personalizada:**
   - Consideraría la eficiencia en términos de espacio y tiempo, asegurándome de liberar la memoria adecuadamente y posiblemente implementando un sistema de referencia para evitar la eliminación prematura de nodos.

10. **Diferencias en gestión de memoria entre C++ y C#:**
    - C++ requiere gestión manual de memoria (new y delete), lo que puede llevar a errores si se olvida liberar memoria. C# utiliza recolección de basura, lo que simplifica el manejo de memoria pero puede tener un costo en términos de rendimiento en algunos casos.

11. **Optimización de arte generativo:**
    - Mantendría un registro de los nodos activos, implementaría un sistema para reutilizar nodos en lugar de crear nuevos constantemente, y aseguraría que cada nodo se libere cuando ya no sea necesario.

### Pruebas

Para probar el programa, se considera lo siguiente:

- **Verificar que se añadan nodos correctamente**: Imprime el tamaño de la lista después de añadir nodos.
- **Probar la función `update()`**: Verifica que la posición de los nodos se actualice correctamente al mover el mouse.
- **Verificar `clear()`**: Añadir nodos, invocar `clear()` y luego comprobar que la lista esté vacía.


## Actividad 2

**Experimentar con pilas y colas en un contexto de arte generativo.**

El código para la pila es este:

**ofApp.h:**


``` c++
#pragma once

#include "ofMain.h"

class Node {
public:
    ofVec2f position;
    Node* next;

    Node(float x, float y) {
        position.set(x, y);
        next = nullptr;
    }
};

class Stack {
public:
    Node* top;

    Stack() {
        top = nullptr;
    }

    ~Stack() {
        clear();
    }

    void push(float x, float y) {
        Node* newNode = new Node(x, y);
        newNode->next = top;
        top = newNode;
    }

    void pop() {
        if (top != nullptr) {
            Node* temp = top;
            top = top->next;
            delete temp;  // Liberar memoria del nodo eliminado
        }
    }

    void clear() {
        while (top != nullptr) {
            pop();
        }
    }

    void display() {
        Node* current = top;
        while (current != nullptr) {
            ofDrawCircle(current->position.x, current->position.y, 20);
            current = current->next;
        }
    }
};

class ofApp : public ofBaseApp {

public:
    Stack circleStack;

    void setup();
    void update();
    void draw();
    void keyPressed(int key);
}
```

**ofApp.cpp:**

``` c++
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofSetBackgroundColor(220);
}

//--------------------------------------------------------------
void ofApp::update() {

}

//--------------------------------------------------------------
void ofApp::draw() {
    // Dibujar todos los círculos en la pila
    circleStack.display();
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'a') { // Apilar un nuevo círculo
        circleStack.push(ofGetMouseX(), ofGetMouseY());
    }
    else if (key == 'd') { // Desapilar el último círculo
        circleStack.pop();
    }
}
```

El código para la cola es este:

**ofApp.h:**

``` c++
#pragma once

#include "ofMain.h"

class Node {
public:
    ofVec2f position;
    Node* next;

    Node(float x, float y) {
        position.set(x, y);
        next = nullptr;
    }
};

class Queue {
public:
    Node* front;
    Node* rear;

    Queue() {
        front = rear = nullptr;
    }

    ~Queue() {
        clear();
    }

    void enqueue(float x, float y) {
        Node* newNode = new Node(x, y);
        if (rear == nullptr) {
            front = rear = newNode;
        }
        else {
            rear->next = newNode;
            rear = newNode;
        }
    }

    void dequeue() {
        if (front != nullptr) {
            Node* temp = front;
            front = front->next;
            if (front == nullptr) {
                rear = nullptr;
            }
            delete temp;  // Liberar memoria del nodo eliminado
        }
    }

    void clear() {
        while (front != nullptr) {
            dequeue();
        }
    }

    void display() {
        Node* current = front;
        while (current != nullptr) {
            ofDrawCircle(current->position.x, current->position.y, 20);
            current = current->next;
        }
    }
};

class ofApp : public ofBaseApp {

public:
    Queue circleQueue;

    void setup();
    void update();
    void draw();
    void keyPressed(int key);
}
```

**ofApp.cpp:**

``` c++
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofSetBackgroundColor(220);
}

//--------------------------------------------------------------
void ofApp::update() {

}

//--------------------------------------------------------------
void ofApp::draw() {
    // Dibujar todos los círculos en la cola
    circleQueue.display();
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'a') { // Encolar un nuevo círculo
        circleQueue.enqueue(ofGetMouseX(), ofGetMouseY());
    }
    else if (key == 'd') { // Desencolar el primer círculo
        circleQueue.dequeue();
    }
}
```

**Entendiendo la Aplicación:**

He estado explorando el programa que implementa una pila y una cola en un contexto de arte generativo utilizando C++ y openFrameworks. Aquí hay un desglose detallado de su funcionamiento:

### **1. Estructura del Programa**

El programa está dividido en dos secciones principales: una que implementa una **pila** (Stack) y otra que implementa una **cola** (Queue). Ambas utilizan una estructura de datos basada en nodos para almacenar posiciones (coordenadas x, y) de círculos que se dibujan en la ventana.

### **2. Clases y Objetos**

- **Node**: Esta clase representa un nodo que contiene:
  - `ofVec2f position`: las coordenadas del círculo.
  - `Node* next`: un puntero al siguiente nodo en la estructura (para enlazar nodos).

- **Stack**: Esta clase gestiona la pila y tiene:
  - `Node* top`: un puntero al nodo superior de la pila.
  - Métodos para:
    - `push`: agregar un nuevo nodo a la pila.
    - `pop`: eliminar el nodo superior.
    - `clear`: liberar toda la memoria ocupada por la pila.
    - `display`: dibujar todos los nodos en la ventana.

- **Queue**: Esta clase gestiona la cola y tiene:
  - `Node* front`: puntero al primer nodo (frente) de la cola.
  - `Node* rear`: puntero al último nodo (final) de la cola.
  - Métodos similares a los de Stack para agregar, eliminar y mostrar nodos.

### **3. Funciones de la Clase ofApp**

La clase `ofApp` es la que controla la aplicación y contiene instancias de `Stack` y `Queue`:

- `setup()`: Inicializa la configuración, estableciendo el color de fondo.
  
- `update()`: Se deja vacío, ya que no se requiere actualizar el estado en cada fotograma.

- `draw()`: Dibuja los círculos almacenados en la pila o cola.

- `keyPressed(int key)`: Captura la entrada del teclado para apilar (`'a'`) o desapilar (`'d'`) círculos en la pila, o encolar (`'a'`) o desencolar (`'d'`) círculos en la cola.

### **4. Gestión de Memoria**


El programa maneja explícitamente la memoria:
- En el destructor de `Stack` y `Queue`, se llama a `clear()` para liberar toda la memoria ocupada por los nodos antes de destruir el objeto. Esto previene fugas de memoria.
- Los métodos `pop()` y `dequeue()` también liberan la memoria del nodo eliminado de manera adecuada.

**Experimentando con el Programa**

Al ejecutar el programa, se pueden observar los siguientes comportamientos:
- Al presionar `'a'`, se agrega un círculo en la posición del mouse, ya sea a la pila o a la cola, dependiendo de la clase activa.
- Al presionar `'d'`, se elimina un círculo de la pila o cola.
- Esto permite ver cómo se gestionan los datos y cómo se visualizan en tiempo real.



### Preguntas sobre la Estructura de Datos

1. **¿Cuál es la función del puntero `next` en la clase `Node`?**
   - El puntero `next` en la clase `Node` se utiliza para enlazar nodos entre sí, formando una lista encadenada. Permite que cada nodo apunte al siguiente, lo que es fundamental para implementar la pila y la cola.

2. **¿Cómo se diferencia el método `push` de la pila del método `enqueue` de la cola en cuanto a la manera en que manejan los nodos?**
   - El método `push` de la pila agrega un nuevo nodo en la parte superior (top), mientras que el método `enqueue` de la cola agrega un nuevo nodo al final (rear) de la estructura. Esto refleja las diferencias en las estrategias LIFO y FIFO.

#### Preguntas sobre las Clases

3. **¿Qué sucede cuando se llama al método `clear` en las clases `Stack` y `Queue`?**
   - Al llamar al método `clear`, se eliminan todos los nodos en la pila o cola. Se invoca repetidamente el método `pop` o `dequeue` hasta que no queden más nodos, liberando así toda la memoria ocupada por ellos.

4. **¿Por qué es importante liberar la memoria en el destructor de las clases `Stack` y `Queue`?**
   - Es importante liberar la memoria en el destructor para evitar fugas de memoria, que pueden ocurrir si se crean objetos dinámicamente (como los nodos) sin liberar la memoria que ocupan al finalizar su uso.

#### Preguntas sobre la Interacción del Usuario

5. **¿Qué acción ocurre al presionar la tecla `'a'` en el contexto de la pila y la cola?**
   - Al presionar la tecla `'a'`, se agrega un nuevo círculo en la posición del mouse. Si se está trabajando con la pila, se usa `push`, y si es la cola, se usa `enqueue`.

6. **¿Qué efecto tiene presionar la tecla `'d'` en la pila y en la cola?**
   - Al presionar la tecla `'d'`, se elimina el último círculo en la pila (con `pop`) o el primer círculo en la cola (con `dequeue`), dependiendo de la estructura activa.

#### Preguntas sobre el Dibujo

7. **¿Cómo se dibujan los círculos en la ventana? Describe el proceso en el método `display`.**
   - En el método `display`, se recorre la lista de nodos comenzando desde el nodo superior (en la pila) o el frente (en la cola). Para cada nodo, se utiliza `ofDrawCircle` para dibujar un círculo en las coordenadas especificadas por el nodo.

8. **¿Qué tamaño tienen los círculos que se dibujan en el método `display`?**
   - Los círculos que se dibujan tienen un radio de 20 unidades, como se especifica en la llamada a `ofDrawCircle`.

#### Preguntas sobre el Flujo del Programa

9. **¿Cuál es el propósito del método `update`, y por qué está vacío en este caso?**
   - El método `update` se utiliza para actualizar el estado de la aplicación en cada fotograma. En este caso está vacío porque no hay lógica que necesite ser actualizada continuamente; solo se manejan interacciones de entrada.

10. **¿Qué ocurre si intentas hacer `pop` o `dequeue` en una pila o cola vacía?**
    - Si se intenta hacer `pop` en una pila vacía o `dequeue` en una cola vacía, no ocurrirá ninguna acción, ya que los métodos verifican si el puntero correspondiente (`top` o `front`) es `nullptr`. Esto previene errores al intentar acceder a nodos inexistentes.


### Reflexiones sobre el stack:

#### 1. Gestión de la Memoria en un Stack Manual en C++

En una implementación manual de un stack en C++, la memoria se gestiona utilizando los operadores `new` y `delete`. Al crear un nodo con `new`, se asigna memoria dinámica en el heap. Esta memoria debe ser liberada explícitamente con `delete` cuando ya no se necesita. 

- **Rendimiento**: El uso de `new` y `delete` puede afectar el rendimiento, especialmente si se realizan muchas asignaciones y liberaciones de memoria, ya que cada operación implica un costo de gestión de memoria.
- **Seguridad**: Si no se manejan correctamente, los punteros pueden causar errores, como accesos a memoria liberada (dangling pointers) o fugas de memoria si se olvida liberar la memoria.

#### 2. Importancia de Liberar Memoria al Desapilar un Nodo

Liberar la memoria al desapilar un nodo es crucial para evitar fugas de memoria. Si se desapilan nodos sin liberar la memoria, la aplicación puede seguir consumiendo memoria sin liberarla, lo que podría llevar a un eventual agotamiento de la memoria disponible en aplicaciones de largo tiempo de ejecución. Esto es especialmente relevante en sistemas donde la memoria es un recurso limitado.

#### 3. Diferencias entre `std::stack` y una Implementación Manual

- **Abstracción**: `std::stack` ofrece una interfaz abstracta que simplifica la gestión de un stack, manejando internamente la memoria y asegurando operaciones seguras. Esto permite a los desarrolladores centrarse en la lógica de la aplicación sin preocuparse por los detalles de la implementación.
- **Control**: Una implementación manual permite un mayor control sobre la gestión de recursos y el comportamiento del stack. Esto es útil en situaciones donde se necesitan características específicas (por ejemplo, almacenamiento de datos en un orden particular).
- **Seguridad**: `std::stack` incluye medidas de seguridad y manejo de excepciones que pueden prevenir errores comunes en una implementación manual.

#### 4. Efecto de la Estructura LIFO en el Acceso y Eliminación

La estructura LIFO del stack significa que el último elemento agregado es el primero en ser eliminado. Esta característica es útil para resolver problemas donde el último estado o acción debe ser procesado primero, como en algoritmos de retroceso (backtracking), expresiones matemáticas (evaluación de expresiones), y la gestión de llamadas a funciones (stack de llamadas).

#### 5. Modificación del Stack para Tipos de Datos Complejos

Para almacenar tipos de datos más complejos en un stack, como objetos con múltiples atributos, se podría usar punteros o referencias a los objetos:

- **Gestión de Memoria**: Si se utilizan punteros, será necesario gestionar cuidadosamente la memoria de los objetos, asegurando que se liberen cuando ya no se necesiten. Se podría implementar un sistema de conteo de referencias o usar smart pointers (como `std::shared_ptr` o `std::unique_ptr`) para manejar automáticamente la memoria.
- **Impacto en la Implementación**: La implementación actual requeriría modificaciones para manejar la construcción y destrucción de estos objetos complejos. También se debe considerar cómo se copian o mueven los objetos en el stack, lo que podría requerir implementar constructores de copia y operadores de asignación adecuados.


### Reflexiones sobre la queue (cola):

#### 1. Manejo de la Memoria en una Implementación Manual de una Queue

En una implementación manual de una queue en C++, la memoria se gestiona usando `new` y `delete` para crear y destruir nodos. Cuando se encola un nuevo elemento, se crea un nuevo nodo y se ajustan los punteros `front` y `rear` adecuadamente.

- **Gestión de Nodos**: Al desencolar un elemento, se debe liberar la memoria del nodo eliminado. Esto es crucial para evitar fugas de memoria.
- **Eficiencia y Seguridad**: Las operaciones de encolado y desencolado deben ser eficientes (O(1) en promedio) para que la queue funcione bien. Si se gestionan mal los nodos (por ejemplo, no liberar adecuadamente la memoria), se pueden generar errores de acceso a memoria y fugas.

#### 2. Desafíos en la Implementación de una Queue vs. un Stack

- **Gestión de Punteros**: En una queue, se gestionan dos punteros: `front` y `rear`. Esto complica un poco más la implementación en comparación con una pila que solo tiene un puntero (`top`).
- **Proceso de Encolado y Desencolado**: En el caso de la queue, al encolar un elemento, se actualiza el puntero `rear`, y al desencolar, se actualiza `front`. Si no se gestionan adecuadamente, se pueden perder referencias a nodos, lo que lleva a fugas de memoria o errores en el acceso.

#### 3. Estructura FIFO y su Uso en Problemas

La estructura FIFO (First In, First Out) de una queue es fundamental en situaciones donde el orden de procesamiento es crítico. 

- **Ejemplos de Uso**: 
  - En sistemas de colas de espera, como en líneas de atención al cliente o procesamiento de tareas, donde el primero en llegar debe ser el primero en ser atendido.
  - En la planificación de tareas en sistemas operativos, donde los procesos deben ser gestionados en el orden en que llegaron.

#### 4. Implementación de una Queue Circular

Una queue circular utiliza una estructura que conecta el último nodo de vuelta al primero, lo que permite aprovechar mejor el espacio en memoria.

- **Ventajas**: 
  - Reduce la necesidad de mover nodos y permite reutilizar espacios vacíos sin necesidad de liberar y volver a crear nodos.
  - Mejora la eficiencia al minimizar el desperdicio de memoria.
  
- **Cambios en la Implementación**: 
  - Se requeriría lógica adicional para gestionar el envolvimiento (wrap-around) cuando `front` y `rear` alcanzan el final de la estructura.
  - Necesitarías llevar un control del tamaño actual para evitar desbordamientos.

#### 5. Problemas por una Gestión Incorrecta de los Punteros `front` y `rear`

Si no se gestionan correctamente los punteros `front` y `rear`, pueden surgir varios problemas:

- **Pérdida de Referencias**: Si se elimina un nodo sin actualizar correctamente `front`, podrías perder el acceso a la queue.
- **Errores de Acceso**: Intentar desencolar cuando `front` apunta a `nullptr` o a un nodo no válido podría causar errores de ejecución.
- **Fugas de Memoria**: Si se olvida liberar un nodo al desencolar, se produce una fuga de memoria.

#### Prevención de Problemas

Para evitar estos problemas, se pueden implementar las siguientes estrategias:

- **Verificaciones de Estado**: Implementar comprobaciones para asegurarse de que `front` y `rear` están correctamente actualizados después de cada operación.
- **Pruebas Rigurosas**: Realizar pruebas exhaustivas para detectar casos de borde, como desencolar de una queue vacía.
- **Uso de Smart Pointers**: Considerar el uso de smart pointers (como `std::shared_ptr` o `std::unique_ptr`) para gestionar automáticamente la memoria y reducir el riesgo de fugas.

## Reto

Crea una obra de arte generativo dinámica (con gestión de memoria). Utilizando los conceptos de arreglos, listas enlazadas, pilas y colas, crea una obra de arte generativo dinámica. Asegúrate de gestionar el ciclo de vida de todos los objetos creados dinámicamente.

**Idea de la obra**

 crear un sistema en el que:

- Cada vez que se presiona el botón izquierdo del mouse, se genera una nueva partícula que se mueve por la pantalla rebotando en los bordes.
- Cada partícula tiene un color, una velocidad y una posición aleatoria.
- Las partículas se almacenan en una lista enlazada que representa el historial de partículas creadas, y se gestiona su ciclo de vida. Además, utilizamos una pila - para manejar las partículas eliminadas, permitiendo hacer un "deshacer" si se desea eliminar la última partícula creada.
- La interacción será a través de los clics del mouse: el clic izquierdo genera una nueva partícula, mientras que el clic derecho elimina la última partícula creada.

**Estructura del Código**

1. **Usaremos**:
   - **Lista enlazada** para almacenar las partículas.
   - **Pila** para almacenar las partículas que se eliminarán temporalmente, permitiendo un "deshacer" de las eliminaciones.

2. **Interactividad**:
   - Añadiremos una tecla para cambiar el color de todas las partículas y otra para deshacer la última eliminación.

3. **Gestión de memoria**:
   - Usaremos `std::unique_ptr` y manejaremos correctamente la pila para liberar la memoria de las partículas eliminadas.

**Código Modificado**

**Particle.h**


``` cpp
#pragma once
#include "ofMain.h"

class Particle {
public:
    ofVec2f position;
    ofVec2f velocity;
    ofColor color;

    Particle(ofVec2f pos, ofVec2f vel, ofColor col)
        : position(pos), velocity(vel), color(col) {}

    void update() {
        position += velocity;

        // Rebote en los bordes de la pantalla
        if (position.x <= 0 || position.x >= ofGetWidth()) {
            velocity.x *= -1;
        }
        if (position.y <= 0 || position.y >= ofGetHeight()) {
            velocity.y *= -1;
        }
    }

    void draw() {
        ofSetColor(color);
        ofDrawCircle(position, 10); // Dibujamos la partícula como un círculo
    }
};


```

**ofApp.h**

```cpp
#pragma once
#include "ofMain.h"
#include "Particle.h"
#include <list>
#include <memory>
#include <stack> // Para usar pila

class ofApp : public ofBaseApp {
public:
    void setup();
    void update();
    void draw();
    void mousePressed(int x, int y, int button);
    void keyPressed(int key); // Añadir método para gestionar teclas
    void exit();

private:
    std::list<std::unique_ptr<Particle>> particles;   // Lista enlazada de partículas activas
    std::stack<std::unique_ptr<Particle>> removedParticles; // Pila para deshacer eliminaciones
};
```

**ofApp.cpp**

```cpp
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofBackground(0); // Fondo negro
}

//--------------------------------------------------------------
void ofApp::update() {
    for (auto& particle : particles) {
        particle->update(); // Actualizar cada partícula
    }
}

//--------------------------------------------------------------
void ofApp::draw() {
    for (auto& particle : particles) {
        particle->draw(); // Dibujar cada partícula
    }
}

//--------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button) {
    if (button == OF_MOUSE_BUTTON_LEFT) {
        // Crear nueva partícula al hacer clic izquierdo
        ofVec2f position(x, y);
        ofVec2f velocity(ofRandom(-5, 5), ofRandom(-5, 5));
        ofColor color(ofRandom(255), ofRandom(255), ofRandom(255));
        particles.emplace_back(std::make_unique<Particle>(position, velocity, color));
    }
    else if (button == OF_MOUSE_BUTTON_RIGHT && !particles.empty()) {
        // Eliminar la última partícula con clic derecho
        removedParticles.push(std::move(particles.back())); // Guardar en la pila
        particles.pop_back(); // Quitar la última partícula
    }
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'c') { // Cambiar color de todas las partículas
        for (auto& particle : particles) {
            particle->color = ofColor(ofRandom(255), ofRandom(255), ofRandom(255));
        }
    }
    else if (key == 'u') { // Deshacer la última eliminación
        if (!removedParticles.empty()) {
            particles.emplace_back(std::move(removedParticles.top())); // Recuperar la partícula
            removedParticles.pop(); // Eliminar de la pila
        }
    }
}

//--------------------------------------------------------------
void ofApp::exit() {
    // No es necesario liberar memoria manualmente, std::unique_ptr lo hace
}
```

1. **Uso de una Pila**:
   - Se añade una `std::stack<std::unique_ptr<Particle>> removedParticles` para almacenar las partículas eliminadas. Esto permite recuperar una partícula eliminada si el usuario lo desea.

2. **Interactividad**:
   - Se añade un método `keyPressed(int key)`, que gestiona la pulsación de teclas.
     - Si se presiona la tecla `'c'`, cambia el color de todas las partículas a colores aleatorios.
     - Si se presiona la tecla `'u'`, recupera la última partícula eliminada de la pila.

3. **Gestión de Memoria**:
   - Cuando se elimina una partícula, se mueve a la pila usando `std::move`, lo que asegura que la memoria se maneje correctamente. Cuando se recupera de la pila, también se utiliza `std::move` para transferir la propiedad de nuevo a la lista de partículas.

Este código modificado combina una lista enlazada y una pila para gestionar las partículas, añade interactividad mediante la pulsación de teclas y asegura una gestión de memoria eficiente usando `std::unique_ptr`. Con estos cambios, la obra generativa ahora es más interactiva y flexible.


### RAE1: Construcción de Aplicaciones Interactivas

**Requisitos Funcionales y No Funcionales**
1. **Funcionales**:
   - Crear partículas en respuesta a clics del mouse.
   - Eliminar partículas y permitir la recuperación de partículas eliminadas.
   - Cambiar el color de las partículas mediante una tecla.

2. **No Funcionales**:
   - Rendimiento: La aplicación debe ser fluida incluso con muchas partículas.
   - Usabilidad: La interfaz debe ser fácil de usar.

**Capturas de Pantalla**
Para documentar tu trabajo, toma capturas de pantalla que muestren diferentes aspectos de la aplicación:

1. **Captura 1**: Interacción al hacer clic izquierdo para crear partículas.
   

https://github.com/user-attachments/assets/618bf0ed-4312-469e-9f69-f4acc64b0c9e


  
2. **Captura 2**: Interacción al hacer clic derecho para eliminar una partícula.
   

https://github.com/user-attachments/assets/71d982b1-2c0b-42fd-ad8b-f54dc6506876



3. **Captura 3**: Uso de la tecla para cambiar colores.

   
https://github.com/user-attachments/assets/4c8aa12f-5051-428f-b850-3c9c8690fc1a



4. **Captura 4**: Recuperación de una partícula eliminada.
   

https://github.com/user-attachments/assets/c259b0c3-1601-4f34-9188-6f1a84d4e07f



5. **Captura 5**: Performance con muchas partículas.
   

https://github.com/user-attachments/assets/3cd3e615-104c-440d-a61f-2e2161e992eb



### RAE2: Pruebas de Software

**Pruebas de Requisitos Individuales**
1. **Creación de Partículas**:
   - **Prueba**: Clic izquierdo en diferentes partes de la pantalla y verificar que se añadan partículas en las posiciones correctas.
   - **Captura**:

https://github.com/user-attachments/assets/0c5f6978-5fc7-4103-9e9e-8e5a481167fc



2. **Eliminación de Partículas**:
   - **Prueba**: Clic derecho sobre una partícula y verificar si se elimina la ultima particula y no la que selecioné. Además que se elimine de la pantalla y que se añada a la pila.
   - **Captura**:

https://github.com/user-attachments/assets/fb31cf0f-5011-413b-856d-163f1c295e44



3. **Cambio de Color**:
   - **Prueba**: Presiona la tecla 'c' y verifica que todas las partículas cambien de color.
   - **Captura**:

https://github.com/user-attachments/assets/f1bda118-8bcc-49e8-a9d4-7bde93e7b65e



4. **Recuperación de Partículas**:
   - **Prueba**: Clic derecho para eliminar una partícula, luego presionar 'u' para recuperarla y verifica que vuelva a aparecer.
   - **Captura**:

https://github.com/user-attachments/assets/d9bf60d1-be39-4ef4-80b9-1256145feaf7



**Pruebas del Sistema Completo**

- **Prueba de Integración**: Todas las interacciones funcionan correctamente en conjunto. Crear, eliminar y recuperar partículas mientras se cambian los colores.
- **Captura**:

https://github.com/user-attachments/assets/53d4e687-5356-4a13-96a2-ef4c4ced60e7




