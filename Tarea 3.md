## Tarea

Usando la BD de Sakila, y en un script de SQL separado, y **en su propio repo de Github**, escribir los queries necesarios y suficientes para dar respuesta a las siguientes preguntas:

1. Cómo obtenemos todos los nombres y correos de nuestros clientes canadienses para una campaña?
~~~ sql
select cl."name", email from customer c 
join customer_list cl on c.customer_id = cl.id 
where country = 'Canada'
~~~

2. Qué cliente ha rentado más de nuestra sección de adultos? hay muchos, sino habria hecho order by cant desc limit 1
~~~ sql
select * from 
(
select nombre, count(rental_id) as cant from
(
select first_name || ' ' || last_name as nombre, film_id, rental_id, rating from customer c 
join store s using (store_id) 
join inventory i  using (store_id)
join rental r using (inventory_id)
join film f using (film_id)
where rating = 'NC-17'
) as tabla1
group by nombre
) as tabla2
where cant =
(
select max(cant) from 
(
select nombre, count(rental_id) as cant from
(
select first_name || ' ' || last_name as nombre, film_id, rental_id, rating from customer c 
join store s using (store_id) 
join inventory i  using (store_id)
join rental r using (inventory_id)
join film f using (film_id)
where rating = 'NC-17'
) as tabla4
group by nombre
) as cant2
)
~~~

3. Qué películas son las más rentadas en todas nuestras stores?
~~~ sql 

~~~

4. Cuál es nuestro revenue por store?
~~~ sql

~~~
