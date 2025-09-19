
# Evidencias de la unidad 5

## Actividad 02
Al revisar en el serial terminal que ocurre con los datos enviado en binario en texto puedo encontrar el siguiente resultado:
<img width="1236" height="318" alt="image" src="https://github.com/user-attachments/assets/fd305631-4e24-47ec-88a0-fce8a6b3766f" />

Diferente al resultado de traducirlos a código hex:
<img width="1226" height="243" alt="image" src="https://github.com/user-attachments/assets/0f2d3f12-9fcd-43fd-b303-f63f706b85e0" />

Cuando se envian los datos en código binario encontramos esta diferencia en la información recibida, si esto se tratara de los datos enviado en ASCII como se hacia anteriormente se podrían traducir a texto pero los datos en binario no son interpretados por el programa, ¿Porque ocurre esto? investigando encuentro que esto es algo que hace parte de las diferencias entre ASCII y binario, en binario se están enviando los códigos directamente en unos y ceros, puede tener para el programa que lo interpreta una ambiguedad alta ya que necesita de donde tomar una referencia para interpretar, en cuanto a porqué con hex no pasa lo mismo es debido a que no debe realmente interpretar el texto respecto a nada, al cambiarlo a hex agrupa de a cuatro los bits y los convierte a su debido código hex. Para poder interpretar lo que pasa se necesita un sistema para decodificar los carácteres, lo que sería en este caso ASCII.

En cuanto a que ventaja le encontraria por ahora a usar binario en vez de ASCII solo sería una cuestión de seguridad, no hay manera de que un interpretador humano entienda que esta pasandose por ahí lo que podría servir para seguridad de un programa, también supongo que al saltarse el paso de traducir cada bit a texto legible la información puede viajar más rápido entre dispositivos. Y en cuanto a desventajas pues encuentro más, es algo que causa menos entendimiento para la persona que lo quiera leer, esto puede ser útil para seguridad pero para casos comunes lo único que puede causar es una dificultad al momento de comprender las señales recividas y enviadas por los programas.

Al cambiar por el nuevo código se envian 12 letras en código hex por cada vez que agito el micro:bit 
<img width="1243" height="260" alt="image" src="https://github.com/user-attachments/assets/549c9463-0f96-4a56-b9aa-e569e2faef5c" />

Cada vez que envia un emnsaje se ve como envia 12 digitos lo cual serían los 6 bytes esperados, debido a que cada byte es equivalente a 2 digitos hex, al analizar cada vez que se envia el mensaje se ve como envia algo así ``fe 14 02 cc 00 00`` viendo su orden y sabiendo la existencia del ``'>2h2B'`` se puede identificar como cumple con el 2 enteros cortos con dos bytes cada uno para los valores del acelerómetro (que en ese caso serían ``fe 14 02 cc`` siendo cada entero 2 digitos hex, mientras que con el estado a y b se envian 2 enteros cada uno de 1 byte, siendo estos en este caso ``00 00`` siendo cada par de ceros el valor de a y b respectivamente, significando que no estan siendo apretados, además se cumple con que primero se envien los de mayor valor. En cuanto a como se ven al ser negativos investigando encontre que aparecen como valores >= 0x8000 porque están en complemento a dos..

Ahora, cambiando al nuevo código que transmite tanto en binario como en ASCII se obtiene lo siguiente:

<img width="212" height="186" alt="image" src="https://github.com/user-attachments/assets/c8cf8346-6784-43f5-a088-4e8b5772c73e" />
<img width="825" height="64" alt="image" src="https://github.com/user-attachments/assets/0c829c7c-08ad-4b99-be26-a6891e564f59" />

Es ahora evidente como al pasarlo al hex los mensajes enviados son mucho más largos, no solo porque se envie dos veces, sino que dejando de lado el mensaje en bits se nota que se envia mucho más, incluso también quitando el mensaje que separa binario y ASCII, el mensaje en ASCII requiere muchos más bytes, demostrando asi una ventaja del lenguaje binario frente a el ASCII, lo cual lleva a preguntas como el ¿Cual es mejor entre ambos?, esto lleva a una respuesta y es que realmente cada uno tiene su fortaleza.

### ¿En que casos es mejor uno que el otro desde el punto del diseño, considerando diferentes factores como la legibilidad y eficiencia?
<a name="pregunta1"></a>
Pues esto es puede ser respondido teniendo en cuenta lo visto hasta ahora e investigando, El uso del ASCII permite una mayor legibilidad y entendimiento, es muchisimo más cómodo para comprender, facilita muchisimo el hecho de interpretar y depurar el contenido de un programa, ahora, como se vió anteriormente al cambiar por ultima vez el código y comparar uno a uno binario y ASCII se vió como este ultimo requiere mayor uso de bytes, esto puede en programas grandes afectar el rendimiento y la rapidez a comparación de el lenguaje binario.

El lenguaje binario es entonces más rápido al momento de enviar datos, los envia de manera más compacta y sencilla y lo hace más rápido, su problema por otro lado es su legibilidad, puede ser en varios casos poco eficiente debido a que puede tener más errores debido a que necesita conocer bien el formato, si no se conoce bien su estructura puede generar errores facilmente. En cuanto a diseño el ASCII es muy usado debido a que permitió estandarizar una forma de representar el texto en estos programas y es usado mayormente en todo programa que requiera algun tipo de interfaz permitiendo que aquellos trabajando en esto puedan hacerlo de manera más cómoda y sencilla, el binario por otro lado es de por si el lenguaje que utiliza todo sistema para funcionar y codificar los mensajes en esto permite como ya lo dije anteriormente más rapidez y rendimiento, es útil principalmente en programas que utilizan grandes cantidades de datos.

## Actividad 03
La razón de que ahora no sea necesario separar por espacios y saltos de lineas la información recibida es debido a que antes el mensaje estaba enviado en ASCII, este podia tener un tamaño variable en bytes y el programa no tenia forma de siempre saber cual era este por lo que necesitaba poder delimitarlo de alguna manera, esto no pasa en binario donde siempre tienen un tamaño de bytes delimitado.

Comparando el código como estaba antes a como estaba ahora respecto a la recepción de datos es notorio como antes habia que transformar y cuadrar de buena manera el texto recibido mientras que ahora por lo explicado anteriormente no es necesario todo este proceso.

<img width="832" height="171" alt="image" src="https://github.com/user-attachments/assets/99e7515a-6566-41b2-a4a2-9503d1632d0a" />

la consola presenta este error, supongo que es un error al momento de enviar los datos de la nueva forma, el programa no recibe bien los datos juntandolos mal, es por esto que necesita la guia que el framing le brinda, este permite que un programa pueda verificar que todos los paquetes de datos se envien bien y leerlos correctamente, pero esto me dio ganas de indagar más del tema y hacerme la pregunta:

### ¿Qué ventajas aporta el uso de un esquema de framing con cabecera y checksum en la comunicación binaria, en comparación con transmitir directamente los datos sin delimitadores, y en qué momentos puede volverse indispensable?
Primero que nada hay que analizar poco a poco como ayuda a que un programa funcione correctamente y que lo hace mejor a simplemente enviarlo directamente:

Primero que nada se cuenta con el header, este permite que realmente el que recibe pueda identificar con claridad el inicio de un paquete, incluso si se perdieron bytes o si los datos llegaron desfasados, esto asegura que el receptor pueda “sincronizarse” con el flujo de datos. Después esta el checksum, este funciona generando un valor en el original y en el destino que le permite verificar si ha sido alterado de alguna manera, esto lo vuelve muy útil en el framing que busca verificar que todo se este enviando y leyendo bien.

El framing es vital porque sin el el programa debería confiar totalmente que la información que recibe esta completa y organizada, lo cual no es siempre verdad, como en el caso del ejemplo que tenemos que sacaba error, no siempre hay alguien que este vigilando el código para saber si si se envian los datos correctamentey el framing sirve como esto que permite que exista la integridad, sincronización y robustez en los datos recibidos.

## Actividad 04
Primero que nada debo explicar que tengo un problema que parece complicado de solucionar que pasaba con el código ejemplo también, investigando veo que es un error quizas relacionado con el navegador pero por más que cambie no funciona, es por esto que el código que tengo tiene los cambios que creo permitirán funcionar al código en condiciones normales pero no puedo probarlo, soy conciente de que esto baja mi calificación en la rúbrica pero nada que hacer.
Error:
<img width="833" height="683" alt="image" src="https://github.com/user-attachments/assets/90925771-9066-44ec-a0e8-ef4856ef4f47" />

Ahora si, empezamos por lo primero, agrego la función de serial data que permite recibir los bytes acomulados
```` py
function readSerialData() {
  let available = port.availableBytes();
  if (available > 0) {
    let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
  }
````
esta parte del código es igual a la del evento ya que son cosas que no afectan mucho entre códigos, ahora lo siguiente es iniciar while que permite ir acomulando paquetes, este funciona esperando hasta que el paquete este completo analizando que si contenga los 8 bytes esperados y descarta hasta encontrar el header, esto permite que se tenga el paquete desde su inicio bien cuadrado y descarta datos que sean residuales, es esto lo que permite la robustez en el programa.
```` py
while (serialBuffer.length >= 8) {
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift();
      continue;
    }
````
Aún dentro del while prosigue lo siguiente: El programa va esperando que lleguen los 8 bytes, los separa y revisa con el checksum que si sea correcto, descartandolo si no y obteniendo los valores si si, es esta parte otra que es demasiado importante y permite que el framing sea algo vital, revisa que los datos que se reciban si sean correctos y de lo contrario los desecha, esto mantiene la integridad del código y al evitar estos desechos evita que se cuelen datos que lleven a los errores antes presentados.
```` py
if (serialBuffer.length < 8) break;

    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8);

    let dataBytes = packet.slice(1, 7);
    let receivedChecksum = packet[7];
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

    if (computedChecksum !== receivedChecksum) {
      console.log("Checksum error in packet");
      continue;
    }

    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0) + windowWidth / 2;
    microBitY = view.getInt16(2) + windowHeight / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);

    // Debug
    print(
      `microBitX:${microBitX} microBitY:${microBitY} A:${microBitAState} B:${microBitBState}`
    );
  }
````
Además se agrega el ``readSerialData();`` y arriba del todo el ``let serialBuffer = [];`` que permiten leer los datos binarios y crear el buffer que va a almacenar todo respectivamente. El código final realmente no cambia mucho y sus cambios son parecidos al del ejemplo, sería así:
```` py
let serialBuffer = [];

let c;
let lineModuleSize = 0;
let angle = 0;
let angleSpeed = 1;
const lineModule = [];
let lineModuleIndex = 0;
let clickPosX = 0;
let clickPosY = 0;

function preload() {
  lineModule[1] = loadImage("02.svg");
  lineModule[2] = loadImage("03.svg");
  lineModule[3] = loadImage("04.svg");
  lineModule[4] = loadImage("05.svg");
}

let port;
let connectBtn;
let microBitConnected = false;

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAIT_MICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};
let appState = STATES.WAIT_MICROBIT_CONNECTION;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(255);

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(0, 0);
  connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}

function updateButtonStates(newAState, newBState) {
  // Evento A PRESSED
  if (newAState === true && prevmicroBitAState === false) {
    lineModuleSize = random(50, 160);
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }
  // Evento B RELEASED
  if (newBState === false && prevmicroBitBState === true) {
    c = color(random(255), random(255), random(255), random(80, 100));
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

function readSerialData() {
  let available = port.availableBytes();
  if (available > 0) {
    let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
  }

  
  while (serialBuffer.length >= 8) {
    if (serialBuffer[0] !== 0xaa) {
      serialBuffer.shift(); // descarta hasta encontrar el header
      continue;
    }

    if (serialBuffer.length < 8) break;

    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8);

    let dataBytes = packet.slice(1, 7);
    let receivedChecksum = packet[7];
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

    if (computedChecksum !== receivedChecksum) {
      console.log("Checksum error in packet");
      continue;
    }

    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0) + windowWidth / 2;
    microBitY = view.getInt16(2) + windowHeight / 2;
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
    updateButtonStates(microBitAState, microBitBState);

    // Debug
    print(
      `microBitX:${microBitX} microBitY:${microBitY} A:${microBitAState} B:${microBitBState}`
    );
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

function draw() {
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");
  }

  switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION:
      if (microBitConnected === true) {
        print("Microbit ready to draw");
        strokeWeight(0.75);
        c = color(181, 157, 0);
        noCursor();
        port.clear();
        prevmicroBitAState = false;
        prevmicroBitBState = false;
        appState = STATES.RUNNING;
      }
      break;

    case STATES.RUNNING:
      if (microBitConnected === false) {
        print("Waiting microbit connection");
        cursor();
        appState = STATES.WAIT_MICROBIT_CONNECTION;
        break;
      }

      
      readSerialData();

      if (microBitAState === true) {
        let x = microBitX;
        let y = microBitY;

        if (keyIsPressed && keyCode === SHIFT) {
          if (abs(clickPosX - x) > abs(clickPosY - y)) {
            y = clickPosY;
          } else {
            x = clickPosX;
          }
        }

        push();
        translate(x, y);
        rotate(radians(angle));
        if (lineModuleIndex != 0) {
          tint(c);
          image(lineModule[lineModuleIndex], 0, 0, lineModuleSize, lineModuleSize);
        } else {
          stroke(c);
          line(0, 0, lineModuleSize, lineModuleSize);
        }
        angle += angleSpeed;
        pop();
      }
      break;
  }
}

function keyPressed() {
  if (keyCode === UP_ARROW) lineModuleSize += 5;
  if (keyCode === DOWN_ARROW) lineModuleSize -= 5;
  if (keyCode === LEFT_ARROW) angleSpeed -= 0.5;
  if (keyCode === RIGHT_ARROW) angleSpeed += 0.5;
}

function keyReleased() {
  if (key === "s" || key === "S") {
    let ts =
      year() +
      nf(month(), 2) +
      nf(day(), 2) +
      "_" +
      nf(hour(), 2) +
      nf(minute(), 2) +
      nf(second(), 2);
    saveCanvas(ts, "png");
  }
  if (keyCode === DELETE || keyCode === BACKSPACE) background(255);

  if (key === "d" || key === "D") {
    angle += 180;
    angleSpeed *= -1;
  }

  if (key === "1") c = color(181, 157, 0);
  if (key === "2") c = color(0, 130, 164);
  if (key === "3") c = color(87, 35, 129);
  if (key === "4") c = color(197, 0, 123);

  if (key === "5") lineModuleIndex = 0;
  if (key === "6") lineModuleIndex = 1;
  if (key === "7") lineModuleIndex = 2;
  if (key === "8") lineModuleIndex = 3;
  if (key === "9") lineModuleIndex = 4;
}
````
## Autoevaluación y evidencias:
Mi nota propuesta: 

Criterio 1: profundidad de la indagación

Mi autoevaluación: me sitúo en el nivel Excelente (nota:4,8) porque…
Evidencias: Tanto en la [actividad 02](#pregunta1) como en la activdad 03 me surgieron preguntas que pude resolver investigando y analizando lo obtenido en clase, estas preguntas iban más allá del qué y se preguntaban el porqué del diseño y en comparar en que situaciones y bajo que casos eran mejor ciertas estrategias y métodos de envio de datos.

