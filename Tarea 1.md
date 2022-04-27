## Ejercicios - Tarea 1

1. Qué contactos de proveedores tienen la posición de sales representative?
~~~ sql
select * from suppliers s where contact_title = 'Sales Representative' 
~~~

2. Qué contactos de proveedores no son marketing managers?
~~~ sql 
select * from suppliers s where contact_title != 'Marketing Manager'  
~~~

3. Cuales órdenes no vienen de clientes en Estados Unidos?
~~~ sql 
select * from customers c join orders o on c.customer_id = o.customer_id where c.country != 'USA' 
~~~

4. Qué productos de los que transportamos son quesos?
~~~ sql 
select * from products p where category_id = 4
~~~

5. Qué ordenes van a Bélgica o Francia?
~~~ sql 
select * from orders o where ship_country in ('France', 'Belgium')
~~~

6. Qué órdenes van a LATAM?
~~~ sql 
select * from orders o where ship_country in ('Argentina', 'Mexico', 'Brazil', 'Venezuela')
~~~

7. Qué órdenes no van a LATAM?
~~~ sql 
select * from orders o where ship_country not in ('Argentina', 'Mexico', 'Brazil', 'Venezuela')
~~~

8. Necesitamos los nombres completos de los empleados, nombres y apellidos unidos en un mismo registro
~~~ sql 
select concat(first_name,' ', last_name) as nombre_completo from employees e
~~~

9. Cuánta lana tenemos en inventario?
~~~ sql 
select unit_price * units_in_stock as lana from products p
~~~

10. Cuantos clientes tenemos de cada país?
~~~ sql 
select country, count(*) from customers c group by country
~~~

11. Obtener un reporte de edades de los empleados para checar su elegibilidad para seguro de gastos médicos menores.
~~~ sql 
select employee_id, (extract(year from current_date) - extract(year from birth_date)) as years from employees e
~~~

12. Cuál es la orden más reciente por cliente?
~~~ sql 
select distinct(c2.contact_name), order_id from (
select contact_name, max(order_date) as maximo
from orders o 
join customers c on c.customer_id = o.customer_id 
group by contact_name
) as fechas
join customers c2 on fechas.contact_name = c2.contact_name 
join orders o on o.customer_id = c2.customer_id
where order_date = maximo
~~~

13. De nuestros clientes, qué función desempeñan y cuántos son?
~~~ sql 
select contact_title, count(*) as cantidad from customers c group by contact_title 
~~~

14. Cuántos productos tenemos de cada categoría?
~~~ sql 
select category_id, count(*) as cantidad from products p group by category_id 
~~~

15. Cómo podemos generar el reporte de reorder?
~~~ sql 
select product_id, product_name, (reorder_level - units_in_stock - units_on_order) as cantidad
from products p where (units_in_stock - units_on_order) <= reorder_level and discontinued = 0
~~~

16. A donde va nuestro envío más voluminoso?

asumiendo que entre mas voluminoso el envio, mayor sera el freight
~~~ sql 
select ship_address from orders o where freight = (select max(freight) from orders)
~~~

17. Cómo creamos una columna en customers que nos diga si un cliente es bueno, regular, o malo?

sacamos el average de ordenes por cliente
~~~ sql 
select avg(count) from (select count(*) from orders o group by customer_id) as a
~~~
el cual da ~9.3,
si tiene entre 6 y 12 sera regular, si tiene mas de 12 sera bueno y si tiene menos de 6 sera malo

18. Qué colaboradores chambearon durante las fiestas de navidad?
~~~ sql 
select employee_id from orders o where extract(day from shipped_date) = 25 and extract(month from shipped_date)=12
~~~

19. Qué productos mandamos en navidad?
tomaremos navidad como solo el 25 de diciembre
~~~ sql 
select product_id from orders o  
join order_details od ON o.order_id = od.order_id 
where extract(day from shipped_date) = 25 and extract(month from shipped_date)=12
~~~

20. Qué país recibe el mayor volumen de producto?
~~~ sql 
select ship_country 
from 
(select ship_country, count(*) as cantidad from orders o group by ship_country) as tabla
where cantidad = 
(select max(cantidad) from (select ship_country, count(*) as cantidad from orders o group by ship_country) as cantidades)
~~~
