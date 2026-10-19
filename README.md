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


## Práctica 2

**Objetivo de la práctica**
<p>
En esta práctica tenemos un coche de fórmula 1, el cual tiene que recorrer un circuito, siguiendo una línea.

En esta práctica aprenderemos a utilizar la cámara, también usaremos ejecuciones basadas en eventos y haremos uso de los cálculos de error (P, PD, PID).
</p>

**Explicación de la detección del color**
<p>
Para que el coche se pueda mover por el circuito, este tiene que seguir una línea roja que hay en el centro de la pista, entonces lo primero que tenemos que hacer es que el coche solamente detecte la línea a través de su color para poder seguirla y también para poder medir la distancia que tiene de ella.

Entonces he creado un filtro de color, que se basa en las dos tonalidades de rojo, ya que en la gama de colores el rojo es el primero y el último entonces he cogido los dos para evitar algun problema, creando una mascara en la que se aplican las dos tonalidades sobre la imagen.

Y tras aplicar la máscara en la imagen el resultado que obtenemos del mapa es el de la imagen superior: 


<img width="1082" height="929" alt="Screenshot from 2026-10-13 17-56-22" src="https://github.com/user-attachments/assets/344a92e7-2414-4c27-a2fb-9e2edd988238" />
</p>

**Explicación del movimiento**
<p>
Entonces ya una vez que tenemos la línea detectada, podemos comenzar con el movimiento del coche

Primero he encontrado el centro de la imagen haciendo uso de una función que pertenece a una de las variables para poder saber el ancho de la imagen y he calculado la mitad, luego tengo otra variable que ubica el centro de los pixeles y tras hacer una operación sacó la distancia que tiene el coche con el centro.

Una vez que tenemos la distancia he puesto un rango de distancia que puede tener el coche con respecto la línea, siendo este rango 10, entonces en el momento en el que el coche supera esa distancia tiene que doblar a la izquierda o a la derecha dependiendo del caso, izquierda si el valor del rango es menor que -10, es negativo porque el eje central es la línea roja entonces los puntos que están en un lado y otro son los mismos pero con el signo cambiado, por lo que si el coche también si supera el rango de 10 tendría que hacer el movimiento opuesto.
</p>

**Explicación resumida del codigo**
<p>
Primero he creado una máquina de estados para en el caso en el que el coche no encuentre la línea de primeras gire, entonces el coche comienza con el estado VEO_LA_LINEA, pero si no ve nada de la linea se cambia al estado NO_VEO_LA_LINEA, este comienza a girar hasta que llega a un mínimo, para que se considere que el coche ve bien la línea, se cambia el estado y este continua con el camino.

Para explicar el movimiento del coche, teniendo en cuenta lo anterior, he creado un if para cada uno de los casos, uno para el movimiento lineal otro para el giro izquierdo y otro para el giro derecho.

Para obtener la velocidad de los distintos movimientos he creado una velocidad basándose en la P del PID, la ecuación es:

Vf = K*dist + vel

La k es una constante, dist es la distancia del coche respecto a la línea y luego a esto se le suma la velocidad 

Para el movimiento lineal le añado un valor inicial de velocidad de 10, tiene una velocidad de giro de cero ya que sigue un movimiento lineal. Luego para los movimientos de giro, les he puesto como valor inicial para la velocidad de giro 0, para que gire lo justo y necesario que necesite según la constante y la distancia y a estos movimientos de giro le he añadido una velocidad de giro de 8, he optado porque sea menor que la anterior, por el peligro que a pueda salir de las curvas por tener demasiada velocidad lineal.
</p>

**Video de ejemplo del movimiento del coche**



[Screencast from 2026-10-13 22-01-35.webm](https://github.com/user-attachments/assets/8ac88063-ab51-4625-897c-402b3765542d)





[Screencast from 2026-10-15 12-29-57.webm](https://github.com/user-attachments/assets/fd00dd31-f23a-4164-a93f-0e03fd25c604)




**Nota del video**: En estos videos me pasa como en el anterior, que el video va con demasiado delay pero en verdad, en el simulador, no se ve de esta forma, el movimiento del coche es mucho más fluido en el simulador.



**Ejemplo de como se vería en realidad**





[20261015_123735_1.webm](https://github.com/user-attachments/assets/ee6440f1-ba38-40e2-bce9-373c0726f1bd)





Este es un ejemplo de como se ve en simulador el movimiento en las curvas



**Problemas que me he encontrado a la hora de hacer la practica**
<p>
El principal problema que me he podido encontrar es a la hora de encontrar la K, ya que este es un valor constante el cual se obtiene a base de hacer muchas pruebas, entonces se tarda mucho en encontrar un valor que pueda ser idóneo para el movimiento.
</p>


## Práctica 3
**Objetivo de la práctica**
<p>
El objetivo de este ejercicio es implementar la lógica del algoritmo de navegación VFF
  
Los objetos, que son los diferentes obstaculos, van a generar una fuerza repulsiva contra el robot y el destino, todo lo contrario, creara una fuerza de atracción que tirara del coche hasta este punto.

Los distintos objetivos a tratar son:

  - Que el coche vaya lo más rapido posible

  - Que el coche escoja la ruta que es más segura

  - Evitar los obstaculos que están en movimiento

  - Y que tenga robustez en aquellos casos en los que el robot este indeciso de por donde poder tirar, es decir, en los casos en los que la suma de los vectores de 0  
</p>
