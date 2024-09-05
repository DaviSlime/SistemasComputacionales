# Bitácora de aprendizaje de la unidad 3: lenguaje de alto nivel

## Actividad 2 Modifica el archivo ofApp.h así:

``` c++
#pragma once

#include "ofMain.h"

class ofApp : public ofBaseApp{

    public:
        void setup();
        void update();
        void draw();

        void mouseMoved(int x, int y );
        void mousePressed(int x, int y, int button);

    private:

        vector<ofVec2f> particles;
        ofColor particleColor;

};

```

### Ahora modifica el archivo ofApp.cpp así:

``` c++
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup(){
    ofBackground(0);
    particleColor = ofColor::white;
}

//--------------------------------------------------------------
void ofApp::update(){

}

//--------------------------------------------------------------
void ofApp::draw(){
    for(auto &pos: particles){
        ofSetColor(particleColor);
        ofDrawCircle(pos.x, pos.y, 50);
    }
}

//--------------------------------------------------------------
void ofApp::mouseMoved(int x, int y ){
    particles.push_back(ofVec2f(x, y));
    if (particles.size() > 100) {
        particles.erase(particles.begin());
    }
}

//--------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button){
    particleColor = ofColor(ofRandom(255), ofRandom(255), ofRandom(255));
}

```

### Análisis

1. **¿Qué fue lo que incluimos en el archivo .h?**

   El archivo `.h` que se incluye aquí es `"ofApp.h"`. Este archivo de encabezado generalmente contiene la declaración de la clase `ofApp` y sus métodos. Es donde se definen las variables miembro y las declaraciones de funciones que se implementan en el archivo `.cpp` (en este caso, `ofApp.cpp`).

2. **¿Cómo funciona la aplicación?**

   La aplicación muestra un fondo negro y dibuja círculos blancos en las posiciones donde se mueve el ratón. El color de los círculos cambia aleatoriamente cuando se hace clic con el ratón. Los círculos se dibujan con un radio fijo de 50 píxeles. Solo se mantienen en pantalla los últimos 100 puntos donde se ha movido el ratón.

3. **¿Qué hace la función `mouseMoved`?**

   La función `mouseMoved` se llama cada vez que el ratón se mueve. Agrega la posición actual del ratón (en forma de `ofVec2f`) al vector `particles`. Si el número de partículas supera los 100, elimina la partícula más antigua (la que está al principio del vector). Esto asegura que solo se mantengan las últimas 100 posiciones del ratón.

4. **¿Qué hace la función `mousePressed`?**

   La función `mousePressed` se llama cada vez que se presiona un botón del ratón. Cambia el color de las partículas (`particleColor`) a un color aleatorio generado usando `ofRandom(255)` para cada componente de color (rojo, verde y azul). Esto hace que el color de los círculos dibujados cambie de forma aleatoria cada vez que se presiona el ratón.

5. **¿Qué hace la función `setup`?**

   La función `setup` se llama al inicio para configurar el entorno de la aplicación. Aquí se establece el fondo de la ventana a negro (`ofBackground(0)`) y se inicializa el color de las partículas (`particleColor`) a blanco (`ofColor::white`).

6. **¿Qué hace la función `update`?**

   La función `update` se llama en cada iteración del loop de actualización de OpenFrameworks. En este caso, la función está vacía, lo que significa que no realiza ninguna acción en cada frame.

7. **¿Qué hace la función `draw`?**

   La función `draw` se llama en cada iteración del loop de dibujo de OpenFrameworks. Dibuja un círculo en cada posición almacenada en el vector `particles`. El color del círculo se establece con `ofSetColor(particleColor)`, y se dibuja un círculo con un radio de 50 píxeles en cada posición (`pos.x`, `pos.y`).


## Actividad 3: Analiza la aplicación anterior. ¿Qué hace cada función? ¿Qué hace cada línea de código?, Realiza un experimento con la aplicación anterior. Modifica alguna parte de su código.

### Linea 1

``` c++
#include "ofApp.h"
```
Incluye el archivo de encabezado ofApp.h, donde se declaran las funciones y variables de la clase ofApp.

### Linea 2

``` c++
void ofApp::setup(){
    ofBackground(0);
    particleColor = ofColor::white;
}

```

* ofApp::setup() es un método que se llama una vez al inicio de la aplicación para realizar configuraciones iniciales.
  
* ofBackground(0); establece el color de fondo de la ventana a negro. El parámetro 0 representa el color negro en la escala de grises (0 es negro, 255 es blanco).
  
* particleColor = ofColor::white; inicializa el color de las partículas a blanco.

### Linea 3

``` c++
void ofApp::update(){
}

```
ofApp::update() es un método que se llama en cada frame para actualizar el estado de la aplicación. En este caso, está vacío, lo que significa que no se realizan actualizaciones durante el ciclo de actualización.

### Linea 4

``` c++
void ofApp::draw(){
    for(auto &pos: particles){
        ofSetColor(particleColor);
        ofDrawCircle(pos.x, pos.y, 50);
    }
}

```

* ofApp::draw() es un método que se llama en cada frame para dibujar en la ventana.

* for(auto &pos: particles) itera sobre el vector particles, que contiene las posiciones de las partículas.

* ofSetColor(particleColor); establece el color de dibujo a particleColor.

* ofDrawCircle(pos.x, pos.y, 50); dibuja un círculo en la posición (pos.x, pos.y) con un radio de 50 píxeles.


### Linea 5

``` c++
void ofApp::mouseMoved(int x, int y ){
    particles.push_back(ofVec2f(x, y));
    if (particles.size() > 100) {
        particles.erase(particles.begin());
    }
}

```

* ofApp::mouseMoved(int x, int y) se llama cada vez que el ratón se mueve.

* particles.push_back(ofVec2f(x, y)); agrega la posición actual del ratón al vector particles.

* if (particles.size() > 100) { particles.erase(particles.begin()); } asegura que solo se mantengan las últimas 100 posiciones del ratón. Si hay más de 100 posiciones, elimina la más antigua.

### Linea 6

``` c++
void ofApp::mousePressed(int x, int y, int button){
    particleColor = ofColor(ofRandom(255), ofRandom(255), ofRandom(255));
}

```

* ofApp::mousePressed(int x, int y, int button) se llama cada vez que se presiona un botón del ratón.

* particleColor = ofColor(ofRandom(255), ofRandom(255), ofRandom(255)); cambia el color de las partículas a un color aleatorio. ofRandom(255) genera un valor aleatorio entre 0 y 255 para cada componente de color (rojo, verde, azul).


### MODIFICACIÓN DEL CODIGO

En el directorio pfApp.h ponemos esto:

``` c++
#pragma once

#include "ofMain.h"

class ofApp : public ofBaseApp{

    public:
        void setup();
        void update();
        void draw();

        void mouseMoved(int x, int y );
        void mousePressed(int x, int y, int button);

    private:

        vector<ofVec2f> particles;
        ofColor particleColor;

};
```


Colocamos en ofApp.cpp lo siguiente
``` c++
#include "ofApp.h"

// Variables para guardar la última posición del ratón
ofVec2f lastMousePos;

//--------------------------------------------------------------
void ofApp::setup(){
    ofBackground(0);
    particleColor = ofColor::white;
    lastMousePos = ofVec2f(0, 0);  // Inicializamos la última posición del ratón
}

//--------------------------------------------------------------
void ofApp::update(){
    // No se realiza ninguna actualización aquí
}

//--------------------------------------------------------------
void ofApp::draw(){
    for(auto &pos: particles){
        ofSetColor(particleColor);
        
        // Calculamos la distancia desde la última posición del ratón
        float distance = pos.distance(lastMousePos);
        
        // El tamaño del círculo se basa en la distancia
        float radius = ofMap(distance, 0, 100, 10, 100, true);
        
        // Dibujamos el círculo con el radio calculado
        ofDrawCircle(pos.x, pos.y, radius);
    }
}

//--------------------------------------------------------------
void ofApp::mouseMoved(int x, int y ){
    // Guardamos la última posición antes de actualizar
    lastMousePos = ofVec2f(x, y);
    
    particles.push_back(ofVec2f(x, y));
    if (particles.size() > 100) {
        particles.erase(particles.begin());
    }
}

//--------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button){
    particleColor = ofColor(ofRandom(255), ofRandom(255), ofRandom(255));
}

```

### Que hace el codigo?

Modifiqué el código para cambiar el tamaño de los círculos según la velocidad del movimiento del ratón. Esto hará que los círculos sean más grandes cuando se mueva el ratón más rápido y más pequeños cuando se mueva lentamente. Para hacer esto, necesitaremos guardar la última posición del ratón y calcular la velocidad.

### Descripción del Cambio

### Añadí

* ofVec2f lastMousePos; para almacenar la última posición del ratón.

* En setup(), inicializamos lastMousePos a (0, 0).

## Modificado en draw():

* Calculamos la distancia entre la posición actual del ratón y la última posición con float distance = pos.distance(lastMousePos);.

* Usamos ofMap(distance, 0, 100, 10, 100, true); para mapear la distancia a un rango de tamaños de radio de 10 a 100 píxeles.

* Dibujamos el círculo con el radio calculado basado en la distancia del movimiento.

### Modificado en mouseMoved():

* Actualizamos lastMousePos a la nueva posición antes de agregarla al vector de partículas.

## Actividad 5: El siguiente ejemplo se supone (en la actividad que sigue vas a corregir un error) que te permite seleccionar una espera y moverla con el mouse.

### Modifica el archivo ofApp.h de la siguiente manera:

``` c++
#pragma once

#include "ofMain.h"


class Sphere {
public:
    Sphere(float x, float y, float radius);
    void draw();
    void update(float x, float y);
    float getX();
    float getY();
    float getRadius();

private:
    float x, y;
    float radius;
    ofColor color;
};

class ofApp : public ofBaseApp{

    public:
        void setup();
        void update();
        void draw();

        void mouseMoved(int x, int y );
        void mousePressed(int x, int y, int button);

    private:

        vector<Sphere*> spheres;
        Sphere* selectedSphere;
};
```

### Y el archivo ofApp.cpp así:

``` c++
#include "ofApp.h"

Sphere::Sphere(float x, float y, float radius) : x(x), y(y), radius(radius) {
    color = ofColor(ofRandom(255), ofRandom(255), ofRandom(255));
}

void Sphere::draw() {
    ofSetColor(color);
    ofDrawCircle(x, y, radius);
}

void Sphere::update(float x, float y) {
    this->x = x;
    this->y = y;
}

float Sphere::getRadius() {
    return radius;
}

float Sphere::getX() {
    return x;
}

float Sphere::getY() {
    return y;
}

//--------------------------------------------------------------
void ofApp::setup(){
    ofBackground(0);

    for (int i = 0; i < 5; i++) {
        float x = ofRandomWidth();
        float y = ofRandomHeight();
        float radius = ofRandom(20, 50);
        spheres.push_back(new Sphere(x, y, radius));
    }
    selectedSphere = nullptr;

}

//--------------------------------------------------------------
void ofApp::update(){
    if (selectedSphere != nullptr) {
        selectedSphere->update(ofGetMouseX(), ofGetMouseY());
    }
}

//--------------------------------------------------------------
void ofApp::draw(){
    for (auto sphere : spheres) {
        sphere->draw();
    }
}


//--------------------------------------------------------------
void ofApp::mouseMoved(int x, int y ){

}

//--------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button){

    if(button == OF_MOUSE_BUTTON_LEFT){
        for (auto sphere : spheres) {
            float distance = ofDist(x, y, sphere->getX(), sphere->getY());
            if (distance < sphere->getRadius()) {

                selectedSphere = sphere;
                break;
            }
        }
    }
}
```

### ¿Cuál es la definición de puntero?

Un puntero en programación es una variable que almacena la dirección de memoria de otra variable. En lugar de almacenar directamente un valor, un puntero almacena la ubicación en la memoria donde se encuentra el valor. Los punteros permiten acceder y manipular la información en esa ubicación de memoria.

### ¿Dónde Está el Puntero?

En ofApp.h:

``` c++
class ofApp : public ofBaseApp {
    // ...
private:
    vector<Sphere*> spheres;
    Sphere* selectedSphere;
};

```

* vector<Sphere*> spheres; es un vector de punteros a objetos de la clase Sphere. Cada elemento en este vector es un puntero que apunta a una instancia de Sphere.
  
* Sphere* selectedSphere; es un puntero a un objeto de la clase Sphere. Este puntero se usa para hacer referencia a la esfera que actualmente está seleccionada.

### ¿Cómo se Inicializa el Puntero?

En el archivo ofApp.cpp, el puntero selectedSphere se inicializa:

``` c++
selectedSphere = nullptr;

```

selectedSphere = nullptr;: Inicializa el puntero selectedSphere a nullptr, lo que significa que no apunta a ninguna ubicación de memoria válida al comienzo. Esto es una práctica común para evitar que el puntero apunte a una dirección de memoria aleatoria o inválida.

### ¿Para Qué Se Está Usando el Puntero?

* selectedSphere: Se utiliza para hacer referencia a la esfera actualmente seleccionada por el usuario. Cuando se hace clic en una esfera, selectedSphere apunta a esa esfera, permitiendo que la esfera seleccionada se mueva con el ratón.

* spheres: El vector spheres almacena punteros a instancias de Sphere. Se utiliza para gestionar y manipular un conjunto de esferas, permitiendo crear múltiples esferas dinámicamente y acceder a ellas a través de sus punteros.

### ¿Qué Es Exactamente lo Que Está Almacenado en el Puntero?

* selectedSphere: Este puntero almacena la dirección de memoria de un objeto Sphere que se ha seleccionado. Si no hay ninguna esfera seleccionada, el puntero es nullptr. Si hay una esfera seleccionada, el puntero contiene la dirección de esa instancia específica de Sphere.

* spheres: Este vector almacena punteros a diferentes instancias de Sphere. Cada puntero dentro del vector apunta a una ubicación en la memoria donde se encuentra un objeto Sphere creado dinámicamente. Así, spheres contiene las direcciones de memoria de múltiples objetos Sphere.

## Actividad 6 El código anterior tiene un problema. ¿Puedes identificar cuál es? ¿Cómo lo solucionarías? Recuerda que deberías poder seleccionar una esfera y moverla con el mouse.

### Identificación del Problema

1. Problema de Actualización de la Posición:

    * En el método update de ofApp, la posición de la esfera seleccionada se actualiza directamente a la posición del mouse (selectedSphere->update(ofGetMouseX(), ofGetMouseY());). Esto hace que, mientras el botón del mouse está presionado, la esfera se mueva con el mouse, pero una vez que se suelta el botón, la esfera debería dejar de moverse. No hay ningún código que haga que la esfera deje de moverse al soltar el botón del mouse.
No hay Desselección de Esfera:

2. No hay lógica para deselectar la esfera seleccionada cuando el mouse se mueve o se suelta.
   
   * Esto puede causar problemas si se selecciona una esfera y luego se mueve el mouse, ya que la esfera seguirá moviéndose aunque el mouse no esté presionado.
  
### Solución

1. Agregar Deselección:

* Cambiar el comportamiento en `mousePressed` para que solo se seleccione una esfera si el mouse está presionado y no moverla si el botón no está presionado.

2. Actualizar el Código:

* Modificar `mousePressed` para asegurarse de que la esfera seleccionada se actualice solo si está siendo arrastrada.
Añadir el método mouseReleased para deselectar la esfera cuando se suelta el botón del mouse.

En el archivo ofApp.h
``` cpp
// Modificaciones en ofApp.h
#pragma once

#include "ofMain.h"

class Sphere {
public:
    Sphere(float x, float y, float radius);
    void draw();
    void update(float x, float y);
    float getX();
    float getY();
    float getRadius();

private:
    float x, y;
    float radius;
    ofColor color;
};

class ofApp : public ofBaseApp{

public:
    void setup();
    void update();
    void draw();

    void mouseMoved(int x, int y );
    void mousePressed(int x, int y, int button);
    void mouseReleased(int x, int y, int button); // Añadir esta línea

private:
    vector<Sphere*> spheres;
    Sphere* selectedSphere;
    bool isDragging; // Añadir esta línea
};


```

En ofApp.cpp

``` cpp
// Modificaciones en ofApp.cpp
#include "ofApp.h"

Sphere::Sphere(float x, float y, float radius) : x(x), y(y), radius(radius) {
    color = ofColor(ofRandom(255), ofRandom(255), ofRandom(255));
}

void Sphere::draw() {
    ofSetColor(color);
    ofDrawCircle(x, y, radius);
}

void Sphere::update(float x, float y) {
    this->x = x;
    this->y = y;
}

float Sphere::getRadius() {
    return radius;
}

float Sphere::getX() {
    return x;
}

float Sphere::getY() {
    return y;
}

//--------------------------------------------------------------
void ofApp::setup(){
    ofBackground(0);
    for (int i = 0; i < 5; i++) {
        float x = ofRandomWidth();
        float y = ofRandomHeight();
        float radius = ofRandom(20, 50);
        spheres.push_back(new Sphere(x, y, radius));
    }
    selectedSphere = nullptr;
    isDragging = false; // Inicializar isDragging
}

//--------------------------------------------------------------
void ofApp::update(){
    if (selectedSphere != nullptr && isDragging) { // Solo actualizar si se está arrastrando
        selectedSphere->update(ofGetMouseX(), ofGetMouseY());
    }
}

//--------------------------------------------------------------
void ofApp::draw(){
    for (auto sphere : spheres) {
        sphere->draw();
    }
}

//--------------------------------------------------------------
void ofApp::mouseMoved(int x, int y ){
    // No es necesario hacer nada aquí para el arrastre
}

//--------------------------------------------------------------
void ofApp::mousePressed(int x, int y, int button){
    if(button == OF_MOUSE_BUTTON_LEFT){
        for (auto sphere : spheres) {
            float distance = ofDist(x, y, sphere->getX(), sphere->getY());
            if (distance < sphere->getRadius()) {
                selectedSphere = sphere;
                isDragging = true; // Iniciar el arrastre
                break;
            }
        }
    }
}

//--------------------------------------------------------------
void ofApp::mouseReleased(int x, int y, int button){
    if(button == OF_MOUSE_BUTTON_LEFT){
        selectedSphere = nullptr;
        isDragging = false; // Detener el arrastre
    }
}

```

## Actividad 7 Ahora te voy a proponer que reflexiones profundamente sobre el manejo de la memoria en un programa. Se trata de un experimento en el que tienes que analizar por qué está funcionando mal.

Modifica el archivo ofApp.h

```cpp
#pragma once

#include "ofMain.h"

class Sphere {
public:
    Sphere(float x, float y, float radius);
    void draw() const;

    float x, y;
    float radius;
    ofColor color;
};

class ofApp : public ofBaseApp {
public:
    void setup();
    void update();
    void draw();

    void keyPressed(int key);

private:
    std::vector<Sphere*> globalVector;
    void createObjectInStack();
};
```

Y el archivo ofApp.cpp
```cpp
#include "ofApp.h"

Sphere::Sphere(float x, float y, float radius) : x(x), y(y), radius(radius) {
    color = ofColor(ofRandom(255), ofRandom(255), ofRandom(255));
}

void Sphere::draw() const {
    ofSetColor(color);
    ofDrawCircle(x, y, radius);
}

void ofApp::setup() {
    ofBackground(0);
}

void ofApp::update() {
}

void ofApp::draw() {
    ofSetColor(255);
    for (Sphere* sphere : globalVector) {
        if (sphere != nullptr) {
            ofDrawBitmapString("Objects pointed: " + ofToString(globalVector.size()), 20, 20);
            ofDrawBitmapString("Attempting to draw stored object...", 20, 40);
            ofDrawBitmapString("Stored Object Position: " + ofToString(sphere->x) + ", " + ofToString(sphere->y), 20, 60);
            sphere->draw();
        }
    }
}

void ofApp::keyPressed(int key) {
    if (key == 'c') {
        if (globalVector.empty()) {
            createObjectInStack();
        }
    }
    else if (key == 'd') {
        if (!globalVector.empty()) {
            ofLog() << "Accessing object in global vector: Position (" << globalVector[0]->x << ", " << globalVector[0]->y << ")";
        }
        else {
            ofLog() << "No objects in the global vector.";
        }
    }
}

void ofApp::createObjectInStack() {
    Sphere localSphere(ofRandomWidth(), ofRandomHeight(), 30);
    globalVector.push_back(&localSphere);
    ofLog() << "Object created in stack: Position (" << localSphere.x << ", " << localSphere.y << ")";
    localSphere.draw();
}
```

### ¿Qué sucede cuando presionas la tecla “c”?

Creación de un Objeto en la Pila (Stack):
En la función `createObjectInStack`, se crea un objeto Sphere en la pila (stack). Luego, se guarda un puntero a este objeto en un vector llamado `globalVector`. Una vez que la función termina, el objeto en la pila se borra automáticamente, pero el puntero en el vector sigue apuntando a esa ubicación de memoria que ya no es válida. Esto provoca que el puntero apunte a una "zona muerta" de la memoria, lo que puede causar errores si intentas usarlo.

el codigo original es:

```cpp
void ofApp::createObjectInStack() {
    Sphere localSphere(ofRandomWidth(), ofRandomHeight(), 30);
    globalVector.push_back(&localSphere); // Puntero a un objeto en la pila
    ofLog() << "Object created in stack: Position (" << localSphere.x << ", " << localSphere.y << ")";
    localSphere.draw();
}

```
El problema es que El objeto `localSphere` ya no existe después de que la función createObjectInStack termine. Así que el puntero que se guardó en globalVector ya no es válido.

Ahora para corregir el problema hay que hacer este codigo:

```cpp
void ofApp::createObjectInStack() {
    Sphere* heapSphere = new Sphere(ofRandomWidth(), ofRandomHeight(), 30); // Objeto en el heap
    globalVector.push_back(heapSphere); // Guardar el puntero
    ofLog() << "Object created in heap: Position (" << heapSphere->x << ", " << heapSphere->y << ")";
    heapSphere->draw();
}

```
Crear un Objeto en el Heap:
En la función `createObjectInStack`, se crea un objeto Sphere en el heap (memoria dinámica) usando new.
Este objeto sigue existiendo hasta que se borre explícitamente con delete.
Guardas el puntero a este objeto en `globalVector`, y el puntero seguirá siendo válido mientras no se libere la memoria.

* Cuando presionas la tecla "c" con la función modificada: Se crea un objeto Sphere en el heap, se guarda un puntero a este objeto en globalVector, y el objeto se dibuja en la pantalla.
  
* Por qué sucede: Crear el objeto en el heap asegura que el objeto persiste mientras el puntero sea válido. La memoria del objeto no se libera automáticamente, lo que requiere que gestiones la memoria manualmente para evitar fugas.


## Actividad 8 

en ofApp.h

```cpp
#pragma once

#include "ofMain.h"

// Declarar la clase Sphere
class Sphere {
public:
    Sphere(float x, float y, float radius);
    void draw() const;

    float x, y;
    float radius;
    ofColor color;
};

// Declarar la esfera global
extern Sphere stackSphere;

class ofApp : public ofBaseApp {
public:
    void setup();
    void update();
    void draw();

    void keyPressed(int key);

private:
    std::vector<Sphere*> heapSpheres; // Punteros a esferas en el heap
};

```

En ofApp.cpp

```cpp
#include "ofApp.h"

// Acceder a la esfera global
extern Sphere stackSphere;

Sphere::Sphere(float x, float y, float radius) : x(x), y(y), radius(radius) {
    color = ofColor(ofRandom(255), ofRandom(255), ofRandom(255));
}

void Sphere::draw() const {
    ofSetColor(color);
    ofDrawCircle(x, y, radius);
}

//--------------------------------------------------------------
void ofApp::setup() {
    ofBackground(0);
}

//--------------------------------------------------------------
void ofApp::update() {
}

//--------------------------------------------------------------
void ofApp::draw() {
    // Dibuja el objeto global
    stackSphere.draw();
    
    // Dibuja objetos en el heap
    for (Sphere* sphere : heapSpheres) {
        if (sphere != nullptr) {
            sphere->draw();
        }
    }
    
    ofSetColor(255);
    ofDrawBitmapString("Press 'h' to create heap sphere", 20, 20);
    ofDrawBitmapString("Press 'c' to clear heap spheres", 20, 40);
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'h') {
        // Crear una esfera en el heap y añadirla al vector
        Sphere* newSphere = new Sphere(ofRandomWidth(), ofRandomHeight(), 20);
        heapSpheres.push_back(newSphere);
    } else if (key == 'c') {
        // Limpiar todas las esferas en el heap
        for (Sphere* sphere : heapSpheres) {
            delete sphere;
        }
        heapSpheres.clear();
    }
}

// Destructor para limpiar la memoria del heap
ofApp::~ofApp() {
    for (Sphere* sphere : heapSpheres) {
        delete sphere;
    }
    heapSpheres.clear();
}


```

En main.cpp:

```c++
#include "ofMain.h"
#include "ofApp.h"

// Definir la esfera global
Sphere stackSphere(100, 100, 30);

int main() {
    ofSetupOpenGL(1024,768,OF_WINDOW);          
    ofRunApp(new ofApp()); // No es necesario pasar la referencia de stackSphere aquí
}

```

* Tecla 'h': Crea una nueva esfera en el heap y la añade al vector heapSpheres. La nueva esfera será visible en la pantalla.
  
* Tecla 'c': Limpia todas las esferas en el heap y libera la memoria. Las esferas ya no serán visibles después de presionar esta tecla.

### ¿Cuándo debo crear objetos en el heap y cuándo en memoria global?

1. Memoria Global

Características:

* Duración: Los objetos globales existen durante toda la vida del programa.

* Acceso: Son accesibles desde cualquier parte del código, siempre que estén declarados como extern en el archivo de encabezado si se definen en otro archivo.

Cuándo usar:

* Datos Compartidos: Usa objetos globales cuando necesites datos o recursos que deben ser accesibles en múltiples partes del programa.

* Configuración y Recursos: Pueden ser útiles para objetos que configuran aspectos globales del sistema, como configuraciones o recursos que deben estar disponibles durante toda la ejecución del programa.


2. Memoria en el Heap

Características:

* Duración: Los objetos en el heap existen hasta que son explícitamente destruidos con delete (en C++) o hasta que el recolector de basura los limpia (en lenguajes con recolección de basura como Java).

* Acceso: Son accesibles desde cualquier parte del programa si se tiene un puntero o referencia al objeto.

Cuándo usar:

* Objetos de Larga Duración: Usa el heap para objetos que necesitan existir durante mucho tiempo, más allá del alcance de una función o bloque.

* Objetos Grandes o Dinámicos: Es útil para objetos cuyo tamaño no se conoce en tiempo de compilación o para grandes cantidades de datos.

3. Resumen:
   
* Memoria Global: Ideal para datos o recursos que deben estar disponibles durante toda la vida del programa. Usa con cuidado para evitar problemas de mantenimiento y acoplamiento.

* Memoria en el Heap: Adecuado para objetos de larga duración, grandes, o cuando el tamaño del objeto no se conoce en tiempo de compilación. Requiere gestión explícita de la memoria.


## Actividad 9 Considera el siguiente código.

en ofApp.h

```cpp
#pragma once

#include "ofMain.h"

class ofApp : public ofBaseApp{
public:
    void setup();
    void update();
    void draw();

    void keyPressed(int key);
    void mousePressed(int x, int y, int button);

private:
    vector<ofVec2f*> heapObjects;
};
```

En ofApp.cpp

```cpp
#include "ofApp.h"

void ofApp::setup(){
    ofBackground(0);
}

void ofApp::update(){
}

void ofApp::draw(){
    ofSetColor(0, 0, 255); // Color azul para los objetos del heap
    for(auto& pos : heapObjects) {
        ofDrawCircle(pos->x, pos->y, 20);
        ofDrawBitmapString("Heap Memory", pos->x - 40, pos->y - 40);
    }
}

void ofApp::keyPressed(int key){
    if(key == 'f') {
        if(!heapObjects.empty()) {
            delete heapObjects.back();
            heapObjects.pop_back();
        }
    }
}

void ofApp::mousePressed(int x, int y, int button){
    heapObjects.push_back(new ofVec2f(x, y));
}
```
#### ¿Qué sucede cuando presionas la tecla “f”?

se borra la ultima esfera creada y asi hasta eliminarlas todas.


## Reto

**Código en ofApp.h**

```c++
#pragma once

#include "ofMain.h"

class ofApp : public ofBaseApp {
public:
    void setup();
    void update();
    void draw();

    void keyPressed(int key);
    void mousePressed(int x, int y, int button);
    
    // Funciones para la intersección del rayo con esferas
    void convertMouseToRay(int mouseX, int mouseY, glm::vec3& rayStart, glm::vec3& rayEnd);
    bool rayIntersectsSphere(const glm::vec3& rayStart, const glm::vec3& rayDir, const glm::vec3& sphereCenter, float sphereRadius, glm::vec3& intersectionPoint);
    
    // Parámetros de la cuadrícula
    int xStep, yStep, distDiv, amplitud;
    vector<glm::vec3> spherePositions;
    
    // Parámetros de la cámara
    ofEasyCam cam;
    
    // Esfera seleccionada
    bool sphereSelected;
    glm::vec3 selectedSpherePos;
};

```

**Código en ofApp.cpp**

```c++
#include "ofApp.h"

void ofApp::setup(){
    // Configuración inicial
    ofSetFrameRate(60);
    ofBackground(200, 200, 200);
    
    // Inicialización de parámetros
    xStep = 50;
    yStep = 50;
    distDiv = 50;
    amplitud = 150;
    
    // Generar posiciones de esferas
    for (int x = -ofGetWidth() / 2; x < ofGetWidth() / 2; x += xStep) {
        for (int y = -ofGetHeight() / 2; y < ofGetHeight() / 2; y += yStep) {
            float z = cos(ofDist(x, y, 0, 0) / distDiv) * amplitud;
            spherePositions.push_back(glm::vec3(x, y, z));
        }
    }
    
    // Inicializar variables
    sphereSelected = false;
}

void ofApp::update() {
    // Actualizar lógica si es necesario
}

void ofApp::draw(){
    cam.begin();
    
    // Dibujar las esferas
    for (auto& pos : spherePositions) {
        if (sphereSelected && pos == selectedSpherePos) {
            ofSetColor(255, 0, 0); // Esfera seleccionada en rojo
        } else {
            ofSetColor(255, 255, 255); // Esferas normales en blanco
        }
        ofDrawSphere(pos, 5.0); // Dibujar la esfera
    }
    
    // Mostrar información de la esfera seleccionada
    if (sphereSelected) {
        ofDrawBitmapString("Esfera seleccionada: " + ofToString(selectedSpherePos), 10, 20);
    }
    
    cam.end();
}

void ofApp::keyPressed(int key){
    switch (key) {
        case OF_KEY_UP:
            yStep += 5;
            break;
        case OF_KEY_DOWN:
            yStep -= 5;
            break;
        case OF_KEY_LEFT:
            xStep -= 5;
            break;
        case OF_KEY_RIGHT:
            xStep += 5;
            break;
        case 'a':
            amplitud += 10;
            break;
        case 'z':
            amplitud -= 10;
            break;
        case 's':
            distDiv += 5;
            break;
        case 'x':
            distDiv -= 5;
            break;
    }
    
    // Regenerar la cuadrícula de esferas con nuevos parámetros
    spherePositions.clear();
    for (int x = -ofGetWidth() / 2; x < ofGetWidth() / 2; x += xStep) {
        for (int y = -ofGetHeight() / 2; y < ofGetHeight() / 2; y += yStep) {
            float z = cos(ofDist(x, y, 0, 0) / distDiv) * amplitud;
            spherePositions.push_back(glm::vec3(x, y, z));
        }
    }
}

void ofApp::mousePressed(int x, int y, int button) {
    // Convertir coordenadas del mouse en un rayo 3D
    glm::vec3 rayStart, rayEnd;
    convertMouseToRay(x, y, rayStart, rayEnd);
    
    // Verificar si el rayo intersecta con alguna esfera
    sphereSelected = false;
    for (auto& pos : spherePositions) {
        glm::vec3 intersectionPoint;
        if (rayIntersectsSphere(rayStart, rayEnd - rayStart, pos, 5.0, intersectionPoint)) {
            sphereSelected = true;
            selectedSpherePos = pos;
            break;
        }
    }
}

void ofApp::convertMouseToRay(int mouseX, int mouseY, glm::vec3& rayStart, glm::vec3& rayEnd) {
    // Obtener matrices de proyección y modelo/vista de la cámara
    glm::mat4 modelview = cam.getModelViewMatrix();
    glm::mat4 projection = cam.getProjectionMatrix();
    ofRectangle viewport = ofGetCurrentViewport();
    
    // Convertir coordenadas del mouse a Normalized Device Coordinates (NDC)
    float x = 2.0f * (mouseX - viewport.x) / viewport.width - 1.0f;
    float y = 1.0f - 2.0f * (mouseY - viewport.y) / viewport.height;
    
    // Crear el rayo en NDC
    glm::vec4 rayStartNDC(x, y, -1.0f, 1.0f); // Near plane
    glm::vec4 rayEndNDC(x, y, 1.0f, 1.0f);   // Far plane
    
    // Convertir a coordenadas mundiales
    glm::vec4 rayStartWorld = glm::inverse(projection * modelview) * rayStartNDC;
    glm::vec4 rayEndWorld = glm::inverse(projection * modelview) * rayEndNDC;
    
    rayStartWorld /= rayStartWorld.w;
    rayEndWorld /= rayEndWorld.w;
    
    rayStart = glm::vec3(rayStartWorld);
    rayEnd = glm::vec3(rayEndWorld);
}

bool ofApp::rayIntersectsSphere(const glm::vec3& rayStart, const glm::vec3& rayDir, const glm::vec3& sphereCenter, float sphereRadius, glm::vec3& intersectionPoint) {
    glm::vec3 oc = rayStart - sphereCenter;
    
    float a = glm::dot(rayDir, rayDir);
    float b = 2.0f * glm::dot(oc, rayDir);
    float c = glm::dot(oc, oc) - sphereRadius * sphereRadius;
    
    float discriminant = b * b - 4 * a * c;
    
    if (discriminant < 0) {
        return false;
    } else {
        float t = (-b - sqrt(discriminant)) / (2.0f * a);
        intersectionPoint = rayStart + t * rayDir;
        return true;
    }
}

```

**Código en main.cpp**

```c++
#include "ofMain.h"
#include "ofApp.h"

//========================================================================
int main( ){
    ofSetupOpenGL(1024, 768, OF_WINDOW);  // Configurar la ventana
    ofRunApp(new ofApp());  // Iniciar la aplicación
}

```

----

**Interacciones del teclado**


| Acción                                     | Tecla(s)                |
|--------------------------------------------|--------------------------|
| Incrementar separación en el eje Y         | Flecha arriba (`UP`)      |
| Decrementar separación en el eje Y         | Flecha abajo (`DOWN`)     |
| Incrementar separación en el eje X         | Flecha derecha (`RIGHT`)  |
| Decrementar separación en el eje X         | Flecha izquierda (`LEFT`) |
| Incrementar amplitud en el eje Z           | `a`                      |
| Decrementar amplitud en el eje Z           | `z`                      |
| Incrementar divisor de distancia (`distDiv`)| `s`                      |
| Decrementar divisor de distancia (`distDiv`)| `x`                      |

**Descripción de los Controles**

- **Modificación de la Separación entre Esferas**:
  - **Tecla de flecha arriba (`UP`)**: Incrementa la separación en el eje Y (`yStep`).
  - **Tecla de flecha abajo (`DOWN`)**: Decrementa la separación en el eje Y (`yStep`).
  - **Tecla de flecha izquierda (`LEFT`)**: Decrementa la separación en el eje X (`xStep`).
  - **Tecla de flecha derecha (`RIGHT`)**: Incrementa la separación en el eje X (`xStep`).

- **Modificación de la Amplitud en el Eje Z**:
  - **Tecla `a`**: Incrementa la amplitud (`amplitud`), lo que hace que las esferas se dispersen más en el eje Z.
  - **Tecla `z`**: Decrementa la amplitud (`amplitud`), lo que reduce la dispersión de las esferas en el eje Z.

- **Modificación de la División de Distancia (`distDiv`)**:
  - **Tecla `s`**: Incrementa el divisor de distancia (`distDiv`), lo que afecta la variación en Z.
  - **Tecla `x`**: Decrementa el divisor de distancia (`distDiv`), lo que cambia la variación en Z.

----
 
**Informe sobre el Manejo de Memoria en la Aplicación de Cuadrícula de Esferas en 3D**

**Datos en la Memoria**

 1. **Posiciones de las Esferas (`spherePositions`)**

- **Tipo de Datos:** `std::vector<glm::vec3>`
- **Memoria Asignada:** Se encuentra en el heap (montículo).
- **Descripción:** El vector `spherePositions` almacena las posiciones en 3D de todas las esferas en la cuadrícula. Cada posición se representa mediante un objeto `glm::vec3`, que es una estructura de datos que contiene tres coordenadas flotantes (x, y, z).
- **Manejo de Memoria:** La memoria para este vector se asigna dinámicamente cuando se ejecuta la función `setup()` y se redimensiona si se cambian los parámetros de la cuadrícula (como `xStep`, `yStep`, `distDiv`, o `amplitud`). Si bien OpenFrameworks y C++ gestionan la asignación y liberación de memoria de los vectores automáticamente, es esencial asegurarse de no causar fragmentación de memoria al regenerar repetidamente el vector.

 2. **Cámara (`cam`)**

- **Tipo de Datos:** `ofEasyCam`
- **Memoria Asignada:** Se encuentra en la stack (pila) al ser una variable miembro de la clase `ofApp`.
- **Descripción:** `ofEasyCam` es un objeto que gestiona la cámara 3D en la aplicación, permitiendo la navegación y visualización de la escena desde diferentes ángulos.
- **Manejo de Memoria:** Al estar en la pila, la memoria se asigna cuando se crea la instancia de `ofApp` y se libera automáticamente cuando se destruye el objeto. Como `ofEasyCam` no utiliza mucha memoria, su impacto es mínimo en comparación con otros elementos de la aplicación.

 3. **Variables de Control (`xStep`, `yStep`, `distDiv`, `amplitud`)**

- **Tipo de Datos:** `int` y `float`
- **Memoria Asignada:** Se encuentran en la stack (pila).
- **Descripción:** Estas variables controlan la generación de la cuadrícula de esferas y su comportamiento visual. Al cambiar estos valores mediante el teclado, se regenera la cuadrícula con nuevas posiciones y formas.
- **Manejo de Memoria:** Al igual que con la cámara, estas variables se asignan en la pila y tienen un bajo impacto en la memoria total. Se almacenan y gestionan de manera automática por el compilador.

 4. **Variables para la Selección de Esferas (`sphereSelected`, `selectedSpherePos`)**

- **Tipo de Datos:** `bool` y `glm::vec3`
- **Memoria Asignada:** Se encuentran en la stack (pila).
- **Descripción:** `sphereSelected` es un booleano que indica si una esfera ha sido seleccionada. `selectedSpherePos` almacena la posición de la esfera seleccionada.
- **Manejo de Memoria:** Al estar en la pila, estas variables se asignan y liberan automáticamente. Como se utilizan únicamente para gestionar la selección de esferas, su impacto en la memoria es insignificante.

 5. **Transformaciones de Rayo y Matrices (`rayStart`, `rayEnd`, `modelview`, `projection`)**

- **Tipo de Datos:** `glm::vec3`, `glm::mat4`
- **Memoria Asignada:** Se encuentran en la stack (pila).
- **Descripción:** Estas variables se utilizan para calcular el rayo 3D generado a partir de las coordenadas del mouse y para determinar si dicho rayo intersecta alguna esfera.
- **Manejo de Memoria:** Al ser temporales, estas variables se asignan en la pila dentro de la función que las utiliza y se liberan al salir de su ámbito. El uso de la pila asegura una rápida asignación y liberación de memoria para estas transformaciones.

El manejo de memoria en esta aplicación es eficiente, utilizando principalmente la pila para variables locales y temporales, y el heap para estructuras de datos más grandes como `spherePositions`. La gestión automática de la memoria por parte de C++ en combinación con el uso de vectores y objetos hace que la aplicación sea segura en términos de fugas de memoria, siempre y cuando se utilicen correctamente. Es importante considerar la regeneración de la cuadrícula en función de la interacción del usuario, ya que puede afectar el rendimiento si se realiza con demasiada frecuencia o con un gran número de esferas.


### Video

https://github.com/user-attachments/assets/7d234971-7a9b-47cf-8e37-be97cad98fac




