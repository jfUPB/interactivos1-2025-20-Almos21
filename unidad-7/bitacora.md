
# Evidencias de la unidad 7

## Actividad 01
- URL que obtuve: ``https://zqdlcf9w-3000.use2.devtunnels.ms/`` creo que se necesita una diferente porque el proceso de conexión al tratarse de un dispositivo externo debe ser diferente y más complicada, y no depende unicamente de la IP de un solo dispositivo.
- Nmp install y start se encargan de descargar todas las carpetas y dependencias de la ubicación asignada e iniciar el servidor, permitiendole empezar a escuchar.
- Estos eran los mensajes, eran bastante iguales entre si .com/user-attachments/assets/376ee0d8-cc54-4510-bb3d-53d4f9e3c8c3" />

- Me funcionó correctamente, no noté que hubiera este retraso.

## Actividad 02
- DevTunnels es necesario ya que en normalmente el localhost que obtenemos se refiere a la máquina en la que es reproducido, esto significa que el url que utilizamos anteriormente no funcionará para conectar dos dispositivos, existen otras soluciones para conectarlos pero se verían limitadas por el uso de una misma red y cualquier firewall, en general la conexión no es del todo segura, DevTunnels soluciona esto logrando crear un espacio seguro y accesible de manera sencilla.
- Esta función identifica cuando se esta tocando la pantalla con el dedo, el threshold permite que solo tome en cuenta movimientos lo suficientemente significativos, de lo contrario culquier pequeño movimiento o vibración del dedo moveria el objeto, haciedo que se vea tembloroso y extraño además de llenar al sistema con demasiadas instrucciones.
- DevTunnels permite utilizar los dos dispositivos de manera segura y sencilla sin importat si estan en una misma red ni tampoco importat firewalls existentes, al contrario de usar la IP local que es mucho más restringida e incomoda de usar.
- <img width="1310" height="840" alt="image" src="https://github.com/user-attachments/assets/53080d04-c148-46db-b61f-9ac9fb5346eb" />

<img width="742" height="1600" alt="image" src="https://github.com/user-attachments/assets/2c3e011a-511a-4b96-89ec-cb0ba4be13ef" />

## Actividad 03
- ``express.static('public')`` le indica a Express que entregue archivos estáticos proveientes de la carpeta ``public`` este se activa cuando el servidor pide ``http://localhost:3000/index.html``  y entonces Express busca por ``public/index.html`` sin necesidad de que definamos rutas manuales, esto se relaciona con ``app.get('/ruta', ...)`` ya que tambien optiene algo que se pide pero la diferencia es que esta última define una ruta dinámica, cuando llega una petición GET a ``/ruta``, la función callback la maneja.
- Primero que nada el navegador captura el menaje movil que recibe y los envia al servidor, el servidor recibe el evento ``message`` y envia un callback con este. Aqui el servidor lo loggea y usa ``socket.broadcast.emit('message', message)`` para retransmitir el mensaje a todos los demás clientes conectados excepto el que lo envió. Se envia con este y con io.emit o socket.emit  debido a que estos o envian de vuelta al socket actual (o sea socket.emit('message', ...) ) o a todos incluyendo al actual (io.emit('message', ...)), mientras que socket.broadcast.emit lo hace con todos menos el actual ya que no necesitamos que el cliente reciba de nuevo el mensaje que acaba de enviar.
- En mensaje lo reciben todos menos el movil que lo envia (por lo explicado en la pregunta pasada)
- Los console.log proporcionan datos como las conexiones y desconexiones de clientes, ver el contenido de lo que envian y frecuencias de los eventos, además de saber quien es el cliente que envia todo esto por el socket.id.

## Actividad 05
El diseño que pensé para esta actividad fue usar la canción "Once more to see you" de Mitski representando visualmente sus instrumentos y la vibra de la canción, esto separando entre los golpes fuertes y bajos de los tambores y los destellos por sonidos más agudos, además de la letra de la canción y un fondo que pasa de un atardecer (referencia al descrito al inicio de la canción) a la noche y más tarde la mañana, el usuario puede usar el mobil para desactivar las representaciones visuales de los instrumentos por separado además puede mover su dedo por la pantalla para hacer como ondas de agua. Lo realicé con ayuda de claude

Esto es como se ve en el desktop

<img width="1919" height="1068" alt="image" src="https://github.com/user-attachments/assets/4e829f4e-6088-41ba-b7a5-11cf71158f3f" />

Y esto en el mobil (un Ipad en este caso)

<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/b912be6c-9275-44b6-97b7-42fb2398d2f2" />

Y en este video esta mostrado como interactuan y como se ve mientras se reproduce
[Prueba actividad 05](https://youtu.be/yll4ZvHB7ZM)

Los códigos usados son:
Desktop Index
```` js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mitski Visual - Desktop</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.7.0/p5.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.7.0/addons/p5.sound.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/4.5.4/socket.io.min.js"></script>
    <style>
        body { 
            margin: 0; 
            padding: 0; 
            overflow: hidden;
        }
        canvas { 
            display: block; 
        }
    </style>
</head>
<body>
    <script src="sketch.js"></script>
</body>
</html>
````
Desktop sketch.js

````js
let socket;
let audio;
let fft;
let amplitude;
let musicTime = 0;
let songDuration = 145; // Duración aproximada en segundos (ajustar según la canción)
let audioLoaded = false;
let useSimulatedAudio = false;



// Estado de capas
let layers = {
    drums: true,
    bass: true,
    cymbals: true,
    lyrics: true
};

// Visuales
let drumWaves = [];
let bassStrings = [];
let cymbalFlashes = [];
let touchRipples = [];

// Letras (agregar fragmentos respetando derechos de autor)
// Timestamps aproximados para "Once More to See You" (puedes afinarlos)
let lyricsTimeline = [
  { time: 13.0, text: "In the rearview mirror, I saw the setting sun on your neck" },
  { time: 26.0, text: "And felt the taste of you bubble up inside me" },
  { time: 33.0, text: "But with everybody watching us, our every move" },
  { time: 41.0, text: "We do have reputations" },
  { time: 46.0, text: "We keep it secret" },
  { time: 51.0, text: "Won't let them have it" },
  { time: 62.0, text: "So come inside and be with me, alone with me" },
  { time: 70.0, text: "Alone, with me alone" },
  { time: 74.0, text: "If you would let me give you pinky promise kisses" },
  { time: 83.0, text: "Then I wouldn't have to scream your name" },
  { time: 88.0, text: "Atop of every roof in the city of my heart" },
  { time: 95.0, text: "If I could see you" },
  { time: 100.0, text: "Once more to see you" },
  { time: 112.0, text: "Come inside and be with me, alone with me" },
  { time: 118.0, text: "Alone, with me alone" },
  { time: 124.0, text: "If you would let me give you pinky promise kisses" },
  { time: 132.0, text: "Then I wouldn't have to scream your name" },
  { time: 136.0, text: "Atop of every roof in the city of my heart" },
  { time: 144.0, text: "If I could see you" },
  { time: 149.0, text: "Once more to see you" },
  { time: 154.0, text: "If I could see you" },
  { time: 159.0, text: "Once more to see you" }
];
let currentLyricIndex = 0;
let lyricTimer = 0;

function preload() {
    // Cargar audio - ruta relativa desde desktop/
    audio = loadSound('../once_more_to_see_you.mp3', 
        () => console.log('✅ Audio loaded'),
        (err) => {
            console.error('❌ Error loading audio:', err);
            console.log('Trying alternative path...');
        }
    );
}

function setup() {
    createCanvas(windowWidth, windowHeight);
    
    // Configurar análisis de audio
    fft = new p5.FFT(0.8, 256);
    amplitude = new p5.Amplitude();
    
    // Conexión socket
    socket = io();
    
    socket.on('connect', () => {
        console.log('✅ Connected to server');
    });
    
    socket.on('layersState', (data) => {
        console.log('📊 Layers state updated:', data);
        layers = data;
    });
    
    socket.on('touchLyrics', (data) => {
        if (data && data.x && data.y) {
            // Convertir coordenadas del móvil al desktop
            let x = map(data.x, 0, data.width, 0, width);
            let y = map(data.y, 0, data.height, 0, height);
            createRipple(x, y);
        }
    });
    
    socket.on('disconnect', () => {
        console.log('❌ Disconnected from server');
    });
    
    // Inicializar cuerdas de bajo
    for (let i = 0; i < 8; i++) {
        bassStrings.push(new BassString(i));
    }
    
    // Click para iniciar audio (necesario en navegadores modernos)
    textAlign(CENTER, CENTER);
    textSize(32);
    fill(255);
    text('Click to start', width / 2, height / 2);
}

function mousePressed() {
    if (!audio.isPlaying()) {
        audio.loop();
        console.log('🎵 Music started');
    }
}

function draw() {
    drawSkyGradient();
    
    // Obtener tiempo de música
    if (audio.isPlaying()) {
        musicTime = audio.currentTime();
    }
    let progress = musicTime / songDuration;
    
    // Variables para datos de audio
    let spectrum, level, bass, treble, mid;
    
    // Obtener datos de audio
    if (audio.isPlaying()) {
        spectrum = fft.analyze();
        level = amplitude.getLevel();
        bass = fft.getEnergy("bass");
        treble = fft.getEnergy("treble");
        mid = fft.getEnergy("mid");
    } else {
        // Valores por defecto cuando no hay audio
        bass = 0;
        treble = 0;
        mid = 0;
        level = 0;
    }
    
    // Dibujar capas según el estado
    if (layers.bass) {
        drawBassStrings(bass);
    }
    
    if (layers.drums) {
        drawDrumWaves(level);
    }
    
    if (layers.cymbals) {
        drawCymbalFlashes(treble);
    }
    
    if (layers.lyrics) {
        drawLyrics();
    }
    
    // Dibujar efectos de toque
    drawTouchRipples();
    
    // Mostrar instrucción si no está reproduciendo
    if (!audio.isPlaying()) {
        push();
        fill(0, 0, 0, 150);
        rect(0, 0, width, height);
        fill(255);
        textAlign(CENTER, CENTER);
        textSize(32);
        text('🎵 Click to start music', width / 2, height / 2);
        pop();
    }
}

function drawSkyGradient() {
    let progress = (musicTime / songDuration) % 1;
    
    // Colores del atardecer a la noche y amanecer
    let sunsetTop = color(255, 100, 50);
    let sunsetBottom = color(255, 180, 100);
    let nightTop = color(10, 10, 40);
    let nightBottom = color(40, 20, 60);
    let dawnTop = color(255, 200, 150);
    let dawnBottom = color(135, 206, 235);
    
    let topColor, bottomColor;
    
    if (progress < 0.3) {
        // Atardecer
        let t = progress / 0.3;
        topColor = lerpColor(sunsetTop, nightTop, t);
        bottomColor = lerpColor(sunsetBottom, nightBottom, t);
    } else if (progress < 0.7) {
        // Noche
        topColor = nightTop;
        bottomColor = nightBottom;
    } else {
        // Amanecer
        let t = (progress - 0.7) / 0.3;
        topColor = lerpColor(nightTop, dawnTop, t);
        bottomColor = lerpColor(nightBottom, dawnBottom, t);
    }
    
    // Dibujar gradiente
    for (let y = 0; y < height; y++) {
        let inter = map(y, 0, height, 0, 1);
        let c = lerpColor(topColor, bottomColor, inter);
        stroke(c);
        line(0, y, width, y);
    }
    
    // Dibujar sol/luna
    let celestialY = map(progress, 0, 1, height - 100, 100);
    let celestialX = width / 2 + cos(progress * TWO_PI - HALF_PI) * width * 0.3;
    
    noStroke();
    if (progress < 0.3 || progress > 0.7) {
        // Sol
        fill(255, 220, 100, 200);
        circle(celestialX, celestialY, 80);
        // Resplandor
        fill(255, 200, 100, 50);
        circle(celestialX, celestialY, 120);
    } else {
        // Luna
        fill(240, 240, 255, 150);
        circle(celestialX, celestialY, 60);
    }
}

function drawDrumWaves(level) {
    // Crear nuevas ondas en los golpes fuertes
    if (level > 0.1 && frameCount % 5 === 0) {
    drumWaves.push({
        x: width / 2,
        y: height / 2,
        radius: 0,
        maxRadius: 400,
        alpha: 255,
        thickness: 2 + level * 8
    });
}

    // Actualizar y dibujar ondas
    for (let i = drumWaves.length - 1; i >= 0; i--) {
        let wave = drumWaves[i];
        wave.radius += 5;
        wave.alpha -= 3;
        
        if (wave.alpha <= 0 || wave.radius > wave.maxRadius) {
            drumWaves.splice(i, 1);
            continue;
        }
        
        noFill();
        stroke(255, 255, 200, wave.alpha);
        strokeWeight(wave.thickness);
        circle(wave.x, wave.y, wave.radius * 2);
    }
}

function drawBassStrings(bassLevel) {
    for (let string of bassStrings) {
        string.update(bassLevel);
        string.display();
    }
}

function drawCymbalFlashes(trebleLevel) {
    // Crear destellos cuando hay energía en agudos
    if (trebleLevel > 90 && random(1) < 0.3) {
    cymbalFlashes.push({
        x: random(width),
        y: random(height),
        size: random(30, 80),
        alpha: 255,
        hue: random(180, 220)
    });
}


    
    // Actualizar y dibujar destellos
    for (let i = cymbalFlashes.length - 1; i >= 0; i--) {
        let flash = cymbalFlashes[i];
        flash.alpha -= 15;
        flash.size += 2;
        
        if (flash.alpha <= 0) {
            cymbalFlashes.splice(i, 1);
            continue;
        }
        
        noStroke();
        fill(flash.hue, 200, 255, flash.alpha);
        circle(flash.x, flash.y, flash.size);
        
        // Destello cruzado
        stroke(flash.hue, 200, 255, flash.alpha);
        strokeWeight(2);
        line(flash.x - flash.size/2, flash.y, flash.x + flash.size/2, flash.y);
        line(flash.x, flash.y - flash.size/2, flash.x, flash.y + flash.size/2);
    }
}

function drawLyrics() {
  // Determinar cuál línea debe mostrarse en el tiempo actual
  for (let i = 0; i < lyricsTimeline.length; i++) {
    if (musicTime >= lyricsTimeline[i].time &&
        (i === lyricsTimeline.length - 1 || musicTime < lyricsTimeline[i + 1].time)) {
      currentLyricIndex = i;
      break;
    }
  }

  push();
  textAlign(CENTER, CENTER);
  noStroke();

  let fadeRange = 2; // número de líneas antes y después para mostrar con fade
  for (let i = max(0, currentLyricIndex - fadeRange);
       i <= min(lyricsTimeline.length - 1, currentLyricIndex + fadeRange);
       i++) {
    let offset = i - currentLyricIndex;
    let y = height / 2 + offset * 60;
    let alpha = map(abs(offset), 0, fadeRange, 255, 40);
    let size = map(abs(offset), 0, fadeRange, 48, 24);

    textSize(size);
    fill(255, 255, 255, alpha);
    text(lyricsTimeline[i].text, width / 2, y);
  }

  pop();
}

function drawTouchRipples() {
    for (let i = touchRipples.length - 1; i >= 0; i--) {
        let ripple = touchRipples[i];
        ripple.radius += 4;
        ripple.alpha -= 5;
        
        if (ripple.alpha <= 0) {
            touchRipples.splice(i, 1);
            continue;
        }
        
        // Efecto de agua
        noFill();
        stroke(100, 150, 255, ripple.alpha);
        strokeWeight(3);
        
        // Múltiples ondas
        for (let j = 0; j < 3; j++) {
            circle(ripple.x, ripple.y, (ripple.radius + j * 20) * 2);
        }
        
        // Distorsión en letras cercanas
        push();
        translate(ripple.x, ripple.y);
        let distortion = map(ripple.alpha, 0, 200, 0, 20);
        rotate(sin(ripple.radius * 0.1) * 0.1);
        pop();
    }
}

function createRipple(x, y) {
    touchRipples.push({
        x: x,
        y: y,
        radius: 0,
        alpha: 200
    });
}

class BassString {
    constructor(index) {
        this.index = index;
        this.x = (width / 9) * (index + 1);
        this.points = [];
        this.numPoints = 50;
        
        for (let i = 0; i < this.numPoints; i++) {
            this.points.push({
                y: map(i, 0, this.numPoints, 0, height),
                offset: 0
            });
        }
    }
    
    update(bassLevel) {
        let time = millis() * 0.001;
        for (let i = 0; i < this.points.length; i++) {
            let point = this.points[i];
            point.offset = sin(time * 3 + i * 0.2 + this.index) * (bassLevel / 10 + 5);
        }
    }
    
    display() {
        noFill();
        stroke(50, 100, 200, 100);
        strokeWeight(3);
        
        beginShape();
        for (let point of this.points) {
            vertex(this.x + point.offset, point.y);
        }
        endShape();
        
        // Efecto de brillo
        stroke(80, 150, 255, 50);
        strokeWeight(6);
        beginShape();
        for (let point of this.points) {
            vertex(this.x + point.offset, point.y);
        }
        endShape();
    }
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
    
    // Reinicializar cuerdas de bajo
    bassStrings = [];
    for (let i = 0; i < 8; i++) {
        bassStrings.push(new BassString(i));
    }
}
````
Mobile Index
````js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Mitski Control - Mobile</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.7.0/p5.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/4.5.4/socket.io.min.js"></script>
    <style>
        body { 
            margin: 0; 
            padding: 0; 
            overflow: hidden;
            touch-action: none;
        }
        canvas { 
            display: block; 
        }
    </style>
</head>
<body>
    <script src="sketch.js"></script>
</body>
</html>
````
Mobile skecth.js
````js
let socket;
let lastTouchX = null;
let lastTouchY = null;
const touchThreshold = 10;

// Estado de capas
let layers = {
    drums: true,
    bass: true,
    cymbals: true,
    lyrics: true
};

// Botones de control
let buttons = [];

function setup() {
    createCanvas(windowWidth, windowHeight);
    
    // Conexión socket
    socket = io();
    
    socket.on('connect', () => {
        console.log('✅ Connected to server');
    });
    
    socket.on('layersState', (data) => {
        console.log('📊 Layers state received:', data);
        layers = data;
    });
    
    socket.on('message', (data) => {
        console.log(`📩 Received message:`, data);
    });
    
    socket.on('disconnect', () => {
        console.log('❌ Disconnected from server');
    });
    
    socket.on('connect_error', (error) => {
        console.error('Socket.IO error:', error);
    });
    
    // Crear botones en las esquinas
    createButtons();
}

function createButtons() {
    buttons = [];
    let buttonSize = min(width, height) * 0.15;
    let margin = 20;
    
    buttons.push(new LayerButton('drums', margin, margin, buttonSize, '🥁', 'Drums'));
    buttons.push(new LayerButton('bass', width - margin - buttonSize, margin, buttonSize, '🎸', 'Bass'));
    buttons.push(new LayerButton('cymbals', margin, height - margin - buttonSize, buttonSize, '✨', 'Cymbals'));
    buttons.push(new LayerButton('lyrics', width - margin - buttonSize, height - margin - buttonSize, buttonSize, '📝', 'Lyrics'));
}

function draw() {
    // Fondo con gradiente
    drawBackground();
    
    // Área central de interacción
    drawInteractionArea();
    
    // Dibujar botones
    for (let button of buttons) {
        button.display();
    }
    
    // Instrucciones
    drawInstructions();
    
    // Indicador de conexión
    drawConnectionStatus();
}

function drawBackground() {
    let c1 = color(20, 20, 40);
    let c2 = color(60, 40, 80);
    
    for (let y = 0; y < height; y++) {
        let inter = map(y, 0, height, 0, 1);
        let c = lerpColor(c1, c2, inter);
        stroke(c);
        line(0, y, width, y);
    }
}

function drawInteractionArea() {
    push();
    noFill();
    stroke(255, 255, 255, 50);
    strokeWeight(2);
    let margin = min(width, height) * 0.25;
    rect(margin, margin, width - margin * 2, height - margin * 2, 20);
    
    // Indicador de toque
    if (mouseIsPressed && mouseX > margin && mouseX < width - margin && 
        mouseY > margin && mouseY < height - margin) {
        fill(100, 150, 255, 100);
        noStroke();
        circle(mouseX, mouseY, 60);
        
        // Ondas alrededor del toque
        noFill();
        stroke(100, 150, 255, 150);
        strokeWeight(2);
        for (let i = 1; i <= 3; i++) {
            circle(mouseX, mouseY, 60 + i * 20);
        }
    }
    pop();
}

function drawInstructions() {
    push();
    textAlign(CENTER, CENTER);
    textSize(min(width, height) * 0.04);
    fill(255, 255, 255, 200);
    noStroke();
    
    text('🎵 Once More To See You - Mitski', width / 2, height / 2 - 50);
    
    textSize(min(width, height) * 0.035);
    fill(255, 255, 255, 150);
    text('Touch center to interact with lyrics', width / 2, height / 2);
    text('Press corners to toggle layers', width / 2, height / 2 + 30);
    pop();
}

function drawConnectionStatus() {
    push();
    let statusColor = socket && socket.connected ? color(100, 255, 100) : color(255, 100, 100);
    let statusText = socket && socket.connected ? '🟢 Connected' : '🔴 Disconnected';
    
    fill(0, 0, 0, 150);
    noStroke();
    rectMode(CENTER);
    rect(width / 2, 30, 150, 40, 20);
    
    fill(statusColor);
    textAlign(CENTER, CENTER);
    textSize(14);
    text(statusText, width / 2, 30);
    pop();
}

function touchStarted() {
    // Verificar si se tocó un botón
    for (let button of buttons) {
        if (button.contains(mouseX, mouseY)) {
            button.toggle();
            return false;
        }
    }
    
    // Interacción con el área central
    sendTouchData();
    return false;
}

function touchMoved() {
    if (socket && socket.connected) {
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);
        
        if (dx > touchThreshold || dy > touchThreshold || lastTouchX === null) {
            sendTouchData();
        }
    }
    return false;
}

function sendTouchData() {
    if (socket && socket.connected) {
        let touchData = {
            x: mouseX,
            y: mouseY,
            width: width,
            height: height
        };
        socket.emit('touchLyrics', touchData);
        
        lastTouchX = mouseX;
        lastTouchY = mouseY;
    }
}

class LayerButton {
    constructor(layer, x, y, size, emoji, label) {
        this.layer = layer;
        this.x = x;
        this.y = y;
        this.size = size;
        this.emoji = emoji;
        this.label = label;
        this.pressed = false;
    }
    
    contains(px, py) {
        return px > this.x && px < this.x + this.size &&
               py > this.y && py < this.y + this.size;
    }
    
    toggle() {
        this.pressed = true;
        setTimeout(() => this.pressed = false, 200);
        
        layers[this.layer] = !layers[this.layer];
        
        if (socket && socket.connected) {
            socket.emit('toggleLayer', {
                layer: this.layer,
                active: layers[this.layer]
            });
            
            console.log(`🔄 Toggled ${this.layer}: ${layers[this.layer]}`);
        }
    }
    
    display() {
        let isActive = layers[this.layer];
        
        push();
        // Fondo del botón
        if (this.pressed) {
            fill(150, 150, 255, 200);
        } else if (isActive) {
            fill(100, 150, 255, 150);
        } else {
            fill(80, 80, 100, 150);
        }
        
        stroke(255, 255, 255, 100);
        strokeWeight(2);
        rect(this.x, this.y, this.size, this.size, 10);
        
        // Emoji
        noStroke();
        fill(255);
        textAlign(CENTER, CENTER);
        textSize(this.size * 0.4);
        text(this.emoji, this.x + this.size / 2, this.y + this.size / 2 - 5);
        
        // Label
        textSize(this.size * 0.15);
        fill(255, 255, 255, 200);
        text(this.label, this.x + this.size / 2, this.y + this.size - 10);
        
        // Indicador de estado
        if (isActive) {
            fill(100, 255, 100);
        } else {
            fill(255, 100, 100);
        }
        noStroke();
        circle(this.x + this.size - 10, this.y + 10, 12);
        
        // Borde del indicador
        noFill();
        stroke(255);
        strokeWeight(1);
        circle(this.x + this.size - 10, this.y + 10, 12);
        pop();
    }
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
    createButtons();
}
````
Server
```` js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const os = require('os');

const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

app.use(express.static('public'));

// Obtener IP local
function getLocalIP() {
    const interfaces = os.networkInterfaces();
    for (let interfaceName in interfaces) {
        for (let iface of interfaces[interfaceName]) {
            if (iface.family === 'IPv4' && !iface.internal) {
                return iface.address;
            }
        }
    }
    return 'localhost';
}

// Estado compartido de las capas activas
let layersState = {
    drums: true,
    bass: true,
    cymbals: true,
    lyrics: true
};

io.on('connection', (socket) => {
    console.log('✅ New client connected:', socket.id);
    
    // Enviar estado actual de capas al nuevo cliente
    socket.emit('layersState', layersState);
    
    // Manejar mensajes genéricos (compatibilidad con código original)
    socket.on('message', (message) => {
        console.log('Received message =>', message);
        socket.broadcast.emit('message', message);
    });
    
    // Manejar toggles de capas
    socket.on('toggleLayer', (data) => {
        console.log('🔄 Toggle layer:', data);
        if (data && data.layer && layersState.hasOwnProperty(data.layer)) {
            layersState[data.layer] = data.active;
            // Broadcast a todos los clientes
            io.emit('layersState', layersState);
        }
    });
    
    // Manejar interacciones táctiles con las letras
    socket.on('touchLyrics', (data) => {
        console.log('👆 Touch lyrics at:', data.x, data.y);
        // Broadcast a todos excepto al emisor
        socket.broadcast.emit('touchLyrics', data);
    });
    
    // Sincronización de tiempo de música
    socket.on('musicTime', (data) => {
        socket.broadcast.emit('musicTime', data);
    });

    socket.on('disconnect', () => {
        console.log('❌ Client disconnected:', socket.id);
    });
});

server.listen(port, () => {
    const localIP = getLocalIP();
    console.log('\n╔═══════════════════════════════════════════╗');
    console.log('║   🎵 Mitski Visual Server Running 🎵    ║');
    console.log('╚═══════════════════════════════════════════╝\n');
    
    console.log('📱 Local Network Access:');
    console.log('   ┌─────────────────────────────────────────');
    console.log(`   │ Desktop: http://${localIP}:${port}/desktop/`);
    console.log(`   │ Mobile:  http://${localIP}:${port}/mobile/`);
    console.log('   └─────────────────────────────────────────\n');
    
    console.log('💻 Localhost Access:');
    console.log('   ┌─────────────────────────────────────────');
    console.log(`   │ Desktop: http://localhost:${port}/desktop/`);
    console.log(`   │ Mobile:  http://localhost:${port}/mobile/`);
    console.log('   └─────────────────────────────────────────\n');
    
    console.log('🌐 For Remote Access (RECOMMENDED):');
    console.log('   ⭐ Use VS Code Dev Tunnels:');
    console.log('   ┌─────────────────────────────────────────');
    console.log('   │ 1. Open "Ports" tab in VS Code');
    console.log('   │    (View → Ports or Ctrl+Shift+`)');
    console.log('   │ 2. Right-click on port 3000');
    console.log('   │ 3. Select "Port Visibility" → "Public"');
    console.log('   │ 4. Copy the URL (e.g.:');
    console.log('   │    https://xxxxx-3000.use2.devtunnels.ms/)');
    console.log('   │ 5. Add /desktop/ or /mobile/');
    console.log('   │');
    console.log('   │ Your URLs will look like:');
    console.log('   │ https://zqdlcf6q-3000.use2.devtunnels.ms/desktop/');
    console.log('   │ https://zqdlcf6q-3000.use2.devtunnels.ms/mobile/');
    console.log('   └─────────────────────────────────────────\n');
    
    console.log('╔═══════════════════════════════════════════╗');
    console.log('║  ✅ Server ready! Press Ctrl+C to stop   ║');
    console.log('╚═══════════════════════════════════════════╝\n');
});
````
Y por último la canción esta subida a este drive, hay que meterla dentro del public y asegurandose de que tenga el nombre igual al referenciado en el código para que funicone
