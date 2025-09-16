
# Evidencias de la unidad 5

## Actividad 02
Al momento de traducir los datos enviador por el micro:bit en binario a texto con el SerialTerminal se obtiene un texto extraño como este: 
D0l   8  00  8$  4  @  @  <L  <(0   D  8       ,    @L <,   8  8  @  <  8  8  4  0  4  4  8  4 
Esto puede ser debido a que el programa no es capáz de interpretar los carácteres que se le brindan, ientras que al momento de pasarlo a Hex pasa a esto 
fe 58 00 9c 00 00 fe 54 00 9c 00 00 fe
un texto que si es reconocible
Es notorio como el binario genera un texto dificil de reconocer e identificar, a diferencia del ASCII que se traduce como texto directamente
(este sería el resultado que aparece al usar ASCII:
- -708,-864,False,False
- -936,-432,False,False
)
