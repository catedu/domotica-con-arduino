#2.4 Apertura puerta

##2.4.1 Conocimientos previos

%accordion%SERVO%accordion%
###2.4.1.1 SERVOMOTORES
Visita [esta página](https://catedu.gitbooks.io/programa-arduino-mediante-codigo/content/montaje_1_testea_tu_servo.html) para que veas dos vídeos y entiendas la diferencia entre:
* Servos convencionales
* Servos de rotación contínua

![](/assets/servo.jpg)

Tranquilo, que el servo que nos interesa es un servo convencional donde simplemente se fija el ángulo con la instrucción en mBlock

![](/assets/instruccionservomblock.jpg)

Si quieres saber más sobre servos te aconsejamos visitar [esta página.](https://www.luisllamas.es/controlar-un-servo-con-arduino/)

%/accordion%

%accordion%INTERRUPTOR TÁCTIL%accordion%
###2.4.1.2 Interruptor táctil

![](/assets/2019-03-08 13_15_12-1.3 Kit de préstamo de CATEDU · DOMOTICA CON ARDUINO.jpg)

No tiene mucho misterio: detecta una acumulación de carga y dispara un pulso positivo.

%/accordion%

%accordion%BUZZER ACTIVO%accordion%
###2.4.1.3 Buzzer activo

![](/assets/buzzer.jpg)

La diferencia con el pasivo es que no es necesario enviarle pulsos para que emita una frecuencia, sólo tenemos que dar la orden y él reproduce un tono.

**Ojo que funciona con lógica negativa** es decir:
* si queremos que suene tenemos que enviar un LOW.
* si queremos que no suene tenemos que enviar un HIGH

Si quieres saber más de este componente visita [esta página](https://www.luisllamas.es/arduino-buzzer-activo/)

%/accordion%

##2.4.2 Objetivo

* Cuando se pulse el interruptor táctil (sería como una llave táctil)
    * Se abre la puerta
* Al cabo de 5 segundos, tiempo suficiente para entrar
    * Se avisa que la puerta se va a cerrar con 3 pulsos buzzer y cambiando el color el sprite del Panda de mBlock
    * Se cierra la puerta
    
##2.4.3 Esquema

* pin 2 digital: El interruptor táctil touchless.
* pin 3 digital: El buzzer activo.
* pin 4 digital: Servo de la puerta.

![](/assets/esquema-llave.jpg)

##2.4.4 Video

{% youtube %}https://youtu.be/bBA3GEhLmRg{% endyoutube%}

##2.4.5 Solución

El programa lo puedes descargar [aquí](https://drive.google.com/open?id=1bV5VehaV7vf1eMwBAjru-LZ0Wh9E75Wq)

![](/assets/codigollave.jpg)

El objeto **puerta** tiene este sencillo programa:

![](/assets/codigopuerta.jpg)
