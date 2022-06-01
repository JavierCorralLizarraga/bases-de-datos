### Tarea 5

Como parte de la modernización de nuestras video rental stores, vamos a automatizar la recepción y entrega de discos con robots.

[![Brazo robótico manejando storage](http://img.youtube.com/vi/CVN93H6EuAU/0.jpg)](http://www.youtube.com/watch?v=CVN93H6EuAU "Brazo robótico manejando storage")

Parte de la infraestructura es diseñar contenedores cilíndricos giratorios para facilitar la colocación y extracción de discos por brazos automatizados. Cada cajita de Blu-Ray mide 20cm x 13.5cm x 1.5cm, y para que el brazo pueda manipular adecuadamente cada cajita, debe estar contenida dentro de un arnés que cambia las medidas a 30cm x 21cm x 8cm para un espacio total de 5040 centímetros cúbicos y un peso de 500 gr por película.

Se nos ha encargado formular la medida de dichos cilindros de manera tal que quepan todas las copias de los Blu-Rays de cada uno de nuestros stores. Las medidas deben ser estándar, es decir, la misma para todas nuestras stores, y en cada store pueden ser instalados más de 1 de estos cilindros. Cada cilindro aguanta un peso máximo de 50kg como máximo. El volúmen de un cilindro se calcula de [ésta forma.](volume of a cylinder)

Esto no se resuelve con 1 solo query. El problema se debe partir en varios cachos y deben resolver cada uno con SQL.

La información que no esté dada por el enunciado del problema o el contenido de la BD, podrá ser establecida como supuestos o assumptions, pero deben ser razonables para el problem domain que estamos tratando.

## solucion 
formula de volumen de los cilindros: volumen = $\pi$ * $radio ^ {2}$ * altura

medida caja BR: 20cm x 13.5cm x 1.5cm

volumen caja BR: 405 cm3

medida arnes: 30cm x 21cm x 8cm

volumen arnes: 5040 cm3

peso arnes 500 g

peso maximo por cilindro: 50 kg = 50,000 g

### queremos la medida de un cilindro:
sabemos entonces que si el cilindro aguanta 50,000 g y cada arnes pesa 500 g, cada cilindro puede contener 100 arneses

arneses por cilindro: 100

asumiendo arbitrariamente que puedan caber 4 arneses por nivel tendriamos 25 niveles. 
Para determinar el radio del cilindro veremos la diagonal de un arnes por pitagoras

diagonal de un arnes : ((30^2)+(21^2))^(1/2) = 36.6 = radio del cilindro

como hay 4 arneses por nivel sabemos que la diagonal de un arnes es igual al radio del cilindro

ahora para sacar la altura del cilindro podemos multiplicar la altura de un arnes por los 25 niveles

altura del cilindro: 25* 8 = 200 

**todo esto es asumiendo que no hay gap entre los arneses**

entonces las medidas del cilindro son: radio = 36.6 cm y altura de 200 cm

lo cual nos da un volumen de: pi*36.6^2*200 = 841670.37 cm3
