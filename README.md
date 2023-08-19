# Complete-SQL-Bootcamp
<h2> Some of the queries created in Udemy course by Jose Portilla </h2>

SELECT customer_id, staff_id, SUM(amount) FROM payment<br>
GROUP BY staff_id, customer_id<br>
ORDER BY customer_id<br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/adcb168f-2089-4bed-848e-3740fb431988)


SELECT DATE(payment_date), SUM(amount) FROM payment<br>
GROUP BY DATE(payment_date)<br>
ORDER BY SUM(amount) DESC <br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/e723454a-01e7-4227-96c3-ca5117616e64)


SELECT rating, ROUND(AVG(replacement_cost),16) FROM film<br>
GROUP BY rating<br>
ORDER BY AVG(replacement_cost) DESC <br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/93e3f33b-977c-40f0-8331-05549b042edf)

SELECT customer_id, SUM(amount) FROM payment<br>
GROUP BY customer_id<br>
ORDER BY SUM(amount) DESC<br>
LIMIT 5;<br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/8a1f5c5c-9e84-4f16-b592-98d78c179a1c)

SELECT customer_id,staff_id, SUM(amount) FROM payment<br>
WHERE staff_id=2<br>
GROUP BY customer_id, staff_id<br>
HAVING SUM(amount)>100<br>
ORDER BY SUM(AMOUNT) DESC; <br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/51695533-e5a2-4e87-a3e7-9f0f5b25c599)


SELECT customer_id,staff_id, SUM(amount) FROM payment<br>
WHERE staff_id=2<br>
GROUP BY customer_id, staff_id<br>
HAVING SUM(amount)>110<br>
ORDER BY SUM(AMOUNT) DESC; <br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/7590440b-8820-4523-883d-91776ba00aa6)


SELECT first_name,last_name,address_id,MAX(customer_id) FROM customer<br>
WHERE first_name ILIKE 'E%' AND address_id<500<br>
GROUP BY first_name, last_name, address_id<br>
ORDER BY MAX(customer_id) DESC<br>
LIMIT 1<br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/3f4a3c91-8e43-4c09-b61f-7e87cb892acc)


SELECT film.film_id, title, inventory_id, store_id<br>
FROM film<br>
LEFT JOIN inventory ON inventory.film_id = film.film_id<br>
WHERE inventory.film_id IS null <br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/9e34e47b-762e-4aab-91b2-8ece6bddb88f)


SELECT district, address, email FROM customer<br>
INNER JOIN address<br>
ON address.address_id = customer.address_id<br>
WHERE address.district='California'<br>
ORDER BY customer_id<br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/afe7474b-96ab-41ef-8af4-01a51094c736)


SELECT title,first_name, last_name FROM actor<br>
INNER JOIN film_actor ON actor.actor_id = film_actor.actor_id<br>
INNER JOIN film ON film.film_id = film_actor.film_id<br>
WHERE first_name ='Nick' AND last_name = 'Wahlberg'<br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/a87ccff1-7165-4a1c-9864-23ed5ddded5d)


SELECT DISTINCT TO_CHAR(payment_date,'MONTH') AS months FROM payment<br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/751d7e7d-e60f-4d41-9590-5f59d70ef22e)
<br>

SELECT LEFT(first_name,1) || last_name || '@gmail.com' FROM customer<br>
![image](https://github.com/hubost/Complete-SQL-Bootcamp/assets/103451733/4139bc33-4b29-4328-a88d-75bfd17d01d4)


SELECT film_id,title FROM film<br>
WHERE film_id IN<br>
(SELECT inventory.film_id FROM rental<br>
INNER JOIN inventory ON inventory.inventory_id = rental.inventory_id<br>
WHERE return_date BETWEEN '2005-05-29' AND '2005-05-30')<br>
ORDER BY film_id<br>

<h3> Assigment tests tasks </h3>

3.
select * from cd.facilities<br>
WHERE monthlymaintenance >= 80<br>

4.
select facid, name, membercost, monthlymaintenance from cd.facilities<br>
WHERE membercost/monthlymaintenance <= 0.02 AND membercost > 1<br>

5.
SELECT * FROM cd.facilities<br>
WHERE name ILIKE '%Tennis%'<br>

6.
SELECT * FROM cd.facilities<br>
WHERE name ILIKE '%2%'<br>

7.
SELECT memid,surname, firstname, joindate FROM cd.members<br>
WHERE joindate > '2012-09-01'<br>

8.
SELECT DISTINCT surname FROM cd.members <br>
ORDER BY surname LIMIT 10<br>

9.
SELECT surname, firstname, joindate FROM cd.members<br>
ORDER BY joindate DESC<br>

10.
SELECT COUNT(*) FROM cd.facilities<br>
WHERE guestcost >= 10<br>

11.
SELECT (facid), SUM(slots) AS slots FROM cd.bookings <br>
WHERE starttime<='2012-09-01' AND starttime <'2012-10-01'<br>
GROUP BY facid ORDER BY slots<br>

12.
SELECT DISTINCT cd.facilities.facid, SUM(slots) FROM cd.facilities<br>
INNER JOIN cd.bookings<br>
ON cd.facilities.facid = cd.bookings.facid<br>
GROUP BY cd.facilities.facid<br>
HAVING SUM(slots)>1000<br>

13.
SELECT * FROM cd.bookings<br>
INNER JOIN cd.facilities<br>
ON cd.facilities.facid = cd.bookings.facid<br>
WHERE starttime BETWEEN '2012-09-21' AND '2012-09-22' AND name ILIKE '%Tennis Court%'<br>
ORDER BY starttime<br>

14.
 
SELECT cd.facilities.facid,cd.bookings.memid, firstname, surname, starttime FROM cd.members<br>
INNER JOIN cd.bookings<br>
ON cd.members.memid = cd.bookings.memid<br>
INNER JOIN cd.facilities<br>
ON cd.facilities.facid = cd.bookings.facid<br>
GROUP BY cd.bookings.memid, cd.facilities.facid, firstname, surname, starttime<br>
HAVING firstname ILIKE '%David%' AND surname ILIKE '%Farrell'<br>

<h3> Creating and managing databases </h3>
CREATE TABLE students(<br>
student_id SERIAL PRIMARY KEY,<br>
first_name VARCHAR(30) NOT NULL,<br>
last_name VARCHAR(40) NOT NULL,<br>
homeroom_number SMALLINT,<br>
    phone VARCHAR(12) UNIQUE NOT NULL,<br>
    email VARCHAR(20) UNIQUE,<br>
    graduation_year SMALLINT<br>
    )

CREATE TABLE teachers (<br>
teacher_id SERIAL PRIMARY KEY,<br>
first_name VARCHAR(40) NOT NULL,<br>
last_name VARCHAR(40) NOT NULL,<br>
    homeroom_number SMALLINT,<br>
    email VARCHAR(40) UNIQUE NOT NULL,<br>
    phone VARCHAR(12) UNIQUE NOT NULL<br>
)

INSERT INTO students(first_name,last_name,homeroom_number,phone,graduation_year)<br>
VALUES ('Mark','Watney',5,'777-555-1234','2035')<br>

INSERT INTO teachers(first_name,last_name,homeroom_number,email,phone)<br>
VALUES ('Jonas','Salk',5,'jsalk@school.org','777-555-4321')	<br>

UPDATE teachers<br>
SET department = 'Biology'<br>
WHERE teacher_id = 1<br>

SELECT customers.customer_id, orders.order_id, orders.order_date<br>
FROM customers <br>
INNER JOIN orders<br>
ON customers.customer_id = orders.customer_id<br>
ORDER BY customers.customer_id;

