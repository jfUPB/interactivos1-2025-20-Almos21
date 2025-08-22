# Unidad 3


## 🛠 Fase: Apply

### Actividad 06
````py
let PASSWORD = ['A', 'B', 'A'];
let inputKeys = [];
let keyIndex = 0;
let count = 20;
let startTime;
let state = "CONFIG";

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(32);
  startTime = millis();
}

function draw() {
  background(20);

  if (state === "CONFIG") {
    fill(200);
    text("Configuración \nTiempo: " + count, width / 2, height / 2);
  } 
  
  else if (state === "ARMED") {
    fill(255, 50, 50);
    text("ARMED\nTiempo: " + count, width / 2, height / 2);

    if (millis() - startTime > 1000) {
      startTime = millis();
      count--;
      if (count <= 0) {
        state = "EXPLODED";
      }
    }
  } 
  
  else if (state === "EXPLODED") {
    background(255, 0, 0);
    fill(0);
    text(" BOOM ", width / 2, height / 2);
  }
}

function keyPressed() {
  let keyValue = key.toUpperCase();
  
  if (state === "CONFIG") {
    if (keyValue === "A") {
      count = min(count + 1, 60);
    } 
    else if (keyValue === "B") {
      count = max(10, count - 1);
    } 
    else if (keyValue === "S") { 
      startTime = millis();
      state = "ARMED";
    }
  } 
  
  else if (state === "ARMED") {
    if (keyValue === "A" || keyValue === "B") {
      inputKeys.push(keyValue);
      keyIndex++;

      if (keyIndex === PASSWORD.length) {
        let passOk = true;
        for (let i = 0; i < PASSWORD.length; i++) {
          if (inputKeys[i] !== PASSWORD[i]) {
            passOk = false;
            break;
          }
        }

        if (passOk) {
          count = 20;
          state = "CONFIG";
        }
        inputKeys = [];
        keyIndex = 0;
      }
    }
  } 
  
  else if (state === "EXPLODED") {
    if (keyValue === "T") { 
      count = 20;
      startTime = millis();
      state = "CONFIG";
    }
  }
}
````
Este sería el código pasado a p5.js, este aprovecha la función keypressed para leer la tecla presionada y después dependiendo del estado en el que este realiza algo distinto, simulando el mismo código hecho anteriormente en el micro bit. se vale de un for que no rompe la concurrencia para leer la contraseña y entender si esta correcta para permitir reiniciar o continuar con el conteo.

### Actividad 07
Código del micro:bit para poder controlar el p5.js
```` js
from microbit import *
import utime

while True:
    if button_a.was_pressed():
        uart.write('A\n')
    elif button_b.was_pressed():
        uart.write('B\n')
    elif accelerometer.was_gesture('shake'):
        uart.write('S\n')
    elif pin_logo.is_touched():
        uart.write('T\n')

    utime.sleep_ms(100)
````
código de p5.js para controlar esto:
```` py
let serial;
let portName = ''; 
let PASSWORD = ['A', 'B', 'A'];
let inputKeys = [];
let keyIndex = 0;
let count = 20;
let startTime;
let state = "CONFIG";

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(32);
  startTime = millis();

 
  serial = new p5.SerialPort();
  serial.list(); 
  serial.openPrompt(); 
  serial.on('data', serialEvent); 
  serial.on('error', (err) => {
    console.error("Serial error: " + err);
  });
}

function draw() {
  background(20);

  if (state === "CONFIG") {
    fill(200);
    text("Configuración \nTiempo: " + count, width / 2, height / 2);
  } 
  
  else if (state === "ARMED") {
    fill(255, 50, 50);
    let elapsed = floor((millis() - startTime) / 1000);
    let remaining = max(count - elapsed, 0);
    text("ARMED\nTiempo: " + remaining, width / 2, height / 2);

    if (remaining <= 0) {
      state = "EXPLODED";
    }
  } 
  
  else if (state === "EXPLODED") {
    background(255, 0, 0);
    fill(0);
    text("  BOOM  ", width / 2, height / 2);
  }
}


function serialEvent() {
  let keyValue = serial.readLine().trim().toUpperCase();
  if (keyValue === "") return;

  console.log("Recibido:", keyValue);

  if (state === "CONFIG") {
    if (keyValue === "A") {
      count = min(count + 1, 60);
    } 
    else if (keyValue === "B") {
      count = max(10, count - 1);
    } 
    else if (keyValue === "S") { 
      startTime = millis();
      state = "ARMED";
    }
  } 
  
  else if (state === "ARMED") {
    if (keyValue === "A" || keyValue === "B") {
      inputKeys.push(keyValue);
      keyIndex++;

      if (keyIndex === PASSWORD.length) {
        let passOk = true;
        for (let i = 0; i < PASSWORD.length; i++) {
          if (inputKeys[i] !== PASSWORD[i]) {
            passOk = false;
            break;
          }
        }

        if (passOk) {
          count = 20;
          state = "CONFIG";
        }
        inputKeys = [];
        keyIndex = 0;
      }
    }
  } 
  
  else if (state === "EXPLODED") {
    if (keyValue === "T") { 
      count = 20;
      startTime = millis();
      state = "CONFIG";
    }
  }
}
````
https://editor.p5js.org/Almos21/full/XtewGSTuq
