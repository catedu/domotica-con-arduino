#2.1 Programación mBlock

Es un programa especializado en el manejo de los robots de Makeblock ([ver cursos de mBot en Aularagon](https://catedu.github.io/robotica/)), estos robots están basados en Arduino por lo tanto este programa también puede programarlos

![](http://66.media.tumblr.com/d2949cd218d9678d77cdf61087beb616/tumblr_inline_nj1lt0pIeA1qmn7ka.jpg)

Se puede descargar gratuitamente en http://www.mblock.cc/

Recomendamos en Windows [la versión 3](http://www.mblock.cc/mblock-software/) 


![](/assets/MBLCCK.jpg)

## 2.1.1 NO PROGRAMAMOS DIRECTAMENTE EN EL ARDUINO
mBlock (y los otros S4A, Snap4Arduino... también) **NO PROGRAMA DIRECTAMENTE EN EL ARDUINO**. Lo que hace el ordenador es traducir el lenguaje SCRACTH y en el Arduino hay instalado un Firmware para ir escuchando y ejecutando lo que manda el ordenador.

**EN EL CAPITULO 3 PROGRAMAREMOS DIRECTAMENTE EN EL ARDUINO **
### 2.1.2 VENTAJAS
Pues te permite interactuar el Arduino y el ordenador, por ejemplo podemos hacer que cuando el detector de humedad detecte agua, que salga por pantalla un fondo acuático.

### 2.1.3 DESVENTAJAS

Pues sí, **en primer lugar hay que cargar dentro del Arduino el Firmware exclusivo de mBlock** para que Arduino haga caso a mBlock

En segundo lugar, al tener **nuestro ordenador como intermediario**, **se come los recursos** y puede no ir o ir lento nuestro programa. (típico de los intermediarios)

Y además, necesitamos el ordenador conectado al Arduino, o sea, trabaja como un esclavo del ordenador.

<iframe src="https://giphy.com/embed/3ohhwBo4gMSdzmjJaU" width="480" height="360" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/3ohhwBo4gMSdzmjJaU">via GIPHY</a></p>
