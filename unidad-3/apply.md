# Unidad 3


## 🛠 Fase: Apply
let Time = 20;
let startMs;
let estado = 'CONFIG'
let buttonA, buttonB, buttonS, buttonT;
    
function setup(){
  createCanvas (400,400);
  background(220);
  textSize(40);
  textAlign(CENTER,CENTER);
  
  buttonA = createButton('A')
  buttonA.position(80,300);
  
  buttonB = createButton('B')
  buttonB.position(350,300);
  
  buttonS = createButton('S')
  buttonS.position(200,300);
  
  buttonT = createButton('T')
  buttonT.position(200,50);
   
}


function draw(){
  background(220);
  
  if (estado === 'CONFIG'){
    if (buttonA.mousePressed){
        Time = min(60,Time + 1)
        }
    else if (buttonB.mousePressed){
        Time = min(10,Time -1 )
    }
    
    else if (buttonS.mousePressed){
      startMs = ms();
      estado = 'ARMED';
    }
    
   text('Tiempo: ' + nf(Time), width/2, height/2);
  }
  else if (estado === 'ARMED'){
    let entero = max((ms() - startMs) / 1000);
    let faltante = max(Time - entero, 0);
    text('Explotará en: ' + nf(faltante, 2), width/2, height/2 )
    
    if(faltante === 0){
      estado = 'EXPLOTED';
    }
  }
  else if (estado === 'EXPLOTED'){
    text('EXPLOTÓ', widht/2, height/2);
    if (buttonT.mousePressed){
      estado = 'CONFIG'
    }
  }
}

function keyPressed() {
  keyValue = key.toUpperCase();
  if(validChars.includes(keyValue)){
    console.log(keyValue);
    port.write(keyValue);
  }
}

......


let PASSWORD = ['A', 'B', 'A'];
let key = [];
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
    fill(255, 0, 0);
    text(" BOOM ", width / 2, height / 2);
  }
}

function keyPressed() {
  keyValue = key.toUpperCase();
  if(validChars.includes(keyValue)){
    console.log(keyValue);
    port.write(keyValue);
  }
  
function keyIsPressed() {
  if (state === "CONFIG") {
    if (key === "A") {
      count = min(count + 1, 60);
    } 
    else if (key === "B") {
      count = max(10, count - 1);
    } 
    else if (key === "S") { // shake
      startTime = millis();
      state = "ARMED";
    }
  } 
  
  else if (state === "ARMED") {
    if (key === "A" || key === "B") {
      key.push(key);
      keyIndex++;

      if (keyIndex === PASSWORD.length) {
        let passOk = true;
        for (let i = 0; i < PASSWORD.length; i++) {
          if (key[i] !== PASSWORD[i]) {
            passOk = false;
            break;
          }
        }

        if (passOk) {
          count = 20;
          state = "CONFIG";
        }
        key = [];
        keyIndex = 0;
      }
    }
  } 
  
  else if (state === "EXPLODED") {
    if (key === "R") { // reset
      count = 20;
      startTime = millis();
      state = "CONFIG";
    }
  }
}
