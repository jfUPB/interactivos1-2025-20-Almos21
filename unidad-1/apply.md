# Unidad 1

## 🛠 Fase: Apply

### Actividad 05


### Actividad 06
[Código al editor de p5.js](https://editor.p5js.org/Almos21/sketches/SdAkdeTqZ)

Código de mirco:bit editor:
``` py
from microbit import *

uart.init(baudrate=115200)

while True:

    if button_a.is_pressed():
        uart.write('A')
    if button_b.is_pressed():
        uart.write('B')
    

    sleep(100)
```
Código de p5.js
``` js
let port;
let connectBtn;
let connectionInitialized = false;
let x = 200;
 
function setup() {
    createCanvas(400, 400);
     background(196, 193, 120);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
}
 
function draw() {
   background(196, 193, 120);
   if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }
 
  if (port.availableBytes() > 0) {
      let dataRx = port.read(1);
      if (dataRx == "A") {
        x -= 10;
      } else if (dataRx == "B") {
        x += 10;
      }
        }
  fill(100,5,70) 
  circle(x, 200, 50);
 
        if (!port.opened()) {
            connectBtn.html("Connect to micro:bit");
        } else {
            connectBtn.html("Disconnect");
        }
}
 
function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
      connectionInitialized = false;
    } else {
        port.close();
    }
}
```
