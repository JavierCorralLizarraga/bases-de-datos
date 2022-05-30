### Tarea 1

Una aplicación frecuente de Ciencia de Datos aplicada a la industria del microlending es el de calificaciones crediticias (credit scoring). Puede interpretarse de muchas formas: propensión a pago, probabilidad de default, etc. La intuición nos dice que las variables más importantes son el saldo o monto del crédito, y la puntualidad del pago; sin embargo, otra variable que frecuentemente escapa a los analistas es el tiempo entre cada pago. La puntualidad es una pésima variable para anticipar default o inferir capacidad de pago de micropréstamos, por su misma naturaleza. Si deseamos examinar la viabilidad de un producto de crédito para nuestras videorental stores:

1. Cuál es el promedio, en formato human-readable, de tiempo entre cada pago por cliente de la BD Sakila?
~~~ sql 
with t2 as(
with t as (
select first_name || ' ' || last_name as nombre, c.customer_id, payment_id, payment_date from payment p 
join customer c using(customer_id)
join rental r using (rental_id)
) 
select nombre, customer_id, payment_date - lag(payment_date) 
over (
order by payment_date) as duracion 
from t
)
select nombre, avg(duracion) as promedio_duracion 
from t2
group by nombre
order by promedio_duracion
~~~
2. Sigue una distribución normal?
~~~ sql 
create view histo as(
with t2 as(
with t as (
select first_name || ' ' || last_name as nombre, c.customer_id, payment_id, payment_date from payment p 
join customer c using(customer_id)
join rental r using (rental_id)
) 
select nombre, customer_id, payment_date - lag(payment_date) 
over (
order by payment_date) as duracion 
from t
)
select nombre, cast(extract(epoch from avg(duracion)) as integer) as promedio_duracion
from t2
group by nombre
order by promedio_duracion
)

select * from histogram('histo', 'promedio_duracion')
~~~
![image](https://user-images.githubusercontent.com/46376887/171067399-4dcf0504-b1c2-4552-8787-488d2997c9c5.png)

vemos que no es normal

3. Qué tanto difiere ese promedio del tiempo entre rentas por cliente?
~~~ sql 
with t3 as(
with t2 as(
with t as (
select first_name || ' ' || last_name as nombre, c.customer_id, payment_id, payment_date from payment p 
join customer c using(customer_id)
join rental r using (rental_id)
) 
select nombre, customer_id, payment_date - lag(payment_date) 
over (
order by payment_date) as duracion 
from t
)
select nombre, cast(extract(epoch from avg(duracion)) as integer) as promedio_duracion
from t2
group by nombre
order by promedio_duracion
)
select avg(promedio_duracion) as media, variance(promedio_duracion) as varianza from t3
~~~
![image](https://user-images.githubusercontent.com/46376887/171067806-068dee8e-ea9a-4a6b-a431-360be0368ca7.png)

