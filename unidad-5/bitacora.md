
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
Pues esto es puede ser respondido teniendo en cuenta lo visto hasta ahora e investigando, El uso del ASCII permite una mayor legibilidad y entendimiento, es muchisimo más cómodo para comprender, facilita muchisimo el hecho de interpretar y depurar el contenido de un programa, ahora, como se vió anteriormente al cambiar por ultima vez el código y comparar uno a uno binario y ASCII se vió como este ultimo requiere mayor uso de bytes, esto puede en programas grandes afectar el rendimiento y la rapidez a comparación de el lenguaje binario.

El lenguaje binario es entonces más rápido al momento de enviar datos, los envia de manera más compacta y sencilla y lo hace más rápido, su problema por otro lado es su legibilidad, puede ser en varios casos poco eficiente debido a que puede tener más errores debido a que necesita conocer bien el formato, si no se conoce bien su estructura puede generar errores facilmente. En cuanto a diseño el ASCII es muy usado debido a que permitió estandarizar una forma de representar el texto en estos programas y es usado mayormente en todo programa que requiera algun tipo de interfaz permitiendo que aquellos trabajando en esto puedan hacerlo de manera más cómoda y sencilla, el binario por otro lado es de por si el lenguaje que utiliza todo sistema para funcionar y codificar los mensajes en esto permite como ya lo dije anteriormente más rapidez y rendimiento, es útil principalmente en programas que utilizan grandes cantidades de datos.
