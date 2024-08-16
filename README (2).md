# Bitácora de aprendizaje para la Unidad 2. Computadores embebidos

## By: David Vanegas Londoño

## Experimento 1

### **¿Cómo se leen los pulsadores A y B?**

se importa una librería especifica de micro:bit que permite utilizar los comandos button_a y button_b por ejemplo:

``` python
from microbit import *

while True:
  if button_a.was_pressed():
     display.show('A')

  elif button_b.was_pressed():
     display.show('B')
```

## Experimento 2

### **¿Cómo se leen el botón virtual que está en el logo del micro:bit?**

Con la libreria importada se usa el comando button_logo y esto activa el codigo especifico de este botón que se activa con un sensor por ejemplo:

```
from microbit import *

while True:
  if button_logo.was_pressed():
     display.show(image.HEART)
```

## Experimento 3

### **¿Cómo se lee información serial que llega al micro:bit?**

La informacion serial se lee por medio de un codigo, nosotros hicimos este experimento:



``` python
from microbit import *
import music

# Define una melodía como una lista de notas
melody = [
    'c4:4', 'd4:4', 'e4:4', 'f4:4', 'g4:4', 'a4:4', 'b4:4', 'c5:4'
]

# Reproduce la melodía
music.play(melody)
```
este programa genera una melodia con los datos y un programa los lee y los interpreta.

## Experimento 4

### **¿Cómo se envía información serial desde el micro:bit?**

La informacion serial se envia desde la lectura de un codigo y llega a la targeta de procesamiento del micro:bit reproduciendo el codigo que creamos.

## Experimento 5

### **¿Cómo dibujar en la pantalla de LED?**

para dibujar en la pantalla led se usan coordenadas x y, como es una matriz de 5x5 se usan los valores desde 0 hasta 4 para las dos coordenadas y de ahi se eligen los leds que se quieren pintar.

## Experimento 6

### **¿Cómo hacer para producir sonidos con el speaker?**

Para producir sonidos con el Speaker primero en el codigo se importa la libreria de music para poder usar los comandos music.play() para cargar una cancion predeterminada y music.pith() para crear tus propias obras usando los codigos de cada tecla y su tiempo de presión.

**EJEMPLO**

```
from microbit import *
import music

# Definir una versión extendida de la melodía de "Golden Hour"
melody = [
    # Parte 1
    'c4:4', 'e4:4', 'g4:4', 'c5:4',
    'g4:4', 'e4:4', 'c4:4',
    
    # Parte 2
    'a4:4', 'f4:4', 'd4:4', 'a4:4',
    'd4:4', 'f4:4', 'a4:4', 'c5:4',
    
    # Parte 3
    'e4:4', 'g4:4', 'b4:4', 'e5:4',
    'b4:4', 'g4:4', 'e4:4',
    
    # Parte 4
    'g4:4', 'e4:4', 'c4:4', 'g4:4',
    'c4:4', 'e4:4', 'g4:4', 'c5:4',

    # Parte 5
    'c4:4', 'e4:4', 'g4:4', 'c5:4',
    'g4:4', 'e4:4', 'c4:4',
    
    # Parte 6
    'a4:4', 'f4:4', 'd4:4', 'a4:4',
    'd4:4', 'f4:4', 'a4:4', 'c5:4',
    
    # Parte 7
    'e4:4', 'g4:4', 'b4:4', 'e5:4',
    'b4:4', 'g4:4', 'e4:4',
    
    # Parte 8 (Final)
    'g4:4', 'e4:4', 'c4:4', 'g4:4',
    'c4:4', 'e4:4', 'g4:4', 'c5:4',
]

# Reproduce la melodía en un bucle
while True:
    music.play(melody)
    sleep(1000)  # Pausa de 1 segundo antes de repetir

```

## Experimento 7

### **Analiza con mucho detenimiento este código:**

``` python
from microbit import *
import utime

class Pixel:
    def __init__(self,pixelX,pixelY,initState,interval):
        self.state = "Init"
        self.startTime = 0
        self.interval = interval
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState

    def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeout"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

        elif self.state == "WaitTimeout":
            currentTime = utime.ticks_ms()
            if utime.ticks_diff(currentTime,self.startTime) > self.interval:
                self.startTime = currentTime
                if self.pixelState == 9:
                    self.pixelState = 0
                else:
                    self.pixelState = 9
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

pixel1 = Pixel(0,0,0,1000)
pixel2 = Pixel(4,4,0,500)

while True:
    pixel1.update()
    pixel2.update()
```

### **Describe detalladamente cómo funciona este ejemplo.**

* ¿Puedes identificar algunos estados?

  Init: El estado inicial en el que se configura el tiempo de inicio (startTime) y se enciende o apaga el píxel por primera vez.
  WaitTimeout: El estado en el que el sistema espera a que pase el intervalo de tiempo antes de cambiar el estado del píxel.

* Del contexto del ejemplo ¿Qué son los estados?

  Los estados en este ejemplo representan las diferentes etapas de comportamiento de un píxel. Controlan el flujo del programa determinando si se debe iniciar el temporizador o si se debe esperar para alternar el estado del píxel.

* Del contexto del ejemplo ¿Qué son los eventos?

  Los eventos son las condiciones o acciones que desencadenan la transición entre estados. En este ejemplo, el evento clave es el paso del tiempo medido (utime.ticks_diff(currentTime, self.startTime)), que decide si es momento de cambiar el estado del píxel, los if de forma jerarquica son los estados.

* Del contexto del ejemplo ¿Qué son las acciones?

  Las acciones son las operaciones que se ejecutan cuando se cambia de estado o se permanece en un estado. En este código, las acciones principales son:

Establecer el estado inicial del píxel en "Init".
Alternar el estado del píxel (encendido/apagado) en "WaitTimeout".
Actualizar la pantalla LED con el nuevo estado del píxel usando display.set_pixel

## Experimento 8

* ¿Qué es una máquina de estados en programación?

Es un modelo de programación que organiza un sistema en varios estados distintos, donde cada estado representa una condición específica del sistema. El sistema puede cambiar de un estado a otro en respuesta a eventos.

* ¿Qué son eventos en una máquina de estados?

Son estímulos o condiciones que provocan que la máquina de estados cambie de un estado a otro, como entradas del usuario o el paso del tiempo.

* ¿Qué son las acciones?

Son tareas que se realizan cuando se entra en un estado, durante una transición entre estados, o mientras se permanece en un estado.

* ¿Cuál sería la estructura de un programa modelado con una máquina de estados?

### Definición de Estados:

Enumerar o definir los diferentes estados que el sistema puede tener.
Ejemplo: INIT, WAITING, PROCESSING, ERROR.

### Definición de Eventos:

Identificar los eventos que pueden ocurrir y que podrían causar un cambio de estado.
Ejemplo: input_received, timeout, error_detected.

### Transiciones:

Definir las reglas de transición que determinan cómo y cuándo se cambia de un estado a otro en respuesta a los eventos.
Ejemplo: if event == input_received and state == INIT: state = PROCESSING.

### Acciones:

Especificar las acciones que deben ejecutarse cuando se entra en un estado, durante una transición, o cuando se permanece en un estado.
Ejemplo: if state == PROCESSING: process_data().

### Bucle:

Un bucle continuo que escucha y maneja los eventos, actualiza los estados, y ejecuta las acciones correspondientes.
Ejemplo:

``` python
while True:
    event = get_event()
    if state == INIT:
        if event == input_received:
            state = PROCESSING
            process_data()
    elif state == PROCESSING:
        if event == timeout:
            state = WAITING
            wait_for_next_input()

```

### Gestión de Estados Finales:`

Si el sistema tiene estados terminales donde deja de funcionar, se debe manejar correctamente.
Ejemplo: if state == ERROR: handle_error_and_exit().

### EJEMPLO

``` python
from microbit import *
import utime

# Estados
STATE_INIT = 0
STATE_A = 1
STATE_B = 2

# Variables disponibles para todos los estados
current_state = STATE_INIT
start_time = 0

while True:
    # Psudoestado inicial
    if current_state == STATE_INIT:
        # Acciones para preparar el estado
        # siguiente:

        # Cambio de estado

    elif current_state == STATE_A:
        # Evento 1
        if condition:
            # Acciones para el evento

            # Acciones para preparar el estado siguiente:

            # Cambio de estado

        # Evento 2
        if condition:
            # Acciones para el evento

            # Acciones para preparar el estado siguiente:

            # Cambio de estado

      elif current_state == STATE_B:
          # Evento 1
          if condition:
              # Acciones para el evento

              # Acciones para preparar el estado siguiente:

              # Cambio de estado

          # Evento 2
          if condition:
            # Acciones para el evento

            # Acciones para preparar el estado siguiente:

            # Cambio de estado
```


## Experimento 9

### Enunciado

Imagina un programa para el micro:bit que muestra diferentes expresiones en la pantalla según un ciclo de tiempo, pero que también reacciona de inmediato si presionas un botón. Al iniciar, se muestra una cara feliz durante un segundo y medio. Después, el micro:bit cambia a una expresión sonriente que dura un segundo. Luego, aparece una cara triste durante dos segundos, y el ciclo vuelve a comenzar.

Sin embargo, si en cualquier momento se presiona el botón A mientras la cara feliz o la sonriente están en pantalla, el micro:bit interrumpe el ciclo y muestra inmediatamente la cara triste o feliz, respectivamente. Si se presiona el botón A mientras la cara triste está en pantalla, el dispositivo cambia a la expresión sonriente. Así, el programa combina una secuencia visual predefinida con la capacidad de responder rápidamente a la interacción del usuario.

### Programa

```
from microbit import *
import utime

STATE_INIT = 0
STATE_HAPPY = 1
STATE_SMILE = 2
STATE_SAD = 3

HAPPY_INTERVAL = 1500
SMILE_INTERVAL = 1000
SAD_INTERVAL = 2000

current_state = STATE_INIT
start_time = 0
interval = 0

while True:
    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        start_time = utime.ticks_ms()
        interval = HAPPY_INTERVAL
        current_state = STATE_HAPPY
    elif current_state == STATE_HAPPY:
        if button_a.was_pressed():
            # Acciones para el evento
            display.show(Image.SAD)
            # Acciones para el siguiente estado
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
            current_state = STATE_SAD
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            # Acciones para el evento
            display.show(Image.SMILE)
            # Acciones para el siguiente estado
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
    elif current_state == STATE_SMILE:
        if button_a.was_pressed():
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.SAD)
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
           current_state = STATE_SAD
    elif current_state == STATE_SAD:
        if button_a.was_pressed():
            display.show(Image.SMILE)
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
```

* Cómo es posible estructurar una aplicación usando una máquina de estados para poder atender varios eventos de manera concurrente?

  

* Vamos a construir juntos un experimento para explorar esta pregunta.




