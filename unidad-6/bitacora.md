
# Evidencias de la unidad 6

## Actividad 01
<a name="1"></a>
- <img width="708" height="260" alt="image" src="https://github.com/user-attachments/assets/08425367-7140-4ec7-8db6-aaf3e1dc7616" />

Al ejecutar npm install salió esto, su propósito entonces supongo que es el de descargar en la dirección del computador indicada cada uno de los paquetes necesarios del servidor e informar si esto fue existoso y su estado.

-<img width="731" height="132" alt="image" src="https://github.com/user-attachments/assets/18bda5f4-9920-4bbb-82d0-700fbc83a73a" />

Apareció este mensaje, creo que indica que ya esta preparado pa ra funcionar y que el servidor esta atento a la actividad presente para funcionar

- <img width="1668" height="965" alt="image" src="https://github.com/user-attachments/assets/b205b6c9-746b-4d67-85a6-723e96400e69" />

Veo en las ventanas separadas estas dos esferas conectadas entre sí por una línea que se mueve junto con las ventanas, no importa que esten separadas las ventanas, este programa puede identificar donde esta ubicada cada una y unirlas en todo momento.

-<img width="748" height="79" alt="image" src="https://github.com/user-attachments/assets/442a4397-cec0-42f5-b43d-ced316b94467" />

Identifica mi ID y establece que me conecté y empieza a recibir datos.

-Pasa lo mismo que ya expliqué anteriormente, pero adicionalmente en el terminal sale lo siguiente:
<img width="728" height="305" alt="image" src="https://github.com/user-attachments/assets/95ea3d53-6a96-4b71-9297-0b738c5131c9" />

Se ve como va recibiendo los datos e identificando quien se concecto y desde que punto y las dimensiones de la ventana para asi saber como configurar el programa
## Actividad 02
<a name="2"></a>
- Si esta "rampa" que me permite acceder a la "carretera" (internet) se cortará lo más probable es que no podría entonces llegar a acceder a esta haciendo imposible para .mi conectarme a el internet y poder navegarlo.
- Ejemplos que se me pueden ocurrir de servidor - cliente serían por ejemplo el restaurante donde el cliente somos nosotros y le pedimos al mesero (servidor) un plato del menú disponible y nos entrega la comida que pedimos. Otro por ejemplo es algo parecido que sería una tienda, vamos a pedir un producto en específico y al estar disponible se nos entrega esto que pedimos.
- Voy a poner como ejemplo esta url: ``https://www.youtube.com/watch?v=V9vuCByb6js&list=RDV9vuCByb6js&start_radio=1`` que lleva a un video musical, el protocolo aquí sería ``https://`` el nombre del dominio es ``www.youtube.com`` si tomamos el ejemplo brindado de la biblioteca y de los dominios siendo como los edificios youtube es aqui el edificio al que quiero ir y el video es la sala específica a la que quiero entrar, esta sería en este caso esta parte ``watch?v=V9vuCByb6js&list=RDV9vuCByb6js&start_radio=1`` si me voy a el link sin esta ultima parte me lleva a la página predeterminada de youtube, el inicio que muestra videos recomendados para mi.
- En todos los protocolos alguien pide (cliente) y alguien responde (servidor o dispositivo), como en el micro bit que recibia un comando y respondia con datos, tambien son similares en que ambos necesitan una manera clara de como comprender los mensajes que se envian.
- Principalmente las diferencias se encuentran en la complejidad de estos, binario y ASCII son pensados para dispositivos más simples como el micro bit, el https puede soportar mucho más tipo de formatos, de dispositivos y en general cosas más complejas.
- El https necesita mucho más por lo importante que es y por lo mucho que abarca, es muy diferente conectar de manera alambrica a un micro bit a interconectar dispositivos a miles de kilometros y no solo uno sino muchos, todo esto requiere obligatoriamente un protocolo mucho más complejo si se quiere que funcione de manera estable, correcta y rápida.
- En este ejemplo el html son los campos de fuerza más el boton, el css son los colores la fuente y los tamaños y java las validaciones y datos dinámicod
-La ventaja de utilizar esto en vez del draw es que la página no se esta actualizando de forma constante e indefinida sino que espera a que la persona realmente haga algo, esto brinda eficiencia en muchos sentidos.
-Creo que usar JavaScript tanto en el cliente como en el servidor es útil porque permite trabajar con un solo lenguaje en toda la aplicación. Eso significa que los desarrolladores no tienen que aprender lenguajes diferentes para cada parte, lo que hace más fácil compartir código, entender mejor el proyecto y trabajar en equipo. Además, se puede reutilizar lógica lo que ahorra tiempo y reduce errores.
-La diferencia principal es que en HTTP tradicional el cliente siempre tiene que hacer una petición para que el servidor responda, mientras que con WebSockets/Socket.IO se abre una conexión permanente donde ambos pueden enviarse datos en tiempo real sin necesidad de pedirlos cada vez. Esto es muy útil en aplicaciones con interacción en tiempo real como juegos, chats en linea, etc. donde la info se tiene que modificar constantemente.
## Actividad 03

<a name="3"></a>
-Sique funcionando en page1, mientras que en pagina_uno me aparece esto 
<img width="1919" height="546" alt="image" src="https://github.com/user-attachments/assets/3eae9257-68b8-4b7f-bd61-5829a56f716e" />

probablemente se deba a que no supe bien que se supone que cambie en el código, investigando me di cuenta que de hacerlo bien debería funcionar en pagina_uno, debido a que el servidor debe responder a las rutas que tiene configuradas y no inventarselas.

-<img width="719" height="123" alt="image" src="https://github.com/user-attachments/assets/19b9da17-8cba-45b4-83a0-a5c0abdc5034" />

El ID es el mismo, y al desconectarse avisa cual se desconecto, esto demuestra que es su manera de identificar a alguien, sin embargo al ver los ID de las anteriores veces este cambió, asi que puedo creer que lo que sucede es que este se mantiene como el mismo para un cliente en específico cada vez dentro de la vez donde se esta corriendo, al cerrarlo y reabrirlo se cambia pero se mantiene este nuevo dentro de la nueva aplicación.

-Cada que muevo uno u otro cambian los datos de la posición, y se registra win2update al mover el page2 y visceversa
<img width="725" height="141" alt="image" src="https://github.com/user-attachments/assets/94b99b66-5008-4447-b173-3e935e2d1957" />

<a name="4"></a>
-Al cambiar el código se deja de actualizar bien en page2, esto porque esta parte estaba encargada de enviar estos datos a page 2 para que funcionara de manera correcta

-Cambiando el port a 3001 solo funciona al terminar en esto, al 3000 no, y en la terminar dice que esta escuchando es en el 3001 
<img width="1330" height="877" alt="image" src="https://github.com/user-attachments/assets/4d6176a2-a061-4cf5-9340-529a85af94cf" />

<img width="402" height="17" alt="image" src="https://github.com/user-attachments/assets/460ab4c2-4386-48e4-8ebd-5af7d7c4ca3a" />

El port le indica a la variable listening donde debe hacerlo y es allí donde se envian estos datos.

### Actividad 05
(no mirar, la mayoria de esto lo hice con ia pero quise ponerlo por lo interesante que quedó, tenpía la idea de hacer un eclipse y que el fondo cambiara a uno nocturno al acercarse, simulando el efecto)
Page 2, luna
````js
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Luna - Página 2</title>
    <script src="/socket.io/socket.io.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            width: 100vw;
            height: 100vh;
            overflow: hidden;
            transition: background 0.5s ease;
            position: relative;
        }
        
        #moon {
            position: absolute;
            width: 120px;
            height: 120px;
            background: radial-gradient(circle at 35% 35%, #f0f0f0 0%, #d0d0d0 50%, #a0a0a0 100%);
            border-radius: 50%;
            cursor: move;
            box-shadow: inset -10px -10px 30px rgba(0, 0, 0, 0.3),
                        0 0 30px rgba(0, 0, 0, 0.5);
            z-index: 2;
            transition: box-shadow 0.3s ease;
        }
        
        /* Cráteres de la luna */
        #moon::before {
            content: '';
            position: absolute;
            width: 20px;
            height: 20px;
            background: radial-gradient(circle, #b0b0b0 0%, #909090 100%);
            border-radius: 50%;
            top: 30%;
            left: 40%;
            box-shadow: inset -2px -2px 5px rgba(0, 0, 0, 0.5);
        }
        
        #moon::after {
            content: '';
            position: absolute;
            width: 15px;
            height: 15px;
            background: radial-gradient(circle, #b0b0b0 0%, #909090 100%);
            border-radius: 50%;
            top: 60%;
            left: 55%;
            box-shadow: inset -2px -2px 5px rgba(0, 0, 0, 0.5);
        }
        
        #sun-glow {
            position: absolute;
            border-radius: 50%;
            pointer-events: none;
            z-index: 0;
            transition: all 0.1s ease;
            display: none;
        }
        
        .status {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.9);
            padding: 15px 25px;
            border-radius: 10px;
            font-family: 'Arial', sans-serif;
            font-size: 14px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            z-index: 1000;
        }
        
        .status-indicator {
            display: inline-block;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-right: 8px;
            background: #ff4444;
            animation: pulse 2s infinite;
        }
        
        .status-indicator.synced {
            background: #44ff44;
            animation: none;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        
        .eclipse-info {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 10px 20px;
            border-radius: 20px;
            font-family: 'Arial', sans-serif;
            font-size: 16px;
            display: none;
        }
        
        .corona {
            position: absolute;
            width: 160px;
            height: 160px;
            border-radius: 50%;
            pointer-events: none;
            z-index: 1;
            display: none;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
        
        .stars {
            position: fixed;
            width: 2px;
            height: 2px;
            background: white;
            border-radius: 50%;
            opacity: 0;
            transition: opacity 0.5s ease;
        }
    </style>
</head>
<body>
    <div class="status">
        <span class="status-indicator" id="statusIndicator"></span>
        <span id="statusText">Esperando conexión...</span>
    </div>
    
    <div id="sun-glow"></div>
    <div id="moon">
        <div class="corona" id="corona"></div>
    </div>
    <div class="eclipse-info" id="eclipseInfo">🌑 ECLIPSE TOTAL 🌑</div>
    
    <script>
        const socket = io();
        const moon = document.getElementById('moon');
        const sunGlow = document.getElementById('sun-glow');
        const corona = document.getElementById('corona');
        const statusIndicator = document.getElementById('statusIndicator');
        const statusText = document.getElementById('statusText');
        const eclipseInfo = document.getElementById('eclipseInfo');
        const body = document.body;
        
        let isDragging = false;
        let offset = { x: 0, y: 0 };
        let otherWindowData = null;
        let isSynced = false;
        
        // Crear estrellas
        for (let i = 0; i < 100; i++) {
            const star = document.createElement('div');
            star.className = 'stars';
            star.style.left = Math.random() * 100 + '%';
            star.style.top = Math.random() * 100 + '%';
            star.style.width = (Math.random() * 2 + 1) + 'px';
            star.style.height = star.style.width;
            body.appendChild(star);
        }
        
        const stars = document.querySelectorAll('.stars');
        
        // Posición inicial centrada
        moon.style.left = (window.innerWidth / 2 - 60) + 'px';
        moon.style.top = (window.innerHeight / 2 - 60) + 'px';
        
        function getWindowData() {
            const rect = moon.getBoundingClientRect();
            return {
                x: rect.left + window.screenX,
                y: rect.top + window.screenY,
                width: rect.width,
                height: rect.height,
                centerX: rect.left + window.screenX + rect.width / 2,
                centerY: rect.top + window.screenY + rect.height / 2
            };
        }
        
        function sendUpdate() {
            const data = getWindowData();
            socket.emit('win2update', data, socket.id);
        }
        
        function calculateDistance() {
            if (!otherWindowData) return null;
            
            const myData = getWindowData();
            const dx = otherWindowData.centerX - myData.centerX;
            const dy = otherWindowData.centerY - myData.centerY;
            const distance = Math.sqrt(dx * dx + dy * dy);
            
            return { distance, dx, dy };
        }
        
        function updateVisuals() {
            const calc = calculateDistance();
            if (!calc) return;
            
            const { distance, dx, dy } = calc;
            const maxDistance = 500;
            const proximity = Math.max(0, 1 - (distance / maxDistance));
            
            // Calcular el progreso de día a noche
            const nightProgress = Math.pow(proximity, 2);
            
            // Colores del cielo
            const skyDay = { r: 135, g: 206, b: 235 };
            const skyNight = { r: 10, g: 10, b: 30 };
            
            const currentR = skyDay.r + (skyNight.r - skyDay.r) * nightProgress;
            const currentG = skyDay.g + (skyNight.g - skyDay.g) * nightProgress;
            const currentB = skyDay.b + (skyNight.b - skyDay.b) * nightProgress;
            
            body.style.background = `rgb(${currentR}, ${currentG}, ${currentB})`;
            
            // Mostrar estrellas
            stars.forEach(star => {
                star.style.opacity = nightProgress * 0.8;
            });
            
            // Mostrar brillo del sol detrás de la luna
            if (distance < 200 && otherWindowData) {
                sunGlow.style.display = 'block';
                sunGlow.style.width = otherWindowData.width + 'px';
                sunGlow.style.height = otherWindowData.height + 'px';
                
                const sunLocalX = otherWindowData.x - window.screenX;
                const sunLocalY = otherWindowData.y - window.screenY;
                
                sunGlow.style.left = sunLocalX + 'px';
                sunGlow.style.top = sunLocalY + 'px';
                
                const glowIntensity = Math.max(0, 1 - (distance / 200));
                sunGlow.style.background = `radial-gradient(circle, 
                    rgba(255, 215, 0, ${glowIntensity * 0.3}) 0%, 
                    rgba(255, 165, 0, ${glowIntensity * 0.2}) 50%, 
                    transparent 70%)`;
                
                // Eclipse total - mostrar corona
                if (distance < 50) {
                    eclipseInfo.style.display = 'block';
                    corona.style.display = 'block';
                    const coronaIntensity = Math.max(0, 1 - (distance / 50));
                    corona.style.boxShadow = `
                        0 0 40px rgba(255, 255, 255, ${coronaIntensity * 0.8}),
                        0 0 80px rgba(255, 200, 100, ${coronaIntensity * 0.6}),
                        0 0 120px rgba(255, 180, 50, ${coronaIntensity * 0.4})
                    `;
                } else {
                    eclipseInfo.style.display = 'none';
                    corona.style.display = 'none';
                }
            } else {
                sunGlow.style.display = 'none';
                eclipseInfo.style.display = 'none';
                corona.style.display = 'none';
            }
        }
        
        // Drag and drop
        moon.addEventListener('mousedown', (e) => {
            isDragging = true;
            offset.x = e.clientX - moon.offsetLeft;
            offset.y = e.clientY - moon.offsetTop;
            moon.style.cursor = 'grabbing';
        });
        
        document.addEventListener('mousemove', (e) => {
            if (isDragging) {
                moon.style.left = (e.clientX - offset.x) + 'px';
                moon.style.top = (e.clientY - offset.y) + 'px';
                sendUpdate();
                updateVisuals();
            }
        });
        
        document.addEventListener('mouseup', () => {
            if (isDragging) {
                isDragging = false;
                moon.style.cursor = 'move';
                sendUpdate();
            }
        });
        
        // Socket events
        socket.on('connect', () => {
            console.log('Connected to server');
            statusText.textContent = 'Conectado - Luna';
            sendUpdate();
            socket.emit('requestSync');
        });
        
        socket.on('getdata', (payload) => {
            if (payload.from === 'page1') {
                otherWindowData = payload.data;
                updateVisuals();
                if (!isSynced) {
                    socket.emit('confirmSync');
                    isSynced = true;
                }
            }
        });
        
        socket.on('fullySynced', (synced) => {
            if (synced) {
                statusIndicator.classList.add('synced');
                statusText.textContent = '✓ Sincronizado - Luna';
            } else {
                statusIndicator.classList.remove('synced');
                statusText.textContent = 'Esperando Sol...';
            }
        });
        
        socket.on('peerDisconnected', () => {
            otherWindowData = null;
            isSynced = false;
            sunGlow.style.display = 'none';
            corona.style.display = 'none';
            eclipseInfo.style.display = 'none';
            body.style.background = 'rgb(135, 206, 235)';
            stars.forEach(star => star.style.opacity = 0);
        });
        
        // Enviar updates periódicos
        setInterval(() => {
            if (!isDragging) {
                sendUpdate();
                updateVisuals();
            }
        }, 100);
        
        // Initial update
        sendUpdate();
    </script>
</body>
</html>
````
Page 1, sol
```` js
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sol - Página 1</title>
    <script src="/socket.io/socket.io.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            width: 100vw;
            height: 100vh;
            overflow: hidden;
            transition: background 0.5s ease;
            position: relative;
        }
        
        #sun {
            position: absolute;
            width: 120px;
            height: 120px;
            background: radial-gradient(circle, #FFD700 0%, #FFA500 50%, #FF8C00 100%);
            border-radius: 50%;
            cursor: move;
            box-shadow: 0 0 60px rgba(255, 215, 0, 0.8),
                        0 0 100px rgba(255, 165, 0, 0.6),
                        0 0 140px rgba(255, 140, 0, 0.4);
            z-index: 1;
            transition: box-shadow 0.3s ease;
        }
        
        #moon-shadow {
            position: absolute;
            border-radius: 50%;
            pointer-events: none;
            z-index: 2;
            transition: all 0.1s ease;
            display: none;
        }
        
        .status {
            position: fixed;
            top: 20px;
            left: 20px;
            background: rgba(255, 255, 255, 0.9);
            padding: 15px 25px;
            border-radius: 10px;
            font-family: 'Arial', sans-serif;
            font-size: 14px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            z-index: 1000;
        }
        
        .status-indicator {
            display: inline-block;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-right: 8px;
            background: #ff4444;
            animation: pulse 2s infinite;
        }
        
        .status-indicator.synced {
            background: #44ff44;
            animation: none;
        }
        
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        
        .eclipse-info {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 10px 20px;
            border-radius: 20px;
            font-family: 'Arial', sans-serif;
            font-size: 16px;
            display: none;
        }
        
        .stars {
            position: fixed;
            width: 2px;
            height: 2px;
            background: white;
            border-radius: 50%;
            opacity: 0;
            transition: opacity 0.5s ease;
        }
    </style>
</head>
<body>
    <div class="status">
        <span class="status-indicator" id="statusIndicator"></span>
        <span id="statusText">Esperando conexión...</span>
    </div>
    
    <div id="sun"></div>
    <div id="moon-shadow"></div>
    <div class="eclipse-info" id="eclipseInfo">🌑 ECLIPSE TOTAL 🌑</div>
    
    <script>
        const socket = io();
        const sun = document.getElementById('sun');
        const moonShadow = document.getElementById('moon-shadow');
        const statusIndicator = document.getElementById('statusIndicator');
        const statusText = document.getElementById('statusText');
        const eclipseInfo = document.getElementById('eclipseInfo');
        const body = document.body;
        
        let isDragging = false;
        let offset = { x: 0, y: 0 };
        let otherWindowData = null;
        let isSynced = false;
        
        // Crear estrellas
        for (let i = 0; i < 100; i++) {
            const star = document.createElement('div');
            star.className = 'stars';
            star.style.left = Math.random() * 100 + '%';
            star.style.top = Math.random() * 100 + '%';
            star.style.width = (Math.random() * 2 + 1) + 'px';
            star.style.height = star.style.width;
            body.appendChild(star);
        }
        
        const stars = document.querySelectorAll('.stars');
        
        // Posición inicial centrada
        sun.style.left = (window.innerWidth / 2 - 60) + 'px';
        sun.style.top = (window.innerHeight / 2 - 60) + 'px';
        
        function getWindowData() {
            const rect = sun.getBoundingClientRect();
            return {
                x: rect.left + window.screenX,
                y: rect.top + window.screenY,
                width: rect.width,
                height: rect.height,
                centerX: rect.left + window.screenX + rect.width / 2,
                centerY: rect.top + window.screenY + rect.height / 2
            };
        }
        
        function sendUpdate() {
            const data = getWindowData();
            socket.emit('win1update', data, socket.id);
        }
        
        function calculateDistance() {
            if (!otherWindowData) return null;
            
            const myData = getWindowData();
            const dx = otherWindowData.centerX - myData.centerX;
            const dy = otherWindowData.centerY - myData.centerY;
            const distance = Math.sqrt(dx * dx + dy * dy);
            
            return { distance, dx, dy };
        }
        
        function updateVisuals() {
            const calc = calculateDistance();
            if (!calc) return;
            
            const { distance, dx, dy } = calc;
            const maxDistance = 500;
            const proximity = Math.max(0, 1 - (distance / maxDistance));
            
            // Calcular el progreso de día a noche (0 = día, 1 = noche)
            const nightProgress = Math.pow(proximity, 2);
            
            // Colores del cielo
            const skyDay = { r: 135, g: 206, b: 235 };
            const skyNight = { r: 10, g: 10, b: 30 };
            
            const currentR = skyDay.r + (skyNight.r - skyDay.r) * nightProgress;
            const currentG = skyDay.g + (skyNight.g - skyDay.g) * nightProgress;
            const currentB = skyDay.b + (skyNight.b - skyDay.b) * nightProgress;
            
            body.style.background = `rgb(${currentR}, ${currentG}, ${currentB})`;
            
            // Mostrar estrellas
            stars.forEach(star => {
                star.style.opacity = nightProgress * 0.8;
            });
            
            // Mostrar sombra de la luna sobre el sol
            if (distance < 200 && otherWindowData) {
                moonShadow.style.display = 'block';
                moonShadow.style.width = otherWindowData.width + 'px';
                moonShadow.style.height = otherWindowData.height + 'px';
                
                const moonLocalX = otherWindowData.x - window.screenX;
                const moonLocalY = otherWindowData.y - window.screenY;
                
                moonShadow.style.left = moonLocalX + 'px';
                moonShadow.style.top = moonLocalY + 'px';
                
                const shadowIntensity = Math.max(0, 1 - (distance / 200));
                moonShadow.style.background = `radial-gradient(circle, rgba(0,0,0,${shadowIntensity * 0.9}) 0%, rgba(0,0,0,${shadowIntensity * 0.5}) 50%, transparent 70%)`;
                
                // Eclipse total
                if (distance < 50) {
                    eclipseInfo.style.display = 'block';
                    sun.style.boxShadow = `0 0 80px rgba(255, 215, 0, ${1 - shadowIntensity}),
                                           0 0 120px rgba(255, 165, 0, ${0.8 - shadowIntensity}),
                                           0 0 160px rgba(255, 140, 0, ${0.6 - shadowIntensity})`;
                } else {
                    eclipseInfo.style.display = 'none';
                    sun.style.boxShadow = '';
                }
            } else {
                moonShadow.style.display = 'none';
                eclipseInfo.style.display = 'none';
                sun.style.boxShadow = '';
            }
        }
        
        // Drag and drop
        sun.addEventListener('mousedown', (e) => {
            isDragging = true;
            offset.x = e.clientX - sun.offsetLeft;
            offset.y = e.clientY - sun.offsetTop;
            sun.style.cursor = 'grabbing';
        });
        
        document.addEventListener('mousemove', (e) => {
            if (isDragging) {
                sun.style.left = (e.clientX - offset.x) + 'px';
                sun.style.top = (e.clientY - offset.y) + 'px';
                sendUpdate();
                updateVisuals();
            }
        });
        
        document.addEventListener('mouseup', () => {
            if (isDragging) {
                isDragging = false;
                sun.style.cursor = 'move';
                sendUpdate();
            }
        });
        
        // Socket events
        socket.on('connect', () => {
            console.log('Connected to server');
            statusText.textContent = 'Conectado - Sol';
            sendUpdate();
            socket.emit('requestSync');
        });
        
        socket.on('getdata', (payload) => {
            if (payload.from === 'page2') {
                otherWindowData = payload.data;
                updateVisuals();
                if (!isSynced) {
                    socket.emit('confirmSync');
                    isSynced = true;
                }
            }
        });
        
        socket.on('fullySynced', (synced) => {
            if (synced) {
                statusIndicator.classList.add('synced');
                statusText.textContent = '✓ Sincronizado - Sol';
            } else {
                statusIndicator.classList.remove('synced');
                statusText.textContent = 'Esperando Luna...';
            }
        });
        
        socket.on('peerDisconnected', () => {
            otherWindowData = null;
            isSynced = false;
            moonShadow.style.display = 'none';
            eclipseInfo.style.display = 'none';
            body.style.background = 'rgb(135, 206, 235)';
            stars.forEach(star => star.style.opacity = 0);
        });
        
        // Enviar updates periódicos
        setInterval(() => {
            if (!isDragging) {
                sendUpdate();
                updateVisuals();
            }
        }, 100);
        
        // Initial update
        sendUpdate();
    </script>
</body>
</html>
````
<img width="1803" height="897" alt="image" src="https://github.com/user-attachments/assets/1d74955b-4955-43fa-8ae9-deeb0f5f7608" />

<img width="924" height="956" alt="image" src="https://github.com/user-attachments/assets/b0bf4959-6868-4aad-b555-99ec3eeec228" />

<img width="924" height="923" alt="image" src="https://github.com/user-attachments/assets/b81d842e-a1e5-4c30-baf2-56563bed31c7" />


## Autoevaluación
### Nota total: 2.7/5
### Actividad 01 autoevaluación: 
Nota propuesta: 1/1
Esta actividad era enfocada a un analisis e interacción inicial del servidor, siento que logré hacer esto bien además de [agregar](#1)  primeras hipótesis y evidencias.

### Actividad 02 autoevaluación: 
Nota propuesta: 1/1
Esta actividad era enfocada al [análisis](#2) de nuevos conceptos y entendimiento de estos, siento que con lo que escribí cumplí con lo que se pedía en esta actividad.

### Actividad 03 autoevaluación: 
Nota propuesta: 0.7/1
Esta actividad era enfocada a la experimentación y análisis de estos resultados, aquí tuve [problemas](#3) en algunas partes y no pude realizar bien la experimentación teniendo que buscar o inferir cual sería en resultado en base a info de internet o info tomada de experiencias de compañeros que si lo pudieron realizar bien, también siento que pude profundizar un poco más en el [análisis](#4).




