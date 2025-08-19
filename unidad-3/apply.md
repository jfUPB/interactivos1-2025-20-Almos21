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
