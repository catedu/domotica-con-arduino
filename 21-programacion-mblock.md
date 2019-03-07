#2.1 Programación mBlock

Es un programa especializado en el manejo de los robots de Makeblock ([ver cursos de mBot en Aularagon](https://catedu.gitbooks.io/robotica/content/)), estos robots están basados en Arduino por lo tanto este programa también puede programarlos

![](http://66.media.tumblr.com/d2949cd218d9678d77cdf61087beb616/tumblr_inline_nj1lt0pIeA1qmn7ka.jpg)

Se puede descargar gratuitamente en http://www.mblock.cc/

Recomendamos en Windows [la versión 3](http://www.mblock.cc/mblock-software/) 


![](/assets/MBLCCK.jpg)

## 2.1.1 NO PROGRAMAMOS DIRECTAMENTE EN EL ARDUINO
mBlock (y los otros S4A, Snap4Arduino... también) **NO PROGRAMA DIRECTAMENTE EN EL ARDUINO** si no que el ordenador traduce el lenguaje SCRACTH a código Arduino y el ordenador manda las instrucciones a la placa:

![](https://catedu.gitbooks.io/ensena-pensamiento-computacional-con-arduino/content/img/mbloc-arduino.png)

**EN EL CAPITULO 3 PROGRAMAREMOS DIRECTAMENTE EN EL ARDUINO **
### 2.1.2 VENTAJAS
Pues te permite interactuar el Arduino y el ordenador, por ejemplo podemos hacer que cuando el detector de humedad detecte agua, que salga por pantalla un fondo acuático.

### 2.1.3 DESVENTAJAS

Pues sí, **en primer lugar hay que cargar dentro del Arduino el Firmware** para que Arduino haga caso a mBlock

En segundo lugar, al tener **nuestro ordenador como intermediario**, **se come los recursos** y puede no ir o ir lento nuestro programa. (típico de los intermediarios) además de que necesitamos el ordenador conectado al Arduino, o sea, trabaja como un exclavo del ordenador.

<iframe src="https://giphy.com/embed/3ohhwBo4gMSdzmjJaU" width="480" height="360" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/3ohhwBo4gMSdzmjJaU">via GIPHY</a></p>
