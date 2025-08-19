# Unidad 3

## 🔎 Fase: Set + Seek
### Actividad 05
#### Construye el modelo de la bomba 3.0.
<img width="1101" height="881" alt="Diagrama sin título drawio" src="https://github.com/user-attachments/assets/1730eda7-f4e5-4829-8f8c-6246edfd604c" />
Aquí podemos ver el modelo que explicaría como funciona la bomba 3.0, tomando en cuenta los eventos existentes y como afectan a los estados, haciendo en unos casos que permanezcan iguales y en otros cambien a un estado siguiente, pasando de ``CONFIG`` a ``ARMED`` y después a ``EXPLOTED`` dependiendo de los eventos.

#### Crear una tabla con los vectores de prueba.
Estado Inicial  ||         Evento         ||        Acciones        ||  Estado final
CONFIG            A o B presionados         Suma o resta tiempo      CONFIG
CONFIG               shake                  Empezar cuenta           ARMED
ARMED             Cuenta mayor a 1          Restar 1 y continuar     ARMED
ARMED             Contraseña incorrecta     Seguir en armed          ARMED
ARMED             Contraseña correcta       Parar cuenta             CONFIG
ARMED             Cuenta llega a 0          Mostrar Skull y explotar EXPLOTED
EXPLOTED          Tocar el pin logo         Reiniciar todo           CONFIG
