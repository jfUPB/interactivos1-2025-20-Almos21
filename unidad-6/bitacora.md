
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



