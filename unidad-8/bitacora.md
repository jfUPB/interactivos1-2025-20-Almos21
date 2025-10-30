# Evidencias de la unidad 8

## Actividad 01
La canción que voy a elegir es House Tour de Sabrina Carpenter

-Referente visuales: 
<img width="1643" height="918" alt="image" src="https://github.com/user-attachments/assets/63bb0e58-3612-459e-827d-53992b452db3" />

<img width="1365" height="656" alt="image" src="https://github.com/user-attachments/assets/ffd7db8b-7f81-480f-85e8-578a76752246" />

- Idea visuales:
Para las visuales tengo la idea de representar la "casa" a la que se refiere sabrina en su canción, para esto quise inspirarme en su escenario del ultimo tour que ha estado haciendo y la casa de la pelicula de barbie, que siento tienen similitud y me dan las mismas vibras, tengo la intención de que se le permita al usuario pasar entre los pisos de la casa e ir moviendo a una mini Sabrina que este cantando adentro a lo largo de todos los pisos, pudiendo también cambiar los colores de fondo y dar un movimiento de cámara que haga que se sienta dinámicas las visuales.
- El micro:bit va a afectar las visuales moviendo entre los tres pisos con los botones a y b. El movil tendrá un slider para controlar los colores de la escena en general y tres botones para cambiar las poses de sabrina, además un botón para alternar la vista entre una general donde se vea la casa en su totalidad y otra donde se haga zoom a Sabrina y la siga a lo largo del movimiento

## Actividad 02
- Proceso de construcción:
El primer paso es el de poder incluir el microbit en el sevidor establecido anteriormente, esto en el apartado de desktop, ya que la conexión con el microbit es directa por usb, para esto agarré como base la máquina de estado hecha en p5.js anteriormente y la después utilicé la idea que tenía y la base de un código que ya permitía utilizar micro:bit dentro del servidor para desarrollarla con IA. Utilicé a Claude y chat gpt. Claude me dio una versión inicial base, pero con problemar como el que el audio no funcionaba y el zoom se hacia mal, chat gpt me ayudo a poder perfeccionar y solucionar errores.

### Evidencia y Códigos:
Este es el video de yo probando el programa:
[Video](https://youtu.be/_gCW_xTQj2k?si=nwca7QXGehRkRCgQ)

Y estos los códigos finales
#### Desktop sketch
```` c++
// === VARIABLES (idénticas a tu versión) ===
let clickPosX = 0;
let clickPosY = 0;

let port;
let connectBtn;
let connectionInitialized = false;
let microBitConnected = false;

let socket;
let song;
let playBtn;
let audioLoaded = false;
let audioError = false;
let audioErrorMsg = '';
// === Variables globales de cámara ===
let currentScale = 1;
let cameraX = 0;
let cameraY = 0;

const STATES = {
  WAIT_MICROBIT_CONNECTION: "WAITMICROBIT_CONNECTION",
  RUNNING: "RUNNING",
};
let appState = STATES.WAIT_MICROBIT_CONNECTION;
let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;
let prevmicroBitAState = false;
let prevmicroBitBState = false;

let currentFloor = 1;
let sabrinaX = 0;
let targetSabrinaX = 0;
let cameraOffsetY = 0;
let targetCameraOffsetY = 0;

let hueShift = 0;
let sabrinaPosition = 1; // 0: izquierda, 1: centro, 2: derecha
let zoomMode = false;

const pinkPalette = {
  light: '#FFB3D9',
  medium: '#FF69B4',
  dark: '#FF1493',
  accent: '#FF85C1',
  background: '#1a0a14'
};

// === PRELOAD / SETUP ===
let audioCandidates = [
  'house-tour.mp3',        // misma carpeta que index.html (preferido)
  'assets/house-tour.mp3', // carpeta assets
  '../house-tour.mp3',     // posible ruta relativa (si tu HTML está en subcarpeta)
  '/house-tour.mp3'        // ruta absoluta desde root
];

function preload() {
  // dejamos preload vacío intencionalmente para evitar problemas de autoplay / rutas.
}

// ---------- Nuevo: cargar audio con reintentos ----------
function loadAudioFile() {
  console.log("🔍 Trying audio path: house-tour.mp3");

  // Reanudar el contexto antes de cargar
  const ac = getAudioContext();
  if (ac && ac.state !== 'running') {
    ac.resume().then(() => console.log("✅ AudioContext resumed before loading"));
  }

  // Intentar cargar el audio
  loadSound(
    'house-tour.mp3',
    (loadedSound) => {
      song = loadedSound;
      audioLoaded = true;
      console.log("✅ Audio loaded successfully");
      playBtn.html("▶ Play Song");
      playBtn.style('background-color', '#32CD32');

      // Autoplay solo si fue un clic directo
      try {
        song.play();
        playBtn.html("⏸ Pause Song");
        playBtn.style('background-color', '#FF6347');
        console.log("🎵 Audio is now playing");
      } catch (e) {
        console.warn("⚠️ Could not auto-play:", e);
      }
    },
    (err) => {
      console.error("❌ Failed to load sound:", err);
      playBtn.html("⚠️ Error loading");
      playBtn.style('background-color', '#FF0000');
    }
  );
}



function setup() {
  createCanvas(windowWidth, windowHeight);
  socket = io();

  socket.on('message', (data) => {
    if (data.type === 'colorChange') hueShift = data.hue;
    else if (data.type === 'sabrinaPosition') sabrinaPosition = data.position;
    else if (data.type === 'viewMode') zoomMode = data.zoom;
  });

  port = createSerial();

  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(20, 20);
  connectBtn.mousePressed(connectBtnClick);

  playBtn = createButton("▶ Play Song");
  playBtn.position(20, 80);
  playBtn.mousePressed(togglePlay);

  sabrinaX = width / 2;
  targetSabrinaX = width / 2;
}

// === FUNCIONES INTACTAS (togglePlay, connectBtnClick, etc.) ===
function togglePlay() {
  // 🔊 Aseguramos que el contexto esté activo
  if (typeof getAudioContext === 'function') {
    const ac = getAudioContext();
    if (ac && ac.state !== 'running') {
      ac.resume().then(() => {
        console.log("✅ AudioContext resumed");
      });
    }
  }

  // Si no está cargado, intentar cargarlo
  if (!song || !audioLoaded) {
    playBtn.html("⏳ Loading...");
    playBtn.style('background-color', '#FFA500');
    loadAudioFile();
    return;
  }

  // Si está cargado, reproducir o pausar
  if (song.isPlaying && song.isPlaying()) {
    song.pause();
    playBtn.html("▶ Play Song");
    playBtn.style('background-color', '#32CD32');
  } else {
    song.play();
    playBtn.html("⏸ Pause Song");
    playBtn.style('background-color', '#FF6347');
  }
}




// ---------- Añadimos mousePressed global para garantizar user gesture ----------
function mousePressed() {
  // Esto desbloquea el AudioContext en la mayoría de los navegadores cuando el usuario interactúa con la página.
  if (typeof userStartAudio === 'function') {
    try { userStartAudio(); } catch (e) { /* ignore */ }
  }
  if (typeof getAudioContext === 'function') {
    try {
      let ac = getAudioContext();
      if (ac && ac.state !== 'running' && typeof ac.resume === 'function') ac.resume();
    } catch (e) { /* ignore */ }
  }
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
    connectionInitialized = false;
  } else port.close();
}

function updateButtonStates(newAState, newBState) {
  if (newAState && !prevmicroBitAState) {
    currentFloor = constrain(currentFloor + 1, 0, 2);
    socket.emit('message', { type: 'floorChange', floor: currentFloor });
  }
  if (newBState && !prevmicroBitBState) {
    currentFloor = constrain(currentFloor - 1, 0, 2);
    socket.emit('message', { type: 'floorChange', floor: currentFloor });
  }
  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}

// === COLOR SHIFT ===
function applyHueShift(col) {
  colorMode(HSB, 360, 100, 100);
  let h = hue(col), s = saturation(col), b = brightness(col);
  let newColor = color((h + hueShift) % 360, s, b);
  colorMode(RGB, 255);
  return newColor;
}

// ==================================================
// 🔧 CAMBIOS PRINCIPALES AQUÍ: MOVIMIENTO POR VENTANA
// ==================================================
function drawHouse() {
  push();

  // === Parámetros base ===
  let totalFloors = 3;
  let floorHeight = height * 0.25;
  let houseWidth = width * 0.5;
  let houseHeight = totalFloors * floorHeight;

  // Centro base de la casa
  let houseCenterX = width / 2;
  let houseCenterY = height / 2 + 50; // pequeño desplazamiento hacia abajo

  // Calcular posición de Sabrina
  let regionCenters = [-houseWidth / 3, 0, houseWidth / 3];
  let regionCenter = regionCenters[constrain(sabrinaPosition, 0, 2)];
  let microOffset = map(constrain(microBitX, -1024, 1024), -1024, 1024, -houseWidth / 6, houseWidth / 6);
  let sabrinaXWorld = houseCenterX + regionCenter + microOffset;
  let sabrinaYWorld = houseCenterY + (1 - currentFloor) * floorHeight + floorHeight * 0.15;


  // === Manejo de cámara ===
  let targetScale = zoomMode ? 2.2 : 1;
  currentScale = lerp(currentScale || 1, targetScale, 0.1);

  let targetCamX, targetCamY;

  if (zoomMode) {
    // Cámara centrada en Sabrina
    targetCamX = sabrinaXWorld - width / 2 / currentScale;
    targetCamY = sabrinaYWorld - height / 2 / currentScale;
  } else {
    // Cámara centrada en toda la casa
    targetCamX = houseCenterX - width / 2 / currentScale;
    targetCamY = houseCenterY - houseHeight / 2 / currentScale;
  }

  cameraX = lerp(cameraX || targetCamX, targetCamX, 0.08);
  cameraY = lerp(cameraY || targetCamY, targetCamY, 0.08);

  // === Aplicar transformaciones de cámara ===
  translate(width / 2, height / 2);
  scale(currentScale);
  translate(-cameraX - width / 2 / currentScale, -cameraY - height / 2 / currentScale);

  // === Dibujo de la casa ===
  for (let i = 0; i < totalFloors; i++) {
    let y = houseCenterY - (i - 1) * floorHeight;

    // Pared principal
    fill(applyHueShift(color(i === currentFloor ? pinkPalette.medium : pinkPalette.dark)));
    stroke(255);
    strokeWeight(2);
    rect(houseCenterX - houseWidth / 2, y - floorHeight / 2, houseWidth, floorHeight, 15);

    // Ventanas / puertas
    fill(applyHueShift(color(pinkPalette.background)));
    noStroke();
    for (let j = 0; j < 3; j++) {
      let wx = houseCenterX + map(j, 0, 2, -houseWidth / 3, houseWidth / 3);
      let wy = y;
      let w = 80;
      let h = floorHeight * 0.6;
      rect(wx - w / 2, wy - h / 2, w, h, 40, 40, 0, 0);
    }

    // Etiqueta de piso
    fill(255);
    noStroke();
    textAlign(CENTER, CENTER);
    textSize(16);
    text(`Floor ${i}`, houseCenterX - houseWidth / 2 + 50, y - 10);
  }

  // === Dibujo de Sabrina ===
  drawSabrina(sabrinaXWorld, sabrinaYWorld);
  drawEffects(sabrinaXWorld, sabrinaYWorld);

  pop();
}


// === DIBUJOS DE SABRINA Y EFECTOS (idénticos) ===
function drawSabrina(x, y) {
  push();
  translate(x, y);
  let bounce = sin(frameCount * 0.1) * 3;
  translate(0, bounce);
  fill(0, 50);
  noStroke();
  ellipse(0, 25, 30, 10);
  fill(applyHueShift(color(pinkPalette.light)));
  stroke(applyHueShift(color(pinkPalette.dark)));
  strokeWeight(2);
  triangle(-15, 0, 15, 0, 0, -30);
  fill(255, 220, 200);
  stroke(applyHueShift(color(pinkPalette.dark)));
  strokeWeight(2);
  circle(0, -40, 20);
  fill(240, 200, 120);
  noStroke();
  arc(0, -42, 24, 20, PI, TWO_PI);
  pop();
}

function drawEffects(x, y) {
  if (sabrinaPosition === 0) {
    // Left: Musical notes
    drawMusicalNotes(x, y);
  } else if (sabrinaPosition === 1) {
    // Center: Sparkles
    drawSparkles(x, y);
  } else if (sabrinaPosition === 2) {
    // Right: Hearts
    drawHearts(x, y);
  }
}

function drawMusicalNotes(x, y) {
  push();
  translate(x, y);
  
  if (frameCount % 30 < 15) {
    fill(applyHueShift(color(pinkPalette.medium)));
    noStroke();
    textSize(20);
    text("♪", 25, -50);
    text("♫", -25, -55);
  }
  
  pop();
}

function drawSparkles(x, y) {
  push();
  translate(x, y);
  
  for (let i = 0; i < 6; i++) {
    let angle = (frameCount * 0.05 + i * PI / 3) % TWO_PI;
    let radius = 25;
    let sparkleX = cos(angle) * radius;
    let sparkleY = sin(angle) * radius - 40;
    
    fill(255, 215, 0, 200);
    noStroke();
    star(sparkleX, sparkleY, 2, 5, 5);
  }
  
  pop();
}

function drawHearts(x, y) {
  push();
  translate(x, y);
  
  for (let i = 0; i < 3; i++) {
    let heartY = -50 + (frameCount * 0.5 + i * 20) % 60;
    let size = 8;
    
    fill(applyHueShift(color(pinkPalette.dark)), 180);
    noStroke();
    
    push();
    translate(0, -heartY);
    beginShape();
    vertex(0, size/2);
    bezierVertex(-size, -size/2, -size, -size, 0, -size/4);
    bezierVertex(size, -size, size, -size/2, 0, size/2);
    endShape(CLOSE);
    pop();
  }
  
  pop();
}

function star(x, y, radius1, radius2, npoints) {
  let angle = TWO_PI / npoints;
  let halfAngle = angle / 2.0;
  
  push();
  translate(x, y);
  beginShape();
  for (let a = -PI / 2; a < TWO_PI - PI / 2; a += angle) {
    let sx = cos(a) * radius2;
    let sy = sin(a) * radius2;
    vertex(sx, sy);
    sx = cos(a + halfAngle) * radius1;
    sy = sin(a + halfAngle) * radius1;
    vertex(sx, sy);
  }
  endShape(CLOSE);
  pop();
}

function draw() {
  // Update play button if audio loads
  if (audioLoaded && playBtn.html() === "Loading...") {
    playBtn.html("▶ Play Song");
    playBtn.style('background-color', '#32CD32');
    playBtn.style('cursor', 'pointer');
  }
  
  // Microbit connection handling
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    microBitConnected = false;
  } else {
    microBitConnected = true;
    connectBtn.html("Disconnect");

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let data = port.readUntil("\n");
      if (data) {
        data = data.trim();
        let values = data.split(",");
        if (values.length == 4) {
          // Map X movement to Sabrina position (constrained within house)
          let normalizedX = int(values[0]);
          targetSabrinaX = map(normalizedX, -512, 512, width * 0.2, width * 0.8);
          
          // Map Y to subtle camera offset
          let normalizedY = int(values[1]);
          targetCameraOffsetY = map(normalizedY, -512, 512, -30, 30);
          
          microBitAState = values[2].toLowerCase() === "true";
          microBitBState = values[3].toLowerCase() === "true";
          updateButtonStates(microBitAState, microBitBState);
          
          // Send position to mobile
          socket.emit('message', {
            type: 'position',
            x: normalizedX,
            y: normalizedY,
            sabrinaX: targetSabrinaX
          });
        }
      }
    }
  }

  // Smooth interpolation
  sabrinaX = lerp(sabrinaX, targetSabrinaX, 0.1);
  cameraOffsetY = lerp(cameraOffsetY, targetCameraOffsetY, 0.05);

  switch (appState) {
    case STATES.WAIT_MICROBIT_CONNECTION:
      background(applyHueShift(color(pinkPalette.background)));
      
      // Waiting screen
      fill(applyHueShift(color(pinkPalette.light)));
      noStroke();
      textAlign(CENTER, CENTER);
      textSize(32);
      text("HOUSE TOUR", width/2, height/2 - 50);
      textSize(18);
      fill(applyHueShift(color(pinkPalette.accent)));
      text("Connect your micro:bit to start", width/2, height/2 + 20);
      text("Button A: Floor Up | Button B: Floor Down", width/2, height/2 + 50);
      text("Tilt: Move Sabrina & Camera", width/2, height/2 + 80);
      
      if (audioLoaded) {
        text("Press Play to start the music!", width/2, height/2 + 110);
      }
      
      if (microBitConnected === true) {
        print("Microbit ready");
        appState = STATES.RUNNING;
      }
      break;

    case STATES.RUNNING:
      if (microBitConnected === false) {
        print("Waiting microbit connection");
        appState = STATES.WAIT_MICROBIT_CONNECTION;
      }

      // Main visual
      background(applyHueShift(color(pinkPalette.background)));
      
      // Draw decorative elements
      fill(applyHueShift(color(pinkPalette.dark)), 30);
      noStroke();
      for (let i = 0; i < 5; i++) {
        let x = (frameCount * (i + 1) * 0.5) % (width + 200) - 100;
        let y = height * 0.2 + i * 80;
        circle(x, y, 60);
      }
      
      // Draw the house
      drawHouse();
      
      // Floor indicator
      fill(applyHueShift(color(pinkPalette.light)));
      noStroke();
      textAlign(LEFT, TOP);
      textSize(18);
      text(`Current Floor: ${currentFloor}`, 20, 140);
      text(`View: ${zoomMode ? 'Zoomed' : 'General'}`, 20, 165);
      text(`Position: ${['Left', 'Center', 'Right'][sabrinaPosition]}`, 20, 190);
      
      break;
  }
  
}
````
#### Desktop Index
```` c++
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sabrina Visual - Desktop</title>

  <!-- ✅ p5.js primero -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>

  <!-- ✅ Luego p5.sound (versión oficial compatible con p5.js 1.9+) -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/addons/p5.sound.min.js"></script>

  <!-- ✅ Socket.IO y p5.webserial -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/4.5.4/socket.io.min.js"></script>
  <script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>

  <style>
    body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      background-color: #000;
      color: #fff;
      font-family: sans-serif;
    }
    canvas {
      display: block;
    }

    /* Botón para iniciar audio si el contexto está suspendido */
    #startButton {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      padding: 1rem 2rem;
      background: #32CD32;
      border: none;
      border-radius: 10px;
      color: white;
      font-size: 1.2rem;
      cursor: pointer;
      display: none;
    }
  </style>
</head>
<body>
  <button id="startButton">Iniciar audio 🔊</button>

  <!-- ✅ Tu sketch al final -->
  <script src="sketch.js"></script>

  <script>
    // ✅ Desbloquear contexto de audio en el primer clic
    const startButton = document.getElementById("startButton");

    function resumeAudioContext() {
      const ac = getAudioContext();
      if (ac.state !== 'running') {
        ac.resume().then(() => {
          console.log("🎧 AudioContext resumed manually");
          startButton.style.display = 'none';
        });
      } else {
        startButton.style.display = 'none';
      }
    }

    // Mostrar botón si el audio está bloqueado
    window.addEventListener('click', () => {
      const ac = getAudioContext();
      if (ac.state !== 'running') {
        startButton.style.display = 'block';
      }
    });

    startButton.addEventListener('click', resumeAudioContext);
  </script>
</body>
</html>
````
#### Mobile Sketch
```` c++
// Socket.io connection
let socket;

// Control variables
let sabrinaPosition = 1; // 0: left, 1: center, 2: right
let zoomMode = false; // false: general view, true: zoom
let hueShift = 0; // Color shift (0-360)
let currentFloor = 1;

// UI elements
let colorSlider;
let positionButtons = [];
let viewToggleBtn;

// Button style constants
const buttonStyle = {
  width: 110,
  height: 50,
  radius: 25,
  spacing: 15
};

const POSITIONS = ['Left', 'Center', 'Right'];

function setup() {
  createCanvas(windowWidth, windowHeight);

  socket = io(); // Automatically connects to the same host
  socket.on('connect', () => console.log('📱 Mobile connected'));
  socket.on('message', (data) => {
    if (data.type === 'floorChange') currentFloor = data.floor;
  });

  setupUI();
}

function setupUI() {
  // 🎨 Color slider
  let sliderY = height * 0.75;
  colorSlider = createSlider(0, 360, hueShift);
  colorSlider.position(width / 2 - 150, sliderY);
  colorSlider.style('width', '300px');
  colorSlider.input(() => {
    hueShift = colorSlider.value();
    sendColorUpdate();
  });

  // 🎯 Position buttons
  let btnY = height * 0.82;
  let totalWidth = (buttonStyle.width * 3) + (buttonStyle.spacing * 2);
  let startX = (width - totalWidth) / 2;

  for (let i = 0; i < 3; i++) {
    let btn = createButton(POSITIONS[i]);
    let btnX = startX + (i * (buttonStyle.width + buttonStyle.spacing));
    btn.position(btnX, btnY);
    btn.size(buttonStyle.width, buttonStyle.height);
    styleButton(btn, i === sabrinaPosition);

    btn.mousePressed(() => {
      sabrinaPosition = i;
      updateButtonStyles();
      sendPositionUpdate();
    });

    positionButtons.push(btn);
  }

  // 🔍 View toggle button
  viewToggleBtn = createButton('🏠 General View');
  viewToggleBtn.position(width / 2 - 80, height * 0.9);
  viewToggleBtn.size(160, 45);
  styleButton(viewToggleBtn, false);

  viewToggleBtn.mousePressed(() => {
    zoomMode = !zoomMode;
    viewToggleBtn.html(zoomMode ? '🔍 Floor Zoom' : '🏠 General View');
    sendViewUpdate();
  });
}

function styleButton(btn, isActive) {
  btn.style('background-color', isActive ? '#FF1493' : '#FF69B4');
  btn.style('color', 'white');
  btn.style('border', isActive ? '3px solid #FFB3D9' : 'none');
  btn.style('border-radius', buttonStyle.radius + 'px');
  btn.style('font-weight', 'bold');
  btn.style('font-size', '14px');
  btn.style('cursor', 'pointer');
  btn.style('box-shadow', '0 4px 10px rgba(0,0,0,0.3)');
}

function updateButtonStyles() {
  for (let i = 0; i < positionButtons.length; i++) {
    styleButton(positionButtons[i], i === sabrinaPosition);
  }
}

// ===== Socket messages =====
function sendColorUpdate() {
  socket.emit('message', { type: 'colorChange', hue: hueShift });
}
function sendPositionUpdate() {
  socket.emit('message', { type: 'sabrinaPosition', position: sabrinaPosition });
}
function sendViewUpdate() {
  socket.emit('message', { type: 'viewMode', zoom: zoomMode });
}

// ===== UI Redraw on resize =====
function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  removeElements();
  setupUI();
}

// ===== Drawing section =====
function draw() {
  colorMode(HSB, 360, 100, 100);
  let bgHue = (330 + hueShift) % 360;
  background(bgHue, 80, 10);
  colorMode(RGB);

  fill(255, 182, 217);
  noStroke();
  textAlign(CENTER, CENTER);

  textSize(32);
  text('HOUSE TOUR', width / 2, height * 0.12);
  textSize(18);
  fill(255, 133, 193);
  text('Mobile Controller', width / 2, height * 0.18);

  fill(255, 182, 217);
  textSize(16);
  text(`Current Floor: ${currentFloor}`, width / 2, height * 0.24);

  fill(255, 133, 193);
  textSize(14);
  text(zoomMode ? '🔍 Zoomed to Floor' : '🏠 General View', width / 2, height * 0.28);

  // Draw preview
  drawPreview();
}
function drawPreview() {
  let previewW = min(width * 0.8, 600);
  let previewH = min(height * 0.36, 300);
  let previewX = width / 2;
  let previewY = height / 2 - 40;

  // background del preview
  fill(255, 20, 147, 25);
  noStroke();
  rect(previewX - previewW/2, previewY - previewH/2, previewW, previewH, 20);

  // calcular los 3 centros de ventana exactamente como en desktop:
  let leftX = previewX - previewW / 3;
  let centerX = previewX;
  let rightX = previewX + previewW / 3;
  let doorY = previewY; // centro vertical en el preview

  // dibujar las 3 ventanas (puertas)
  fill(26, 10, 20);
  noStroke();
  let doorW = previewW * 0.18; // proporción de la vista
  let doorH = previewH * 0.6;
  rect(leftX - doorW/2, doorY - doorH/2, doorW, doorH, doorW/2, doorW/2, 0, 0);
  rect(centerX - doorW/2, doorY - doorH/2, doorW, doorH, doorW/2, doorW/2, 0, 0);
  rect(rightX - doorW/2, doorY - doorH/2, doorW, doorH, doorW/2, doorW/2, 0, 0);

  // sabrina preview X según sabrinaPosition
  let posXmap = [leftX, centerX, rightX];
  let sabrinaX = posXmap[sabrinaPosition] || centerX;
  drawMiniSabrina(sabrinaX, doorY, 2);

  // efectos según posición
  if (sabrinaPosition === 0) drawMusicalNotes(sabrinaX, doorY);
  else if (sabrinaPosition === 1) drawSparkles(sabrinaX, doorY);
  else drawHearts(sabrinaX, doorY);

  // labels / info
  fill(255);
  textSize(16);
  text(`Position: ${POSITIONS[sabrinaPosition]}`, previewX, previewY + previewH/2 + 28);
}


// ===== Mini drawings =====
function drawMiniSabrina(x, y, scale = 1) {
  push();
  translate(x, y);
  scale(scale);

  let bounce = sin(frameCount * 0.1) * 2;
  translate(0, bounce);

  fill(0, 50);
  noStroke();
  ellipse(0, 20, 25, 8);

  fill(255, 182, 217);
  stroke(255, 20, 147);
  strokeWeight(2);
  triangle(-12, 0, 12, 0, 0, -25);

  fill(255, 220, 200);
  stroke(255, 20, 147);
  circle(0, -32, 16);

  fill(240, 200, 120);
  noStroke();
  arc(0, -34, 18, 16, PI, TWO_PI);

  push();
  let micSway = sin(frameCount * 0.15) * 5;
  rotate(radians(micSway));
  stroke(150);
  strokeWeight(2);
  line(4, -25, 4, -18);
  fill(100);
  circle(4, -16, 6);
  pop();

  pop();
}

function drawMusicalNotes(x, y) {
  push();
  translate(x, y);
  fill(255, 105, 180);
  textSize(24);
  textAlign(CENTER, CENTER);
  let notes = ['♪', '♫', '♪'];
  for (let i = 0; i < notes.length; i++) {
    if ((frameCount + i * 10) % 30 < 20) {
      text(notes[i], (i - 1) * 40, -60 + sin((frameCount + i * 10) * 0.1) * 5);
    }
  }
  pop();
}

function drawSparkles(x, y) {
  push();
  translate(x, y);
  for (let i = 0; i < 8; i++) {
    let angle = (frameCount * 0.05 + i * PI / 4) % TWO_PI;
    let r = 30 + sin(frameCount * 0.1 + i) * 10;
    fill(255, 215, 0, 200);
    noStroke();
    star(cos(angle) * r, sin(angle) * r, 3, 6, 5);
  }
  pop();
}

function drawHearts(x, y) {
  push();
  translate(x, y);
  for (let i = 0; i < 5; i++) {
    let hx = random(-50, 50);
    let hy = -60 + (frameCount * 0.5 + i * 20) % 100;
    let s = random(8, 15);
    fill(255, 20, 147, 180);
    noStroke();
    push();
    translate(hx, -hy);
    beginShape();
    vertex(0, s / 2);
    bezierVertex(-s, -s / 2, -s, -s, 0, -s / 4);
    bezierVertex(s, -s, s, -s / 2, 0, s / 2);
    endShape(CLOSE);
    pop();
  }
  pop();
}

function star(x, y, r1, r2, n) {
  let angle = TWO_PI / n;
  beginShape();
  for (let a = -PI / 2; a < TWO_PI - PI / 2; a += angle) {
    vertex(x + cos(a) * r2, y + sin(a) * r2);
    vertex(x + cos(a + angle / 2) * r1, y + sin(a + angle / 2) * r1);
  }
  endShape(CLOSE);
}
````
#### Mobile index
```` c++
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Sabrina Control - Mobile</title>
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
#### Server 
```` c++
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;
const path = require('path');

app.use(express.static('public'));
app.use('/desktop', express.static(path.join(__dirname, 'public/desktop')));
app.use('/mobile', express.static(path.join(__dirname, 'public/mobile')));

io.on('connection', (socket) => {
    console.log('New client connected');
    socket.on('message', (message) => {
        console.log('Received message =>', message);
        socket.broadcast.emit('message', message);
    });

    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
````

#### Micro:bit
```` c++
from microbit import *
import math

while True:
    x = accelerometer.get_x()
    y = accelerometer.get_y()
    A = button_a.is_pressed()
    B = button_b.is_pressed()
    print("{},{},{},{}".format(x, y, A, B))
    sleep(100)
````
[Link al audio](https://upbeduco-my.sharepoint.com/:u:/g/personal/emmanuel_toro_upb_edu_co/EZpajg5D_zpPit38uNkb6swByJ65Qz6nXG6TuipHi3MTuQ?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=by62Z0)
