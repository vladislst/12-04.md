# Домашнее задание к занятию "`SQL. Часть 2`" - `Степанов Владислав`

### Задание 1

select concat(st.first_name,' ',st.last_name) as full_name, city, count(c.customer_id) as count_customer
from customer c
join store s on c.store_id = s.store_id
join address a on s.address_id = a.address_id 
join staff st on s.manager_staff_id = st.staff_id
join city ci on a.city_id = ci.city_id
group by c.store_id
having count_cus > 300

### Задание 2  

select count(film.film_id)
from film
where length > (select avg(film.length) from film)

### Задание 3

select month(p.payment_date) 'mount' ,sum(p.amount) 'sum_payment_in_mount', t2.cnt 'count_rent'
from payment p
join (
select count(r.rental_id) cnt , month(r.rental_date) rental_m
from rental r
group by month(r.rental_date)
) t2 on month(p.payment_date) = t2.rental_m
group by month(p.payment_date),t2.rental_m
order by sum(p.amount) desc
limit 1
