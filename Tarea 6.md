## Tarea

Una de las métricas para saber si un cliente es bueno, aparte de la suma y el promedio de sus pagos, es si tenemos una progresión consistentemente creciente en los montos.

Debemos calcular para cada cliente su promedio mensual de _deltas_ en los pagos de sus órdenes en la tabla `order_details` en la BD de Northwind, es decir, la diferencia entre el monto total de una orden en tiempo _t_ y el anterior en _t-1_, para tener la foto completa sobre el customer lifetime value de cada miembro de nuestra cartera.
