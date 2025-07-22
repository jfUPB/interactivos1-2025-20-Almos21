# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 1

#### ¿Qué es un sistema físico interactivo?
Según comprendí por los videos los sistemas físicos interactivos son sistemas que aprovechan imputs físicos para funcionar en tiempo real y crear una experiencia interactiva que varía dependiendo de la información que vaya captando, aprovechando así la capacidad de los sistemas de seguir unas reglas y adaptarlas a las condiciones del momento o a parámetros establecidos para crear experiencias únicas y en tiempo real.

#### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?
Estos sistemas permiten experimentar en gran medida con que experiencias puedo crear aprovechando mis conocimientos en animación e ilustración, poder crear experiencias únicas para los clientes que sean innovadoras y en tiempo real y aprovechen mis conocimientos en ilustración, jugar con los colores, escenarios que cambien, efectos que acompañen la situación, extiende las posibilidades que posee mi línea de enfasís e interes (animación).

### Actividad 2
#### ¿Qué es el diseño/arte generativo?
El arte y diseño generativo aprovechan el uso de sistemas tecnológicos e interactivos para generar resultados visuales que varien, estos pueden aprovechar la capacidad de estos sistemas de seguir unas reglas impuestas mientras que a la misma vez interpretan la situación y las usan dependiendo de esto, generando diferentes resultados según datos aleatorios dentro de los parámetros establecidos o según imputs que les brindan información sobre la cual trabajar como el ejemplo de la filarmónica donde era el sonido lo que hacia que estos varíaran.

#### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?
Aprovechando lo que me permite realizar este tipo de diseño y arte podría crear programas que generen diseños como el de la filarmónica, propuestas como estas me interesan mucho porque brindan originalidad e innovación en el diseño, utilizar esto para crear proyectos que sean innovadores y atraigan interés puede beneficiarme bastante en mi vida profesional y enriquecer las experiencias que puedo ofrecer a mis usuarios o clientes.

### Actividad 3
#### En este sistemas físico interactivo identifica los inputs, outputs y el proceso.
Los imputs son las teclas presionadas en el micro bit o las acciones realizadas como sacudirlo, todo esto es procesado por el programa que dependiendo de lo que esté codificado genera diferentes respuestas estas son finalmente presentadas a través del output que sería la pantalla del micro bit que genera diferentes patrones.

### Actividad 4
#### Mi propio programa en p5.js
Para este aproveché la función de cos y el random para asignarle una posición y color random a el circulo pero siempre por encima de la función coseno.
``` js
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(100, 7);

  let x = mouseX;
  let angle = radians(mouseX);           
  let y = random(0,255) + cos(angle) * 50;          
  
  
  fill(random(0,255), random(0,255), random(0,255));
circle(x, y, 50);
}
```

![Pantallazo de resultado](<img width="1555" height="641" alt="image" src="https://github.com/user-attachments/assets/30a8fb33-d61e-410d-ad9a-f7bed603bbee" />)
