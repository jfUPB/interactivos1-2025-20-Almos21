# Unidad 2


## 🛠 Fase: Apply
### Actividad 04
<img width="721" height="741" alt="Diagrama sin título drawio" src="https://github.com/user-attachments/assets/27b6de2c-76c3-4f2a-9945-cf09ca5121db" />

### Actividad 05
Este es el cóigo que sigue la lógica de el diagrama anterior, logra cumplir con las condiciones de sumar y restar los valores del tiempo, armar la bomba, contar hasta el valor necesario, representar la cuenta con las lineas led y despues representar la explosión con la calaver y el sonido.
```` py
from microbit import *
import utime
import speech

STATE_INIT = 0
STATE_ARMED = 1
STATE_KABOOM = 2

current_state = STATE_INIT 
start_time = 20000

while True:
    if current_state == STATE_INIT:
        if button_a.was_pressed():
            start_time += 1000
            if start_time>60000:
                start_time= 60000
        elif button_b.was_pressed():
            start_time-= 1000
            if start_time < 10000:
                start_time = 10000
            print(start_time)
        elif accelerometer.was_gesture('shake'):
            current_state = STATE_ARMED
            print(start_time)
    if current_state == STATE_ARMED:
        divide_time = start_time
        start_tick = utime.ticks_ms()

        for i in range (5):
            while utime.ticks_diff(utime.ticks_ms(), start_tick) <divide_time * (i+1):
                pass
            for col in range(5):
                display.set_pixel(col, i, 9)
        current_state = STATE_KABOOM
    if current_state == STATE_KABOOM:
        display.show(Image.SKULL)
        speech.say('BOOM')
        if button_b.was_pressed() or button_b.was_pressed():
            current_state = STATE_INIT
            display.clear()
````
#### La definición de los vectores de prueba básicos que permiten verificar el correcto funcionamiento del programa.
- El primero sería la comprobación de la suma y resta de tiempo, aqui tecnicamente serían dos pero con el mismo funcionamiento: presionar A o B, pasando del estado incicial ````STATE_INIT```` a este mismo estado pero con ```start_time```  disminuyendo o aumentando su valor dentro de los máximos y minimos definidos.
- El segundo sería agitar el micro:bit lo cual debería pasar del estado inicial ````STATE_INIT```` a el estado ```STATE_ARMED```
- El tercero es que al entrar al estado ```STATE_ARMED``` se enciendan las filas de LED individalmente cada ```start_time```/5 ms y pasando al estado final ```STATE_KABOOM```
- Depués el cuarto vector de prueba sería ver que al entrar al estado ```STATE_KABOOM``` la imagen de la calavera aparezca y el sonido de BOOM suene, todo esto finalizando igual en el estado ```STATE_KABOOM```
- Por último solo queda probar que al estar en el estado ```STATE_KABOOM``` y presionar A o B se regrese al estado ````STATE_INIT````


