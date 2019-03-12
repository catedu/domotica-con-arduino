#3.6 FUEGO
##3.6.1 Objetivos
Tenemos que hacer dos programaciones
* Activar o no la alarma
    * cuando hay una pulsación larga en el pulsador escondido, se activa o se desactiva la alarma
    * si se ha disparado la alarma tiene que apagarla
* Disparo de la alarma
    * Si la alarma está actividad, vigilando y se produce una detección, la alarma tiene que sonar hasta que la desactivamos con una pulsación larga del pulsador.
    
##3.6.2 Maqueta
Fijaremos en la pared el sensor llama que lo vimos anteriormente en 2.7 y el pulsador de activación o no de la alarma.

1. Sensor llama
1. Pulsador analógico
1. Conexión sensor llama a la entrada digital
1. Conexión del pulsador analógico a la entrada analógica

Las alimentaciones de los dos sensores igual que en las páginas anteriores.

![](/assets/maqueta-llama.jpg)

##3.6.3 Esquema eléctrico

* Sensor llama a D9
* Pulsador analógico a A4

##3.6.4 Vídeo

{% youtube %}https://youtu.be/51ehH9JvDz4{% endyoutube%}

##3.6.5 Código

<pre>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;LIBRERIAS</font>
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><b><font color="#d35400">Servo</font></b><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font> 
<font color="#5e6d03">#include</font> <font color="#434f54">&lt;</font><b><font color="#d35400">SoftwareSerial</font></b><font color="#434f54">.</font><font color="#000000">h</font><font color="#434f54">&gt;</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;ENTRADAS SALIDAS DIGITALES &#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#434f54">&#47;&#47; 0 ocupado por el puerto serie ordenador-arduino</font>
<font color="#434f54">&#47;&#47; 1 ocupado por el puerto serie ordenador-arduino</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">PULSADORTIMBRE</font> <font color="#434f54">=</font><font color="#000000">2</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;sensor tactil</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">TIMBRE</font> <font color="#434f54">=</font><font color="#000000">3</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;buzzer activo</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">PUERTA</font> <font color="#434f54">=</font> <font color="#000000">4</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;servo puerta</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">AZUL</font> <font color="#434f54">=</font> <font color="#000000">5</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;led RGB</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">ROJO</font> <font color="#434f54">=</font> <font color="#000000">6</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;led RGB</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">VERDE</font> <font color="#434f54">=</font> <font color="#000000">7</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;led RGB</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">AGUA</font> <font color="#434f54">=</font><font color="#000000">8</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;sensor agua</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">LLAMA</font><font color="#434f54">=</font><font color="#000000">9</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;sensor LLAMA</font>



<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">LED</font> <font color="#434f54">=</font> <font color="#000000">13</font><font color="#000000">;</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47; ENTRADAS ANALÓGICAS &#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>

<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">JOYSTICKAZUL</font> <font color="#434f54">=</font> <font color="#000000">1</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;potenciómetro eje x del joystick</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">JOYSTICKROJO</font> <font color="#434f54">=</font> <font color="#000000">2</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;potenciómetro eje y del joystick</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">JOYSTICKSW</font> &nbsp;&nbsp;<font color="#434f54">=</font> <font color="#000000">3</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;switch del joystick</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">ONOFF</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">=</font> <font color="#000000">4</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;interruptor que apaga o enciende la alarma</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47; OBJETOS&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<b><font color="#d35400">Servo</font></b> <font color="#000000">myservo</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;objeto servo</font>

<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;VARIABLES&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">ABIERTO</font> <font color="#434f54">=</font><font color="#000000">0</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;ángulo abierto puerta</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">CERRADO</font> <font color="#434f54">=</font><font color="#000000">75</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;ángulo cerrado puerta, se ha modificado con respecto a 90 que es cierre total pues tropezaba con la pared</font>
<font color="#00979c">bool</font> <font color="#000000">PUERTAABIERTA</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;guardará si está abierto o no</font>
<font color="#00979c">const</font> <font color="#00979c">int</font> <font color="#000000">QUITAREBOTES</font> <font color="#434f54">=</font> <font color="#000000">1000</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;el tiempo para eliminar rebotes</font>
<font color="#00979c">String</font> <font color="#d35400">command</font> <font color="#434f54">=</font> <font color="#005c5f">&#34;&#34;</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47; guardará la respuesta desde el BT</font>
<font color="#00979c">bool</font> <font color="#000000">ENCENDIDO</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;guardará que debe de dejar la luz encendida</font>
<font color="#00979c">bool</font> <font color="#000000">PONERALARMA</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;guardará que las alarmas están activas</font>
<font color="#00979c">String</font> <font color="#000000">QUESENSOR</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;guarda qué sensor se ha disparado;</font>
<font color="#00979c">bool</font> <font color="#000000">DISPARO</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;guardará que ha ocurrido un disparo de alarma</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;FUNCIONES</font>
<font color="#00979c">void</font> <font color="#000000">CerrarPuerta</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
<font color="#00979c">void</font> <font color="#000000">Alarma</font><font color="#000000">(</font><font color="#00979c">String</font> <font color="#000000">Que</font><font color="#000000">)</font><font color="#000000">;</font>

<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;INICIO &#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#00979c">void</font> <font color="#5e6d03">setup</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>
 &nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">begin</font><font color="#000000">(</font><font color="#000000">9600</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;inicializar el puerto serie del ordenador</font>

 &nbsp;<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;fijar input&#47;output</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">PULSADORTIMBRE</font><font color="#434f54">,</font> <font color="#00979c">INPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">TIMBRE</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">PUERTA</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font> 
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">AZUL</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">ROJO</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">VERDE</font><font color="#434f54">,</font> <font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">LED</font><font color="#434f54">,</font><font color="#00979c">OUTPUT</font><font color="#000000">)</font><font color="#000000">;</font> 
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">AGUA</font><font color="#434f54">,</font><font color="#00979c">INPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">pinMode</font><font color="#000000">(</font><font color="#000000">LLAMA</font><font color="#434f54">,</font><font color="#00979c">INPUT</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;fijar situación inicial</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">TIMBRE</font><font color="#434f54">,</font><font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;<font color="#434f54">&#47;&#47; timbre apagado</font>
 &nbsp;<font color="#000000">myservo</font><font color="#434f54">.</font><font color="#d35400">attach</font><font color="#000000">(</font><font color="#000000">PUERTA</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;servo en el pin correspondiente</font>
 &nbsp;<font color="#000000">myservo</font><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#000000">CERRADO</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;<font color="#434f54">&#47;&#47;puerta cerrada</font>
 &nbsp;<font color="#000000">PUERTAABIERTA</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">AZUL</font><font color="#434f54">,</font><font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;<font color="#434f54">&#47;&#47;luz rgb apagada &nbsp;</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">ROJO</font><font color="#434f54">,</font><font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;<font color="#434f54">&#47;&#47;luz rgb apagada &nbsp;</font>
 &nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">VERDE</font><font color="#434f54">,</font><font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;<font color="#434f54">&#47;&#47;luz verde apagada &nbsp;</font>
 &nbsp;<font color="#000000">PONERALARMA</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">DISPARO</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">QUESENSOR</font> <font color="#434f54">=</font> <font color="#005c5f">&#34;&#34;</font><font color="#000000">;</font>
<font color="#000000">}</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;BUCLE &#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#00979c">void</font> <font color="#5e6d03">loop</font><font color="#000000">(</font><font color="#000000">)</font> <font color="#000000">{</font>

 &nbsp;<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47; timbre &#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">digitalRead</font><font color="#000000">(</font><font color="#000000">PULSADORTIMBRE</font><font color="#000000">)</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;Abriendo puerta .... &#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">PUERTAABIERTA</font><font color="#434f54">=</font><font color="#00979c">true</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">myservo</font><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#000000">ABIERTO</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">3000</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">CerrarPuerta</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47; pulsadorjoystick abrir y cerrar la puerta &nbsp;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
 &nbsp;<font color="#00979c">int</font> <font color="#000000">valor</font><font color="#434f54">=</font><font color="#d35400">analogRead</font><font color="#000000">(</font><font color="#000000">JOYSTICKSW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#434f54">&#47;&#47;Serial.println(valor);</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">valor</font><font color="#434f54">==</font><font color="#000000">0</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">QUITAREBOTES</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">valor</font><font color="#434f54">=</font><font color="#d35400">analogRead</font><font color="#000000">(</font><font color="#000000">JOYSTICKSW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">valor</font><font color="#434f54">==</font><font color="#000000">0</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;HAS PULSADO EL BOTÓN DEL JOYSTICK&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#d35400">command</font><font color="#434f54">=</font><font color="#005c5f">&#34;boton&#34;</font><font color="#000000">;</font> &nbsp;
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">command</font><font color="#434f54">==</font><font color="#005c5f">&#34;boton&#34;</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#434f54">!</font><font color="#000000">PUERTAABIERTA</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;Abriendo puerta .... &#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">PUERTAABIERTA</font><font color="#434f54">=</font><font color="#00979c">true</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">myservo</font><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#000000">ABIERTO</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">}</font><font color="#5e6d03">else</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">CerrarPuerta</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#d35400">command</font> <font color="#434f54">=</font> <font color="#005c5f">&#34;&#34;</font><font color="#000000">;</font>
 &nbsp;&nbsp;<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47; juego luces joystick &#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
 &nbsp;<font color="#00979c">int</font> <font color="#000000">valorAz</font> <font color="#434f54">=</font> <font color="#d35400">analogRead</font><font color="#000000">(</font><font color="#000000">JOYSTICKAZUL</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">valorAz</font> <font color="#434f54">=</font> <font color="#000000">(</font><font color="#000000">valorAz</font><font color="#434f54">-</font><font color="#000000">500</font><font color="#000000">)</font><font color="#434f54">&#47;</font><font color="#000000">2.5</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">valorAz</font><font color="#434f54">&lt;</font><font color="#000000">5</font><font color="#000000">)</font> <font color="#000000">valorAz</font> <font color="#434f54">=</font><font color="#000000">0</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#434f54">!</font><font color="#000000">ENCENDIDO</font><font color="#000000">)</font><font color="#d35400">analogWrite</font><font color="#000000">(</font><font color="#000000">AZUL</font><font color="#434f54">,</font><font color="#000000">valorAz</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#00979c">int</font> <font color="#000000">valorRo</font> <font color="#434f54">=</font> <font color="#d35400">analogRead</font><font color="#000000">(</font><font color="#000000">JOYSTICKROJO</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">valorRo</font> <font color="#434f54">=</font> <font color="#000000">(</font><font color="#000000">valorRo</font><font color="#434f54">-</font><font color="#000000">550</font><font color="#000000">)</font><font color="#434f54">&#47;</font><font color="#000000">2.5</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">valorRo</font><font color="#434f54">&lt;</font><font color="#000000">5</font><font color="#000000">)</font> <font color="#000000">valorRo</font> <font color="#434f54">=</font><font color="#000000">0</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#434f54">!</font><font color="#000000">ENCENDIDO</font><font color="#000000">)</font> <font color="#d35400">analogWrite</font><font color="#000000">(</font><font color="#000000">ROJO</font><font color="#434f54">,</font><font color="#000000">valorRo</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47; agua &#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">digitalRead</font><font color="#000000">(</font><font color="#000000">AGUA</font><font color="#000000">)</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">Alarma</font><font color="#000000">(</font><font color="#005c5f">&#34;AGUA !!!&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">PUERTAABIERTA</font><font color="#000000">)</font> &nbsp;<font color="#000000">CerrarPuerta</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47; ALARMA FUEGO &#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">PONERALARMA</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">VERDE</font><font color="#434f54">,</font><font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;&nbsp;&nbsp;&nbsp;
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#d35400">digitalRead</font><font color="#000000">(</font><font color="#000000">LLAMA</font><font color="#000000">)</font><font color="#434f54">==</font><font color="#000000">0</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">DISPARO</font><font color="#434f54">=</font><font color="#00979c">true</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">QUESENSOR</font> <font color="#434f54">=</font><font color="#005c5f">&#34;FUEGO&#34;</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;&nbsp;&nbsp;<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47; DISPARO &#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">DISPARO</font><font color="#000000">)</font> <font color="#000000">Alarma</font><font color="#000000">(</font><font color="#000000">QUESENSOR</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font><font color="#5e6d03">else</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">VERDE</font><font color="#434f54">,</font><font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47; ONOFF &#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
 &nbsp;<font color="#000000">valor</font><font color="#434f54">=</font><font color="#d35400">analogRead</font><font color="#000000">(</font><font color="#000000">ONOFF</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">valor</font><font color="#434f54">==</font><font color="#000000">0</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">QUITAREBOTES</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">valor</font><font color="#434f54">=</font><font color="#d35400">analogRead</font><font color="#000000">(</font><font color="#000000">ONOFF</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">valor</font><font color="#434f54">==</font><font color="#000000">0</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;HAS PULSADO EL BOTÓN ON&#47;OFF ALARMA &#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">PONERALARMA</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">PONERALARMA</font><font color="#434f54">=</font><font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">DISPARO</font> <font color="#434f54">=</font> <font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">}</font><font color="#5e6d03">else</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">PONERALARMA</font><font color="#434f54">=</font><font color="#00979c">true</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;<font color="#000000">}</font>
<font color="#000000">}</font>






<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;FUNCION CERRAR PUERTA&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#00979c">void</font> <font color="#000000">CerrarPuerta</font><font color="#000000">(</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;<font color="#5e6d03">if</font> <font color="#000000">(</font><font color="#000000">PUERTAABIERTA</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#5e6d03">for</font> <font color="#000000">(</font><font color="#00979c">int</font> <font color="#000000">i</font><font color="#434f54">=</font><font color="#000000">1</font><font color="#000000">;</font><font color="#000000">i</font><font color="#434f54">&lt;=</font><font color="#000000">3</font><font color="#000000">;</font><font color="#000000">i</font><font color="#434f54">++</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;CERRANDO PUERTA !!!&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">LED</font><font color="#434f54">,</font><font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">TIMBRE</font><font color="#434f54">,</font><font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">1000</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">TIMBRE</font><font color="#434f54">,</font><font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">LED</font><font color="#434f54">,</font><font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">1000</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">}</font>
 &nbsp;&nbsp;&nbsp;&nbsp;<font color="#000000">myservo</font><font color="#434f54">.</font><font color="#d35400">write</font><font color="#000000">(</font><font color="#000000">CERRADO</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">PUERTAABIERTA</font><font color="#434f54">=</font><font color="#00979c">false</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#005c5f">&#34;Puerta cerrada&#34;</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;<font color="#000000">}</font>
<font color="#000000">}</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;FUNCION ALARMA &#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#434f54">&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;&#47;</font>
<font color="#00979c">void</font> <font color="#000000">Alarma</font><font color="#000000">(</font><font color="#00979c">String</font> <font color="#000000">Que</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;<font color="#5e6d03">for</font> <font color="#000000">(</font><font color="#00979c">int</font> <font color="#000000">i</font> <font color="#434f54">=</font> <font color="#000000">1</font><font color="#000000">;</font><font color="#000000">i</font><font color="#434f54">&lt;=</font><font color="#000000">10</font><font color="#000000">;</font><font color="#000000">i</font><font color="#434f54">++</font><font color="#000000">)</font><font color="#000000">{</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">TIMBRE</font><font color="#434f54">,</font><font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">LED</font><font color="#434f54">,</font><font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#00979c">String</font> <font color="#000000">mensaje</font><font color="#434f54">=</font><font color="#005c5f">&#34;ALARMA !!!!!!&#34;</font><font color="#434f54">+</font><font color="#000000">Que</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#000000">mensaje</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">100</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">TIMBRE</font><font color="#434f54">,</font><font color="#00979c">HIGH</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">digitalWrite</font><font color="#000000">(</font><font color="#000000">LED</font><font color="#434f54">,</font><font color="#00979c">LOW</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#000000">mensaje</font><font color="#434f54">=</font><font color="#005c5f">&#34;ATENCIÓN !!!!!!&#34;</font><font color="#434f54">+</font><font color="#000000">Que</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<b><font color="#d35400">Serial</font></b><font color="#434f54">.</font><font color="#d35400">println</font><font color="#000000">(</font><font color="#000000">mensaje</font><font color="#000000">)</font><font color="#000000">;</font>
 &nbsp;&nbsp;&nbsp;<font color="#d35400">delay</font><font color="#000000">(</font><font color="#000000">100</font><font color="#000000">)</font><font color="#000000">;</font> &nbsp;
 &nbsp;<font color="#000000">}</font>
<font color="#000000">}</font>

</pre>