# 2.3 INTERRUPTOR CREPUSCULAR
## 2.3.1 Conocimientos previos
%accordion%SENSOR DE LUZ LDR%accordion%
### 2.3.1.1 SENSOR DE LUZ LDR
El LDR es una resistencia que varía su valor con la luz, cuanto más **OSCURO** más grande es su valor, por lo tanto por la ley de Ohm este módulo nos da una señal analógica que aumenta con la oscuridad. Para saber más del LDR te recomendamos [esta página de Luis Llamas](https://www.luisllamas.es/medir-nivel-luz-con-arduino-y-fotoresistencia-ldr/).
#####2.3.1.1.1 Valores umbrales
**Por software**: Los valores analógicos, [tal y como dice aquí](https://catedu.gitbooks.io/programa-arduino-mediante-codigo/content/conexiones_analgicas.html), van desde 0 a 1023, luego hay que elegir un valor umbral, nosotros hemos elegido 500.

**Por hardware**: Puedes regular el potenciómetro que tiene el módulo para que produzca el cambio cuando lo desees:

![](/assets/2019-03-07 19_34_24-Window.jpg)
%/accordion%

%accordion%SENSOR DE LUZ LDR%accordion%

###2.3.2 Módulo LED RGB Keyes
Este módulo tiene 4 pines que podemos proporcionar valores analógicos desde 0V a 5V para conseguir diferentes colores:

Pines B = Blue G = Green R = Red (-) = GND

Como Arduino no tiene valores de salida analógicos, utilizaremos los pines PWM (~)para simular tensiones variables de salida ¿no sabes lo que es PWM (~)? eso es que no te has leído [esto](https://catedu.gitbooks.io/programa-arduino-mediante-codigo/content/un_caso_especial_seales_pwm.html).

![](/assets/rgbkeyes.jpg)

En [esta página](https://tkkrlab.nl/wiki/Arduino_KY-016_3-color_LED_module) puedes encontrar más detalles de este módulo y un ejemplo curioso de utilización sin cables.
%/accordion%

##Objetivo
* Cuando el sensor LDR detecte oscuridad
    * El led RGB se enciende verde
    * Cambiamos a fondo tipo "noche"
* En caso contrario
    * el led RGB está apagado
    * el fondo es día

##Esquema
* El módulo LDR lo conectamos al pin analógico A0 
* El LED RGB lo conectamos
    * Pin 7 - Green

##Video
{% youtube %}https://www.youtube.com/watch?v=c_eyV8aCdvk&feature=youtu.be{% endyoutube%}
## Solución
Aunque lo correcto para encender el color verde habría que utilizar la señal PWM a tope, es lo mismo que poner la señal digital en HIGH, es decir estas dos instrucciones son iguales

![](/assets/2019-03-07 19_53_03-Window.jpg)
El programa lo puedes descargar [aquí](https://drive.google.com/open?id=1bV5VehaV7vf1eMwBAjru-LZ0Wh9E75Wq)
![](/assets/23interruptorcrepuscular.jpg)