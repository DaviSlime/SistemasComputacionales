# Bitácora de aprendizaje de la unidad 2: lenguaje ensamblador

## By: David Vanegas Londoño

## Actividad 1

### ¿Qué es la entrada-salida mapeada a memoria?

En la plataforma Hack, la entrada-salida mapeada a memoria es un método en el que los dispositivos de entrada y salida se controlan a través de la memoria del sistema lo que crea es que se pueda leer una informacion como el teclado y pasarlo a un codigo usando solo la memoria del sistema.

### ¿Cómo se implementa en la plataforma Hack?

Se implementa para leer el valor del teclado y mostrar un codigo en la pantalla, estos pueden ser leídos y escritos como si fueran ubicaciones de memoria regulares.

### Inventa un programa que haga uso de la entrada-salida mapeada a memoria.

``` 
@KEYBOARD    // Dirección de la entrada del teclado
D=M        // Leer el valor del teclado

@SCREEN      // Dirección de la salida de la pantalla
M=D        // Escribir el valor del teclado en la pantalla

@END         // Salto al final del programa
0;JMP 
```

al simular este codigo lo que nos damos cuenta es que lo que hace este programa es leer el valor del teclado y mostrarlo en la pantalla.

## Actividad 3

### Vas a implementar y simular una modificación al retos 20 de la unidad anterior. Si se presiona la letra “d” muestras la imagen que diseñaste en el reto 18. Si no se presiona ninguna tecla, borraras la imagen.

```
// Verifica si se presiona la tecla 'd'
(START)
@24576   // Dirección del teclado (0x6000)
D=M      // Leer el valor del teclado
@100     // Valor ASCII de 'd'
D=D-A    // Comparar con 'd'
@PRESIONED
D;JEQ    // Si es igual, saltar a PRESIONED
@CLEAR_SCREEN
0;JMP    // Si no es igual, ir a CLEAR_SCREEN

(PRESIONED)
@SCREEN  // Dirección de la pantalla (0x6001)
D=A
@R12     // Guardar la dirección de la pantalla en R12
M=D
@RETURN_ADDRESS
D=A
@R13     // Guardar la dirección de retorno en R13
M=D

(draw)
	@SCREEN
	D=A
	@R12
	A=M
	@32
	AD=D+A
	M=0
	@32
	AD=D+A
	M=0
	@32
	AD=D+A
	M=0
	@32
	AD=D+A
	M=0
	@32
	AD=D+A
	M=0
	@32
	AD=D+A
	M=0
	@32
	AD=D+A
	M=0
	@32
	AD=D+A
	M=0
	@32
	AD=D+A
	M=0
	@32
	AD=D+A
	@15420
	D=D+A
	A=D-A
	M=0xFF  // Dibuja en la fila 11
	@32
	AD=D+A
	@16962
	D=D+A
	A=D-A
	M=0xFF  // Dibuja en la fila 12
	@32
	AD=D+A
	@32383
	D=D+A
	A=D-A
	M=0xFF  // Dibuja en la fila 13
	@32
	AD=D+A
	@29647
	D=D+A
	A=D-A
	M=0xFF  // Dibuja en la fila 14
	@32
	AD=D+A
	@31135
	D=D+A
	A=D-A
	M=0xFF  // Dibuja en la fila 15
	@32
	AD=D+A
	@17346
	D=D+A
	A=D-A
	M=0xFF  // Dibuja en la fila 16
	@32
	AD=D+A
	@8580
	D=D+A
	A=D-A
	M=0xFF  // Dibuja en la fila 17
	@32
	AD=D+A
	@4488
	D=D+A
	A=D-A
	M=0xFF  // Dibuja en la fila 18
	@32
	AD=D+A
	@2064
	D=D+A
	A=D-A
	M=0xFF  // Dibuja en la fila 19
	@32
	AD=D+A
	@1056
	D=D+A
	A=D-A
	M=0xFF  // Dibuja en la fila 20

	@R13
	A=M
	D;JMP

(CLEAR_SCREEN)
@SCREEN
	D=A
	@R12
	A=M
	@32
	AD=D+A
	M=0  // Borra la primera fila
	@32
	AD=D+A
	M=0  // Borra la segunda fila
	@32
	AD=D+A
	M=0  // Borra la tercera fila
	@32
	AD=D+A
	M=0  // Borra la cuarta fila
	@32
	AD=D+A
	M=0  // Borra la quinta fila
	@32
	AD=D+A
	M=0  // Borra la sexta fila
	@32
	AD=D+A
	M=0  // Borra la séptima fila
	@32
	AD=D+A
	M=0  // Borra la octava fila
	@32
	AD=D+A
	M=0  // Borra la novena fila
	@32
	AD=D+A
	M=0  // Borra la décima fila

	@R13
	A=M
	D;JMP

(RETURN_ADDRESS)
@0
D=A

```

## Actividad 4 

### Ahora realizarás una nueva variación al programa de la actividad anterior. Si se presiona la letra “d” muestras la imagen que diseñaste en el reto 18. Solo si se presiona la letra “e” borraras la imagen que se muestra en pantalla.

```
// Verifica si se presiona la tecla 'd' o 'e'
(START)
@24576   // Dirección del teclado (0x6000)
D=M      // Leer el valor del teclado
@100     // Valor ASCII de 'd'
D=D-A    // Comparar con 'd'
@DRAW_IMAGE
D;JEQ    // Si se presiona 'd', saltar a DRAW_IMAGE
@101     // Valor ASCII de 'e'
D=M-D    // Comparar con 'e'
@CLEAR_SCREEN
D;JEQ    // Si se presiona 'e', saltar a CLEAR_SCREEN
@START
0;JMP    // Si no se presiona ni 'd' ni 'e', repetir

(DRAW_IMAGE)
@SCREEN  // Dirección de la pantalla (0x6001)
D=A      // Obtener la dirección base de la pantalla
@R12     // Guardar la dirección de la pantalla en R12
M=D
@RETURN_ADDRESS
D=A
@R13     // Guardar la dirección de retorno en R13
M=D

(draw)
	// put bitmap location value in R12
	// put code return address in R13
	@SCREEN
	D=A
	@R12
	AD=D+M
	// row 1
	M=0
	// row 2
	D=A // D holds previous addr
	@32
	AD=D+A
	M=0
	// row 3
	D=A // D holds previous addr
	@32
	AD=D+A
	M=0
	// row 4
	D=A // D holds previous addr
	@32
	AD=D+A
	M=0
	// row 5
	D=A // D holds previous addr
	@32
	AD=D+A
	M=0
	// row 6
	D=A // D holds previous addr
	@32
	AD=D+A
	M=0
	// row 7
	D=A // D holds previous addr
	@32
	AD=D+A
	M=0
	// row 8
	D=A // D holds previous addr
	@32
	AD=D+A
	M=0
	// row 9
	D=A // D holds previous addr
	@32
	AD=D+A
	M=0
	// row 10
	D=A // D holds previous addr
	@32
	AD=D+A
	@15420 // A holds val
	D=D+A // D = addr + val
	A=D-A // A=addr + val - val = addr
	M=D-A // RAM[addr] = val
	// row 11
	D=A // D holds previous addr
	@32
	AD=D+A
	@16962 // A holds val
	D=D+A // D = addr + val
	A=D-A // A=addr + val - val = addr
	M=D-A // RAM[addr] = val
	// row 12
	D=A // D holds previous addr
	@32
	AD=D+A
	@32383 // A holds val
	D=D+A // D = addr + val
	A=D-A // A=addr + val - val = addr
	M=A-D // RAM[addr]=-val
	// row 13
	D=A // D holds previous addr
	@32
	AD=D+A
	@29647 // A holds val
	D=D+A // D = addr + val
	A=D-A // A=addr + val - val = addr
	M=A-D // RAM[addr]=-val
	// row 14
	D=A // D holds previous addr
	@32
	AD=D+A
	@31135 // A holds val
	D=D+A // D = addr + val
	A=D-A // A=addr + val - val = addr
	M=A-D // RAM[addr]=-val
	// row 15
	D=A // D holds previous addr
	@32
	AD=D+A
	@17346 // A holds val
	D=D+A // D = addr + val
	A=D-A // A=addr + val - val = addr
	M=D-A // RAM[addr] = val
	// row 16
	D=A // D holds previous addr
	@32
	AD=D+A
	@8580 // A holds val
	D=D+A // D = addr + val
	A=D-A // A=addr + val - val = addr
	M=D-A // RAM[addr] = val
	// row 17
	D=A // D holds previous addr
	@32
	AD=D+A
	@4488 // A holds val
	D=D+A // D = addr + val
	A=D-A // A=addr + val - val = addr
	M=D-A // RAM[addr] = val
	// row 18
	D=A // D holds previous addr
	@32
	AD=D+A
	@2064 // A holds val
	D=D+A // D = addr + val
	A=D-A // A=addr + val - val = addr
	M=D-A // RAM[addr] = val
	// row 19
	D=A // D holds previous addr
	@32
	AD=D+A
	@1056 // A holds val
	D=D+A // D = addr + val
	A=D-A // A=addr + val - val = addr
	M=D-A // RAM[addr] = val
	// row 20
	D=A // D holds previous addr
	@32
	AD=D+A
	@960 // A holds val
	D=D+A // D = addr + val
	A=D-A // A=addr + val - val = addr
	M=D-A // RAM[addr] = val
	// return
	@R13
	A=M
	D;JMP
(CLEAR_SCREEN)
	@SCREEN  // Dirección de la pantalla (0x6001)
	D=A      // Obtener la dirección base de la pantalla
	@R12     // Guardar la dirección de la pantalla en R12
	M=D
	@RETURN_ADDRESS
	D=A
	@R13     // Guardar la dirección de retorno en R13
	M=D

(clear)
	@R12
	A=M      // Obtener la dirección base de la pantalla
	@0       // Comenzar en la dirección 0 (la primera celda de la pantalla)
	@20480   // Número total de celdas a modificar (256 columnas * 80 filas = 20480 celdas)
	D=A
	@CLEAR_LOOP
	M=0      // Establecer la celda a 0 (vacía)
	@20480
	D=D-A    // Decrementar el contador de celdas
	@CLEAR_LOOP
	D;JGT    // Si D > 0, repite el loop
	@R13
	A=M
	D;JMP

(RETURN_ADDRESS)
@0
D=A

```

# RETOS

## Reto 1

### Escribe un programa en lenguaje ensamblador que sume los primeros 100 números naturales.

``` python
int i = 1;
int sum = 0;
While (i <= 100){
   sum += i;
   i++;
}
```

```
// Inicialización de variables
@1       // i = 1
D=A
@i       // Guardar i en la dirección @i
M=D

@0       // sum = 0
D=A
@sum     // Guardar sum en la dirección @sum
M=D

@100     // Límite superior
D=A
@limit   // Guardar límite en la dirección @limit
M=D

// Comienza el bucle
(LOOP)
    @i       // Cargar el valor de i
    D=M
    @limit   // Comparar i con el límite
    D=D-M
    @END     // Si i > 100, saltar al final
    D;JGT

    @sum     // Cargar el valor de sum
    D=M
    @i       // Cargar el valor de i
    D=D+M
    @sum     // Guardar la nueva suma
    M=D

    @i       // Incrementar i
    D=M
    @1
    D=D+A
    @i
    M=D

    @LOOP   // Repetir el bucle
    0;JMP

(END)
// Fin del programa
@END
0;JMP

```

### ¿Cómo están implementadas las variables i y sum?

Las variables i y sum están implementadas en el programa de ensamblador utilizando registros de la memoria de la plataforma Hack. En Hack, cada variable se almacena en una dirección específica de memoria, y los valores se manipulan directamente en estas direcciones.

### ¿En qué direcciones de memoria están estas variables?

La variable i está almacenada en la dirección de memoria etiquetada como @i.
La variable sum está almacenada en la dirección de memoria etiquetada como @sum.

### ¿Cómo está implementado el ciclo while?

El ciclo while se implementa utilizando una combinación de etiquetas y saltos condicionales:

Se compara i con el límite superior (100).
Si i es menor o igual que 100, se realiza la suma y el incremento de i.
Después de cada iteración, el flujo regresa al inicio del ciclo mediante un salto incondicional (0;JMP).

### ¿Cómo se implementa la variable i?

La variable i se implementa utilizando una dirección de memoria específica donde se almacena su valor. En cada iteración del ciclo, el valor de i se lee, se incrementa y se vuelve a escribir en la misma dirección de memoria.

### ¿En qué parte de la memoria se almacena la variable i?

En el código, la variable i está almacenada en la dirección de memoria representada por @i. En un programa Hack real, el ensamblador asignará una dirección de memoria concreta a esta etiqueta cuando se compile el código. En la simulación, esto puede ser una dirección en el rango de memoria de datos del Hack.

### Después de todo lo que has hecho, ¿Qué es entonces una variable?

Una variable, en el contexto de programación, es un contenedor para almacenar datos que pueden cambiar durante la ejecución del programa. En el lenguaje ensamblador Hack, una variable se implementa como una dirección de memoria específica donde se almacenan y manipulan los datos.

### ¿Qué es la dirección de una variable?

La dirección de una variable es la ubicación específica en la memoria donde se almacena el valor de la variable. Es un número que representa la posición en la memoria y permite a la CPU acceder y modificar el valor almacenado en esa posición.

### ¿Qué es el contenido de una variable?

El contenido de una variable es el valor que se almacena en la dirección de memoria asignada a la variable. Es la información que se puede leer o modificar mediante operaciones en el programa.

## Reto 2

### Transforma el programa en alto nivel anterior para que utilice un ciclo for en vez de un ciclo while.

``` python
int sum = 0;
for (int i = 1; i <= 100; i++) {
    sum += i;
}

```

## Reto 3

### Escribe un programa en lenguaje ensamblador que implemente el programa anterior.

```
// Inicialización de variables
@0   
D=A    
@sum   
M=D     

// Inicializar i
@1     
D=A   
@i     
M=D     

// Definir el límite superior
@100     
D=A   
@limit 
M=D    

// Inicio del ciclo for
(FOR_LOOP)
    @i      
    D=M
    @limit   
    D=D-M  
    @END    
    D;JGT

    @sum    
    D=M
    @i    
    D=D+M  
    @sum   
    M=D

    @i       
    D=M
    @1      
    D=D+A    
    @i       
    M=D

    @FOR_LOOP 
    0;JMP

(END)
// Fin del programa
@END
0;JMP

```

## Reto 4

### Ahora vamos a acercarnos al concepto de puntero. Un puntero es una variable que almacena la dirección de memoria de otra variable. Observa el siguiente programa escrito en C++:

``` c++
int a = 10;
int *p;
p = &a;
*p = 20;
```

El programa anterior modifica el contenido de la variable a por medio de la variable p. p es un puntero porque almacena la dirección de memoria de la variable a. En este caso el valor de la variable a será 20 luego de ejecutar *p = 20;. Ahora analiza:

* ¿Cómo se declara un puntero en C++? int *p;. p es una variable que almacenará nla dirección de un variable que almacena enteros. 

* ¿Cómo se define un puntero en C++?

  p = &a;. Definir el puntero es inicializar el valor del puntero, es decir, guardar la dirección de una variable. En este caso p contendrá la dirección de a.

* ¿Cómo se almacena en C++ la dirección de memoria de una variable?

   Con el operador &. p = &a;

* ¿Cómo se escribe el contenido de la variable a la que apunta un puntero?

  Con el operador *. *p = 20;. En este caso como p contiene la dirección de a entonces *p a la izquierda del igual indica que quieres actualizar el valor de la variable a.

## Reto 5

### Traduce este programa a lenguaje ensamblador:

``` c++
int a = 10;
int *p;
p = &a;
*p = 20;
```

```
// Inicialización de la variable 'a'
@10      // Cargar el valor 10
D=A      // Guardar el valor 10 en el registro D
@a       // Dirección de la variable 'a'
M=D      // Guardar el valor de D (10) en la dirección de 'a'

// Declaración e inicialización del puntero 'p'
@a       // Cargar la dirección de la variable 'a'
D=A      // Guardar la dirección de 'a' en el registro D
@p       // Dirección de la variable 'p'
M=D      // Guardar la dirección de 'a' en 'p'

// Actualizar el valor de 'a' a través del puntero 'p'
@p       // Cargar la dirección de 'p'
D=M      // Obtener la dirección almacenada en 'p' (la dirección de 'a')
@20      // Cargar el valor 20
M=D      // Usar la dirección de 'a' para actualizar el valor a 20

// Fin del programa
@END    // Etiqueta para el final del programa
0;JMP   // Salto incondicional para finalizar la ejecución

// Definición de variables
(a)     // Etiqueta para la dirección de la variable 'a'
@0      // Valor inicial (en la memoria)
0;JMP   // No se ejecuta nada, solo etiqueta

(p)     // Etiqueta para la dirección de la variable 'p'
@0      // Valor inicial (en la memoria)
0;JMP   // No se ejecuta nada, solo etiqueta

(END)   // Etiqueta de fin del programa

```

## Reto 6

Ahora vas a usar un puntero para leer la posición de memoria a la que este apunta, es decir, vas a leer por medio del puntero la variable cuya dirección está almacenada en él.

``` c++

int a = 10;
int b = 5;
int *p;
p = &a;
b = *p;
```

entonces en ensamblador queda asi:

```
// Inicialización de las variables 'a' y 'b'
@10      // Cargar el valor 10
D=A      // Guardar el valor 10 en el registro D
@a       // Dirección de la variable 'a'
M=D      // Guardar el valor de D (10) en la dirección de 'a'

@5       // Cargar el valor 5
D=A      // Guardar el valor 5 en el registro D
@b       // Dirección de la variable 'b'
M=D      // Guardar el valor de D (5) en la dirección de 'b'

// Declaración e inicialización del puntero 'p'
@a       // Cargar la dirección de la variable 'a'
D=A      // Guardar la dirección de 'a' en el registro D
@p       // Dirección de la variable 'p'
M=D      // Guardar la dirección de 'a' en 'p'

// Leer el valor al que apunta 'p' y asignar a 'b'
@p       // Cargar la dirección de 'p'
D=M      // Obtener la dirección almacenada en 'p' (la dirección de 'a')
@M      // Leer el valor en la dirección de 'a'
D=M      // Guardar el valor de la dirección de 'a' en el registro D
@b       // Dirección de la variable 'b'
M=D      // Guardar el valor de D (que es el valor de 'a') en 'b'

// Fin del programa
@END    // Etiqueta para el final del programa
0;JMP   // Salto incondicional para finalizar la ejecución

// Definición de variables
(a)     // Etiqueta para la dirección de la variable 'a'
@0      // Valor inicial (en la memoria)
0;JMP   // No se ejecuta nada, solo etiqueta

(b)     // Etiqueta para la dirección de la variable 'b'
@0      // Valor inicial (en la memoria)
0;JMP   // No se ejecuta nada, solo etiqueta

(p)     // Etiqueta para la dirección de la variable 'p'
@0      // Valor inicial (en la memoria)
0;JMP   // No se ejecuta nada, solo etiqueta

(END)   // Etiqueta de fin del programa

```

## Reto 7

### Traduce este programa a lenguaje ensamblador:

``` c++
int a = 10;
int b = 5;
int *p;
p = &a;
b = *p;
```

```
// Inicialización de la variable 'a'
@10       // Cargar el valor 10
D=A       // Guardar el valor 10 en el registro D
@a        // Dirección de la variable 'a'
M=D       // Guardar el valor 10 en la dirección de 'a'

// Inicialización de la variable 'b'
@5        // Cargar el valor 5
D=A       // Guardar el valor 5 en el registro D
@b        // Dirección de la variable 'b'
M=D       // Guardar el valor 5 en la dirección de 'b'

// Declaración e inicialización del puntero 'p'
@a        // Cargar la dirección de la variable 'a'
D=A       // Guardar la dirección de 'a' en el registro D
@p        // Dirección de la variable 'p'
M=D       // Guardar la dirección de 'a' en 'p'

// Leer el valor al que apunta 'p' y asignar a 'b'
@p        // Cargar la dirección de la variable 'p'
D=M       // Obtener la dirección almacenada en 'p' (la dirección de 'a')
@a        // Cargar la dirección de la variable 'a' (donde está el valor 10)
D=M       // Leer el valor en la dirección de 'a' (10)
@b        // Dirección de la variable 'b'
M=D       // Guardar el valor leído (10) en 'b'

// Fin del programa
@END      // Etiqueta para el final del programa
0;JMP     // Salto incondicional para finalizar la ejecución

// Definición de variables
(a)       // Etiqueta para la dirección de la variable 'a'
@0        // Valor inicial (en la memoria)
0;JMP     // No se ejecuta nada, solo etiqueta

(b)       // Etiqueta para la dirección de la variable 'b'
@0        // Valor inicial (en la memoria)
0;JMP     // No se ejecuta nada, solo etiqueta

(p)       // Etiqueta para la dirección de la variable 'p'
@0        // Valor inicial (en la memoria)
0;JMP     // No se ejecuta nada, solo etiqueta

(END)     // Etiqueta de fin del programa

```

## Reto 8

### Vas a parar un momento y tratarás de recodar de memoria lo siguiente. Luego verifica con un compañero o con el profesor.

* ¿Qué hace esto int *pvar;?

Esto declara un puntero llamado pvar que puede apuntar a una variable de tipo int.

* ¿Qué hace esto *pvar = var;?

asigna el valor de var a la variable a la que pvar apunta. Primero, el puntero pvar debe estar apuntando a una dirección de memoria válida. Luego, *pvar se establece con el valor de var.

* ¿Qué hace esto var2 = *pvar?

asigna el valor de la variable a la que pvar apunta a la variable var2. Primero, *pvar obtiene el valor de la dirección de memoria almacenada en pvar, y luego ese valor se asigna a var2.

* ¿Qué hace esto pvar = &var3?

asigna la dirección de la variable var3 al puntero pvar. Ahora, pvar apunta a la dirección de var3, lo que significa que *pvar se puede usar para acceder o modificar el valor de var3.

## Reto 9

### Considera que el punto de entrada del siguiente programa es la función main, es decir, el programa inicia llamando la función main. Vas a proponer una posible traducción a lenguaje ensamblador de la función suma, cómo llamar a suma y cómo regresar a std::cout << "El valor de c es: " << c << std::endl; una vez suma termine.

``` c++
#include <iostream>

int suma(int a, int b) {
   int var = a + b;
   return var;
}


int main() {
   int c = suma(6, 9);
   std::cout << "El valor de c es: " << c << std::endl;
   return 0;
}
```

```
(START)

// Inicializar valores para la llamada a suma
@6       
D=A    
@R1      
M=D     

@9      
D=A    
@R1    
A=M+1    
M=D     

// Llamar a la función suma
@SUMA     
0;JMP

// Etiqueta de retorno de la función main
(POSTSUMA)
@R1    
D=M      
@R0    
M=D   

// Simular std::cout << "El valor de c es: " << c << std::endl;
@SCREEN  
D=A    
@R0     
A=M      
M=D      

// Terminar el programa
@END
0;JMP

// Función suma
(SUMA)

    @R1    
    D=M   


    @2       
    D=D+A    
    A=D      
    D=M    
    @R2      
    M=D     

    @R1     
    D=M     

    @3       
    D=D+A    
    A=D     
    D=M   
    @R3      
    M=D     


    @R2     
    D=M   
    @R3      
    D=D+M   


    @R4   
    M=D     


    @R4   
    D=M      
    @R1    
    M=D   

    @POSTSUMA 
    0;JMP


(END)
    @END
    0;JMP

```
