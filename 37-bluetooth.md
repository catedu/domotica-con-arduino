#3.7 BLUETOOTH
#3.7.1 Conocimientos previos
Tienes que visitar las siguientes páginas de la [Unidad 4 Comunicaciones con Arduino](https://catedu.gitbooks.io/programa-arduino-mediante-codigo/content/arduino_y_mvil.html):

* ¿Qué es el [HC-06](https://catedu.gitbooks.io/programa-arduino-mediante-codigo/content/mdulo_bluetooth.html)?
* [La APP](https://catedu.gitbooks.io/programa-arduino-mediante-codigo/content/la_app.html) que tienes que intalarte
    
* [Vincular tu móvil con el HC-06](https://catedu.gitbooks.io/programa-arduino-mediante-codigo/content/vincular_mvil.html)

> Aprende a configurar los botones de la APP !! diapositiva 12 pero en vez de Up, Down, Right y Left los que se establezcan en 3.7.2 Objetivos.

<iframe width="100%" height="569" src="https://docs.google.com/presentation/d/e/2PACX-1vT0vG1z61MuZXKmdiw4ga7z15FlQfeussqDNYzMauJSZUU2G2NlL7M-JjXb4PFT4YTigj9Yal8PzHmR/embed?start=false&amp;loop=false&amp;delayms=3000" frameborder="0" allowfullscreen="allowfullscreen" mozallowfullscreen="mozallowfullscreen" webkitallowfullscreen="webkitallowfullscreen"></iframe>

* [Configuración avanzada](https://catedu.gitbooks.io/programa-arduino-mediante-codigo/content/configuracion_avanzada.html) pues **nosotros conectaremos el HC-06 en los pines digitales D11 y D12** y no en D0 y D1 pues están ocupados con la comunicación del ordenador.

##3.7.2 Objetivos

Controlar nuestra casa con el móvil, para ello vamos a definir los siguientes comandos:

| COMANDO     | VOZ    | DATO   |  descripción                                           |
|-------------|--------|--------|--------------------------------------------------------|
| Comando 1   | abrir  | A      | abrir la puerta y cierra automáticamente               |
| Comando 2   | puerta | P      | abrir/cerrar la puerta                                 |
| Comando 3   | alarma | L      | activar/desactivar la alarma                           |
| Comando 4   | pit    | T       | hace un pit                                            |
| Comando 5   | rojo   | R      | enciende luz interior roja                             |
| Comando 6   | azul   | B      | enciende luz interior azul                             |
| Comando 7   | apaga  | O      | apaga luces interiores                                 |

Lo tienes que hacer así:

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vSCv2j25rIQxh6pHjMM4n4AXttDDetQPL93qMrYfQO2p-BVC6tSzeRVgU7nVq4_pXEnLedrvF7LTM4V/embed?start=false&loop=false&delayms=3000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

##3.7.3 Conexión eléctrica

* Conectaremos Vcc y GND del HC06 igual que antes en la placa protoboard *sí ya sé que casi no queda sitio, es el último, lo prometo*
* TX de HC06 al pin D11
* RX de HC06 al pin D12

##3.7.4 Vídeo