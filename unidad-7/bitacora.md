
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
- Primero que nada el navegador captura el menaje movil que recibe
