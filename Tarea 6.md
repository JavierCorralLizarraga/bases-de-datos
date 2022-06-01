## Tarea

Una de las métricas para saber si un cliente es bueno, aparte de la suma y el promedio de sus pagos, es si tenemos una progresión consistentemente creciente en los montos.

Debemos calcular para cada cliente su promedio mensual de _deltas_ en los pagos de sus órdenes en la tabla `order_details` en la BD de Northwind, es decir, la diferencia entre el monto total de una orden en tiempo _t_ y el anterior en _t-1_, para tener la foto completa sobre el customer lifetime value de cada miembro de nuestra cartera.

asumimos que la mejor metrica es la de quantity por tanto sobre esa hacemos el delta

~~~ sql 
with t2 as(
with t as(
select contact_name as nombre, quantity from order_details od 
join orders o using (order_id)
join customers c using (customer_id)
)
select nombre, quantity - lag(quantity) over (partition by nombre) as delta
from t
)
select nombre, avg(delta) as promedio_delta
from t2 
group by nombre 
~~~
