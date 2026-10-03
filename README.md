# Robotica-Movil


## Practica 1
**Objetivo de la practica**
<p>
El objetivo de nuestra practica es crear una maquina de estados para un robot rumba; crear un algoritmo de cobertura.
</p>
<p>
Lo que tiene que hacer la rumba es limpiar la mayor cantidad de superficie posible, de una habitación en la que nuestro dispositivo no conoce el mapa,
entonces se va a ir moviendo por la habitación y se ira chocando con algunos obstaculos, entonces lo que tenemos que hacer es cambiar el destino de este 
hacia otra dirección y que siga recorriendo el mapa, limpiando más superficie.
</p>
<p>
En esta practica no podemos hacer uso del Bumper, ni tampoco podemos ponerle, cuando el robot se choca, como un contador de espera ya que este último sería un error importante.  
</p>

**Explicación del movimiento**
<p>
Yo he creado un tipo de movimiento, que es totalmente aleatorio para que evite repetir las menores zonas posibles, ya que por ejemplo habia probado primero con un movimiento en espiral pero veía que ocupaba pocas zonas durante demasiado tiempo, entonces el movimiento que optado por hacer es lineal.
</p>
<p>
El robot primero se mueve en una dirección lineal, mientras los 180 grados del laser van comprobando su distancia y en el momento en el que uno de ellos llega a una distancia de 0,3; siendo esta la distancia limite que he optado por poner para que el robot no reciba un choque tan brusco, empieza a retroceder y a girar; el giro cambia dependiendo de si es un angulo par o impar en ese momento, entonces esto me ha ayudado a que pueda coger superficie de algunos huecos y que a su vez pueda salir sin tener muchas dificultades.
</p>
<p>
Partes positivas que podria destacar es que por ejemplo el robot, utilizando este movimiento, lleva recorrido mas o menos 40% y solo lleva 14 minutos del Real Time.
</p>


<img width="1119" height="931" alt="Screenshot from 2026-10-03 16-53-32" src="https://github.com/user-attachments/assets/2d42372d-9832-4a58-9d43-0554ae8c870b" />



**Problemas que me estoy encontrando**
<p>
Estoy teniendo problemas con los laseres, entonces cuando comparo datos de los laseres o quiero acceder a uno en concreto de ellos, no funciona el programa, ya que no llega a ese x numero de datos del array y no he encontrado ningun tipo de resticción para evitar este fallo, entonces me ha realentizado mucho a la hora de realizar el código.

Resulta que hay veces que el robot, no se porque motivo, no coge datos de ningun tipo, entonces cuando veo la información que guarda por ejemplo laser data me dice que por ejemplo su rango max y min son ambos cero, que el array de los valores tambien es cero...
</p>

<img width="450" height="95" alt="Screenshot from 2026-10-02 14-22-40" src="https://github.com/user-attachments/assets/69dc84b8-4e3d-469c-ae0d-41f79b5bd749" />
<p>
Otro problema que me he encontrado, que creo que ya es del servidor, es que el mapa del simulador no coincide con el esquema de la casa, el tamaño de las paredes y de los muebles no coinciden con los originales, falta una pared de la casa... Entonces yo no se si esto se hace queriendo o simplemente es un fallo o un problema de la app
</p>


