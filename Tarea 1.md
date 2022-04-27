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

~~~

16. A donde va nuestro envío más voluminoso?

asumiendo que voluminoso se refiere a cantidad
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
~~~ sql 

~~~
18. Qué colaboradores chambearon durante las fiestas de navidad?
~~~ sql 

~~~

19. Qué productos mandamos en navidad?
tomaremos navidad como solo el 25 de diciembre
~~~ sql 

~~~

20. Qué país recibe el mayor volumen de producto?
~~~ sql 

~~~
