# 12-04-sql  

Задание 1  
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:   
фамилия и имя сотрудника из этого магазина;  
город нахождения магазина;  
количество пользователей, закреплённых в этом магазине  

SELECT concat(st.last_name, ' ', st.first_name) AS "seller", count(c.customer_id) AS "num of buyers", ci.city  
FROM store s   
JOIN customer c ON c.store_id = s.store_id    
JOIN address a ON a.address_id = s.address_id   
JOIN city ci ON ci.city_id = a.city_id   
JOIN staff st ON st.store_id = s.store_id   
GROUP BY ci.city_id, st.staff_id   
HAVING count(c.customer_id) > 300;  

Задание 2  
Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.  

SELECT COUNT(f.title)  
from film f   
WHERE f.`length` > (SELECT AVG(`length`) from film);  

Задание 3  
Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.  

SELECT DATE_FORMAT(payment_date, "%m-%Y"), COUNT(payment_id), SUM(amount)  
FROM payment WHERE DATE_FORMAT(payment_date, "%m") 
GROUP BY DATE_FORMAT(payment_date, "%m-%Y")   
ORDER BY SUM(amount) DESC   
LIMIT 1;   
