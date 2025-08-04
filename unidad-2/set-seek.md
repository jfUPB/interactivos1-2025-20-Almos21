# Unidad 2

## 🔎 Fase: Set + Seek

un estado esta esperando a un evento

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
