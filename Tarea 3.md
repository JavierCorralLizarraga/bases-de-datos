## Tarea

Usando la BD de Sakila, y en un script de SQL separado, y **en su propio repo de Github**, escribir los queries necesarios y suficientes para dar respuesta a las siguientes preguntas:

1. Cómo obtenemos todos los nombres y correos de nuestros clientes canadienses para una campaña?
~~~ sql
select cl."name", email from customer c 
join customer_list cl on c.customer_id = cl.id 
where country = 'Canada'
~~~

2. Qué cliente ha rentado más de nuestra sección de adultos?

3. Qué películas son las más rentadas en todas nuestras stores?

4. Cuál es nuestro revenue por store?
