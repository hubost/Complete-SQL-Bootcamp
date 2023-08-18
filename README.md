# Complete-SQL-Bootcamp
<h2> Some of the queries used in Udemy course by Jose Portilla </h2>

SELECT customer_id, staff_id, SUM(amount) FROM payment
GROUP BY staff_id, customer_id
ORDER BY customer_id
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/3576b146-b5d5-4f61-8a76-8930d812628c)

SELECT DATE(payment_date), SUM(amount) FROM payment
GROUP BY DATE(payment_date)
ORDER BY SUM(amount) DESC <br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/18b30efc-e126-471a-af95-f196ff509009)

SELECT rating, ROUND(AVG(replacement_cost),16) FROM film
GROUP BY rating
ORDER BY AVG(replacement_cost) DESC <br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/14250a94-9167-4b6f-a80f-af2e3c028b3f)

SELECT customer_id,staff_id, SUM(amount) FROM payment
WHERE staff_id=2
GROUP BY customer_id, staff_id
HAVING SUM(amount)>100
ORDER BY SUM(AMOUNT) DESC; <br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/bd61aa44-9d08-4dc8-af27-56eb1e69d060)

SELECT customer_id,staff_id, SUM(amount) FROM payment
WHERE staff_id=2
GROUP BY customer_id, staff_id
HAVING SUM(amount)>110
ORDER BY SUM(AMOUNT) DESC; <br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/a1027cbb-f769-4574-8c0c-477710a8fb59)

SELECT first_name,last_name,address_id,MAX(customer_id) FROM customer
WHERE first_name ILIKE 'E%' AND address_id<500
GROUP BY first_name, last_name, address_id
ORDER BY MAX(customer_id) DESC
LIMIT 1
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/f0af26b0-f0a8-476c-8e31-f03653115455)

SELECT film.film_id, title, inventory_id, store_id
FROM film
LEFT JOIN inventory ON inventory.film_id = film.film_id
WHERE inventory.film_id IS null <br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/f2627ca3-32fd-4f8a-ab60-c2bb03fc1d40)


SELECT district, address, email FROM customer
INNER JOIN address
ON address.address_id = customer.address_id
WHERE address.district='California'
ORDER BY customer_id<br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/be76f91e-8313-4f9c-a44e-bcd3c08ff010)


SELECT title,first_name, last_name FROM actor
INNER JOIN film_actor ON actor.actor_id = film_actor.actor_id
INNER JOIN film ON film.film_id = film_actor.film_id
WHERE first_name ='Nick' AND last_name = 'Wahlberg'<br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/f65b41d2-cdde-4d0b-b97b-d7d2885abb9f)

SELECT DISTINCT TO_CHAR(payment_date,'MONTH') AS months FROM payment<br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/9519e17e-8068-46e3-9b22-91e519e3781f)<br>

SELECT LEFT(first_name,1) || last_name || '@gmail.com' FROM customer<br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/14fe805a-e14a-483e-ae08-fd4b5b3d08a3)

SELECT film_id,title FROM film
WHERE film_id IN
(SELECT inventory.film_id FROM rental
INNER JOIN inventory ON inventory.inventory_id = rental.inventory_id
WHERE return_date BETWEEN '2005-05-29' AND '2005-05-30')
ORDER BY film_id

<h3> Assigment tests tasks </h3>

3.
select * from cd.facilities
WHERE monthlymaintenance >= 80

4.
select facid, name, membercost, monthlymaintenance from cd.facilities
WHERE membercost/monthlymaintenance <= 0.02 AND membercost > 1

5.
SELECT * FROM cd.facilities
WHERE name ILIKE '%Tennis%'

6.
SELECT * FROM cd.facilities
WHERE name ILIKE '%2%'

7.
SELECT memid,surname, firstname, joindate FROM cd.members
WHERE joindate > '2012-09-01'

8.
SELECT DISTINCT surname FROM cd.members 
ORDER BY surname LIMIT 10

9.
SELECT surname, firstname, joindate FROM cd.members
ORDER BY joindate DESC

10.
SELECT COUNT(*) FROM cd.facilities
WHERE guestcost >= 10

11.
SELECT (facid), SUM(slots) AS slots FROM cd.bookings 
WHERE starttime<='2012-09-01' AND starttime <'2012-10-01'
GROUP BY facid ORDER BY slots

12.
SELECT DISTINCT cd.facilities.facid, SUM(slots) FROM cd.facilities
INNER JOIN cd.bookings
ON cd.facilities.facid = cd.bookings.facid
GROUP BY cd.facilities.facid
HAVING SUM(slots)>1000

13.
SELECT * FROM cd.bookings
INNER JOIN cd.facilities
ON cd.facilities.facid = cd.bookings.facid
WHERE starttime BETWEEN '2012-09-21' AND '2012-09-22' AND name ILIKE '%Tennis Court%'
ORDER BY starttime

14.
 
SELECT cd.facilities.facid,cd.bookings.memid, firstname, surname, starttime FROM cd.members
INNER JOIN cd.bookings
ON cd.members.memid = cd.bookings.memid
INNER JOIN cd.facilities
ON cd.facilities.facid = cd.bookings.facid
GROUP BY cd.bookings.memid, cd.facilities.facid, firstname, surname, starttime
HAVING firstname ILIKE '%David%' AND surname ILIKE '%Farrell'

<h3> Creating and managing databases </h3>
CREATE TABLE students(
student_id SERIAL PRIMARY KEY,
first_name VARCHAR(30) NOT NULL,
last_name VARCHAR(40) NOT NULL,
homeroom_number SMALLINT,
    phone VARCHAR(12) UNIQUE NOT NULL,
    email VARCHAR(20) UNIQUE,
    graduation_year SMALLINT
    )

CREATE TABLE teachers (
teacher_id SERIAL PRIMARY KEY,
first_name VARCHAR(40) NOT NULL,
last_name VARCHAR(40) NOT NULL,
    homeroom_number SMALLINT,
    email VARCHAR(40) UNIQUE NOT NULL,
    phone VARCHAR(12) UNIQUE NOT NULL
)

INSERT INTO students(first_name,last_name,homeroom_number,phone,graduation_year)
VALUES ('Mark','Watney',5,'777-555-1234','2035')

INSERT INTO teachers(first_name,last_name,homeroom_number,email,phone)
VALUES ('Jonas','Salk',5,'jsalk@school.org','777-555-4321')	

UPDATE teachers
SET department = 'Biology'
WHERE teacher_id = 1

SELECT customers.customer_id, orders.order_id, orders.order_date
FROM customers 
INNER JOIN orders
ON customers.customer_id = orders.customer_id
ORDER BY customers.customer_id;

