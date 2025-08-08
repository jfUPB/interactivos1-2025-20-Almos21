# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 01
#### Describe detalladamente cómo funciona el ejemplo.
En el código mostrado en la guía se crea una clase pixel que declara un pixel con varios parámetros que definen sus características y estado, este se va actualizando en el update, lo que permite que este se encienda y apague entre intervalos de tiempo cambiando entre los estados init y waittimeout, al final del código se instancian 2 de estos y en el ciclo principal se les indica que se actualicen constantemente.
#### ¿Cuáles son los estados en el programa?
Los estados que se presentan son Init y Waittimeout
#### ¿Cuáles son los eventos/inputs en el programa?
El programa esta constantemente comparando los tiempos y al identificar que el intervalo designado ha pasado entonces cambia el estado, por ende aqui el tiempo funciona como in imput para el programa.
#### ¿Cuáles son las acciones en el programa?
Las acciones que realiza el programa serían encender y apagar las luces, calcular los tiempos y actualizar los estados de los objetos.

### Actividad 02
Aquí se buscaba hacer un código para crear un semáforo con los estados.
````py
from microbit import *
import utime

class TrafficLight:
    def __init__(self):
        self.state = "Rojo"
        self.start_time = utime.ticks_ms()

    def update(self):
        current_time = utime.ticks_ms()
        elapsed = utime.ticks_diff(current_time, self.start_time)

        if self.state == "Rojo":
            self.show_rojo()
            if elapsed > 3000:
                self.state = "Amarillo"
                self.start_time = current_time
#pongan mitski
        elif self.state == "Verde":
            self.show_verde()
            if elapsed > 3000:
                self.state = "Rojo"
                self.start_time = current_time

        elif self.state == "Amarillo":
            self.show_amarillo()
            if elapsed > 1000:
                self.state = "Verde"
                self.start_time = current_time

    def show_rojo(self):
        display.clear()
        display.set_pixel(2, 0, 9)  

    def show_verde(self):
        display.clear()
        display.set_pixel(2, 2, 9)  

    def show_amarillo(self):
        display.clear()
        display.set_pixel(2, 1, 9) 


traffic_light = TrafficLight()
while True:
    traffic_light.update()
    sleep(100)

````
#### Identifica los estados, eventos y acciones en tu código.
Los estados son Rojo, Verde y Amarillo que encienden y apagan los diferentes pixeles representando los colores del semáforo.
Los eventos son los cambios en el tiempo, son estos los que determinan cuando un estado empieza, siendo 3 segundos entre rojo y amarillo y 1 segundo entre amarillo y verde, replicando su tiempo en la vida real.
Por último las acciones serían el limpiar la pantalla y limpiar un nuevo pixel cada vez que se empiezan los estados.

### Actividad 03
#### Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.
En el código entregado de expresiones lo que permite que se realizen a la vez varias tareas es el bucle y el uso del tiempo, en este código son estas cosas las que permiten a el programa simular un comportamiento paralelo, dentro del bucle todas las acciones se estan revisando y cambiando entre sí constantemente.
#### Identifica los estados, eventos y acciones en el programa.
Los estados serán: el estado incial, el estado feliz, el estado sonriente y el estado triste. 
En cuanto a los eventos se pueden indentificar el presionar el botón y el paso del tiempo, que son los que permiten a los estados intercambiar entre si.
Las acciones son mostrar imagenes en el microbit, reiniciar el conteo del tiempo, definir los intervalos y cambiar entre los estados.

#### Describe y aplica al menos 3 vectores de prueba para el programa. 
##### Primer vector de prueba, transición entre HAPPY a SMILE sin presionar ningun botón
Para este primero las condiciones iniciales serían: los estados cambian así: ````STATE_INIT```` → entra a ````STATE_HAPPY```` y pasa un tiempo sin presionar el botón A
el evento sería entonces que pase el tiempo designado sin presionar el botón A, para esto esta 1500 ms sin presionar.
Los resultados que se esperan son: que la imagen cambie de HAPPY a SMILE, el estado actual seqa ````STATE_SMILE````, se reinicie el ````start_time```` y que nuestro nuevo intervalo sea ````SMILE_INTERVAL = 1000````, esto se comprueba eventualmente y nos da como resultado que si funciona.
##### Segundo vector de pureba, Botón A presionado en estado SMILE
Las condiciones iniciales serían: el estado actual ````STATE_SMILE ```` y la persona presiona botón A, y entonces aqui el evento resultante sería ````button_a.was_pressed()```` devolviendo el valor true.
Entonces aquí los resultados esperados serían: La imagen cambia a HAPPY, después el estado cambia a ````STATE_HAPPY```` y el intervalo que tenemos cambia a 1500 ms para que por último se  reinicie````start_time````.
Finalmente el resultado observado es que estas condiciones se cumple.
##### Tercer vector de prueba, Presionar botón A en estado HAPPY
En este caso las condiciones iniciales que tenemos son  el estado: ````STATE_HAPPY```` y el botón A presionado antes de que pasen 1500 ms., esto tambien generaría el evento de ````button_a.was_pressed()```` devolviendo el valor true.
Aquí los resultados esperados son la imagen cambiando a SAD, el estado cambiando a ````STATE_SAD````, el intervalo a ````SAD_INTERVAL = 2000```` y por último que se reinicie ````start_time````.







