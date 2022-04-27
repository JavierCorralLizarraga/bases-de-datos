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

~~~

14. Cuántos productos tenemos de cada categoría?
~~~ sql 

~~~

15. Cómo podemos generar el reporte de reorder?
~~~ sql 

~~~

16. A donde va nuestro envío más voluminoso?
~~~ sql 

~~~

17. Cómo creamos una columna en customers que nos diga si un cliente es bueno, regular, o malo?
~~~ sql 

~~~

18. Qué colaboradores chambearon durante las fiestas de navidad?
~~~ sql 

~~~

19. Qué productos mandamos en navidad?
~~~ sql 

~~~

20. Qué país recibe el mayor volumen de producto?
~~~ sql 

~~~
