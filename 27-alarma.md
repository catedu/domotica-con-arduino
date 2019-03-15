#2.7 ALARMA
##2.7.1 Conocimientos previos
%accordion%Sensor distancia por ultrasonidos%accordion%
##2.7.1.1 SENSOR DISTANCIA POR ULTRASONIDOS
![](https://catedu.gitbooks.io/programa-arduino-mediante-codigo/content/img/Captura_de_pantalla_2015-04-01_a_las_22.48.19.png)

Este sensor mide las distancias utilizando el eco:

* Un *ojo* marcado con la T es un altavoz: Emite un sonido ultrasónico fuera de lo audible
* El otro *ojo* marcado con una R es un micrófono que detecta el pulso emitido por T.

Por software hay que calcular la distancia utilizando la fórmula v=e/t donde v es la velocidad del sonido.

Si quieres saber más de este sensor mira esta página de [Luis Llamas.](https://www.luisllamas.es/medir-distancia-con-arduino-y-sensor-de-ultrasonidos-hc-sr04/)

%/accordion%


%accordion%Por qué elegimos este sensor%accordion%

En *mBlock* ya lo hace esta instrucción por eso nos gusta este sensor por la sencillez de programación y por la precisión:

![](/assets/ordenultrasonico.jpg)

Mientras que en código ya es otra cosa, [mira esta página](https://catedu.gitbooks.io/programa-arduino-mediante-codigo/content/montaje_7_medicin_de_la_distancia.html).


%/accordion%

##2.7.2 Objetivo

* Si se pulsa el botón de activación
    * Si la alarma no está activada
        * **Activa** la alarma, es decir *está vigilando*.
    * Si la alarma está activada
        * **Desactiva** la alarma, *deja de vigilar*.
    * Si la alarma está disparada
        * Anula el disparo y desactiva la alarma
* Si la alarma está activada:
    * Está encendido el led verde para indicar que *está vigilando*.
    * Si detecta un *intruso* a menos de 10 cm
        * Se **dispara** la alarma, es decir se enciende la luz roja y el buzzer de forma intermitente, no se apaga hasta que se pulsa el interruptor.
        

###OJO
Haremos un proyecto **totalmente nuevo**, debido a que mBlock no aguanta con todo, incluso este programa suele *colgarse* luego de vez en cuando hay que dar a *Actualizar Firmware*
Ya lo comentamos en desventajas en el capítulo [2.1 Programando con mBlock](/21-programacion-mblock.md)

##2.7.3 Conexiones

* Entradas y salidas digitales
    * D3 Buzzer
    * D5 Blue de led RGB
    * D6 Red de led RGB
    * D7 Green de led RGB
    * D12 Echo del sensor de ultrasonidos
    * D13 Trg del sensor de ultrasonidos
* Entradas y salidas analógicas
    * A4 Pulsador

##2.7.4 Video
{% youtube %}https://youtu.be/RB7K16FhHlg{% endyoutube%}
##2.7.5 Solución
Haremos programación con bloques, este es el programa principal:

![](/assets/alarma1.jpg)

La activación o no de la alarma y la anulación del disparo:

![](/assets/alarma2.jpg)

El sonido de la alarma y la intermitencia del rojo

![](/assets/alarma3.jpg)

Al inicio hay que resetear todo:

![](/assets/alarma4.jpg)

El bloque de vigilar

![](/assets/alarma5.jpg)