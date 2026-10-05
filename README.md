# Robotica-Movil


## Práctica 1
**Objetivo de la práctica**
<p>
El objetivo de nuestra práctica es crear una máquina de estados para un robot roomba; crear un algoritmo de cobertura.
</p>
<p>
Lo que tiene que hacer la rumba es limpiar la mayor cantidad de superficie posible, de una habitación en la que nuestro dispositivo no conoce el mapa,
entonces se va a ir moviendo por la habitación y se irá chocando con algunos obstáculos, entonces lo que tenemos que hacer es cambiar el destino de este 
hacía otra dirección y que siga recorriendo el mapa, limpiando más superficie.
</p>
<p>
En esta práctica no podemos hacer uso del Bumper, ni tampoco timesleep.
</p>

**Explicación del movimiento**
<p>
Yo he creado un tipo de movimiento, que es totalmente aleatorio para que evite repetir las menores zonas posibles, ya que por ejemplo había probado primero con un movimiento en espiral pero veía que ocupaba pocas zonas durante demasiado tiempo, entonces el movimiento que he optado por hacer es lineal.
</p>
<p>
El robot primero se mueve en una dirección lineal, mientras los 180 grados del laser van comprobando su distancia y en el momento en el que uno de ellos llega a una distancia de 0,3; siendo esta la distancia límite que he optado por poner para que el robot no reciba un choque tan brusco, empieza a retroceder y a girar; el giro cambia dependiendo de si el ángulo es par o impar, entonces esto me ha ayudado a que pueda coger superficie de algunos huecos y que a su vez pueda salir sin tener muchas dificultades.
</p>
<p>
Partes positivas que podría destacar, por ejemplo el robot, utilizando este movimiento, lleva recorrido más o menos 45% y solo lleva 19 minutos del Real Time.
</p>
<p>
El único problema que le puedo ver es que sea a lo mejor el movimiento, demasiado aleatorio, ya que según el ángulo que pille en ese momento hará un tipo de rotación o hará otra, entonces hay veces en las que pueda recorrer más y en otras ocasiones menos.
</p>


<img width="1161" height="944" alt="Screenshot from 2026-10-05 20-23-11" src="https://github.com/user-attachments/assets/151d9941-2cb3-460a-aeb7-7107fdee51a2" />



**Explicación resumida del codigo**
<p>
Antes de empezar, pude solucionar lo del problema con los láseres, poniendo un if para comprobarlo con respecto al tamaño del array.

Lo que he creado es una máquina de estado que solo consta de tres partes:


  -RECTO

  
  -MOVIMIENTO DERECHO


  -MOVIMIENTO IZQUIERDO

Como he comentado anteriormente el robot comienza en estado RECTO, entonces este se mueve únicamente con velocidad v en línea recta, hasta que llegue algún obstáculo y tengan una distancia de 0.3, en ese instante se comprueba el ángulo, y vemos si es par o si es impar con una división, supongamos que el ángulo que ha salido es par, entonces en ese caso el robot tendría una velocidad de retroceso junto con una velocidad de giro, como es par sale MOVIMIENTO IZQUIERDO, por lo que el robot empezará a rotar, como el propio estado indica, a la izquierda, luego esta rotación tiene una duración de un segundo, en el momento en el que la diferencia del tiempo inicial de choque, con el segundo que nos encontramos en ese instante salga que es mayor que el segundo pasamos de nuevo al movimiento lineal y así sucesivamente.
</p>

**Pequeña demostración del movimiento del robot**

[Screencast from 2026-10-05 20-42-09.webm](https://github.com/user-attachments/assets/eabfcfea-0289-4b24-b344-264f5e6c722a)


**Nota sobre el video**: parece que el video va con un poco de delay, pero en el ordenador el movimiento del robot se ve más limpio.



**Problemas que me he encontrado**
<p>
Estoy teniendo problemas con los láseres, entonces cuando comparo datos de los láseres o quiero acceder a uno en concreto de ellos, no funciona el programa, ya que no llega a ese x número de datos del array y no he encontrado ningún tipo de restricción para evitar este fallo, entonces me ha ralentizado mucho a la hora de realizar el código.

Resulta que hay veces que el robot, no se porque motivo, no coge datos de ningún tipo, entonces cuando veo la información que guarda por ejemplo laser data me dice que por ejemplo su rango max y min son ambos cero, que el array de los valores también es cero...
</p>

<img width="450" height="95" alt="Screenshot from 2026-10-02 14-22-40" src="https://github.com/user-attachments/assets/69dc84b8-4e3d-469c-ae0d-41f79b5bd749" />
<p>
Otro problema que me he encontrado, que creo que ya es del servidor, es que el mapa del simulador no coincide con el esquema de la casa, el tamaño de las paredes y de los muebles no coinciden con los originales, falta una pared de la casa... Entonces yo no sé si esto se hace queriendo o simplemente es un fallo o un problema de la app
</p>


