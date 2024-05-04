# Day 4
## DML Commands

### Exercise 16
~~~sql
1.
CREATE TABLE Database(
    Name TEXT,
    Version FLOAT, 
    Download_count INTEGER
    );

~~~

### Exercise 17
~~~sql
1.
ALTER table movies
ADD Aspect_ratio float ;

2.
ALTER Table Movies
ADD Language TEXT default English;
~~~

### Exercise 18
~~~sql
1.
DROP TABLE IF EXISTS Movies;

2.
DROP TABLE IF EXISTS Boxoffice;
~~~

## SSMS
~~~sql
CREATE TABLE salesman (
    salesman_id INT PRIMARY KEY,
    name VARCHAR(255),
    city VARCHAR(255),
    commission DECIMAL(4, 2)
);

select * from salesman

INSERT INTO salesman (salesman_id, name, city, commission) VALUES
(5001, 'James Hoog', 'New York', 0.15),
(5002, 'Nail Knite', 'Paris', 0.13),
(5005, 'Pit Alex', 'London', 0.11),
(5006, 'Mc Lyon', 'Paris', 0.14),
(5003, 'Lauson Hen', NULL, 0.12),
(5007, 'Paul Adam', 'Rome', 0.13);

-- Task 1
-- Find the average commision of a saleman from Paris
select avg(commission) 
from salesman
where city='paris';
 
-- Task 2
-- Find out if there are cities with only one salesman and list them | No nulls
SELECT city
FROM salesman where city is not null
GROUP BY city
HAVING COUNT(*) = 1;
 
-- Task 3
-- Determine the maximum commission in each city, and list the salesmen who earn this commission
-- Clue: Join
select city 
from salesman 
group by city
having count(city)<2 AND city is not null


CREATE TABLE orders (
    ord_no INT PRIMARY KEY,
    purch_amt DECIMAL(10, 2),
    ord_date DATE,
    customer_id INT,
    salesman_id INT
);
 
 
INSERT INTO orders (ord_no, purch_amt, ord_date, customer_id, salesman_id) VALUES
(70001, 150.5, '2012-10-05', 3005, 5002),
(70009, 270.65, '2012-09-10', 3001, 5005),
(70002, 65.26, '2012-10-05', 3002, 5001),
(70004, 110.5, '2012-08-17', 3009, 5003),
(70007, 948.5, '2012-09-10', 3005, 5002),
(70005, 2400.6, '2012-07-27', 3007, 5001),
(70008, 5760, '2012-09-10', 3002, 5001),
(70010, 1983.43, '2012-10-10', 3004, 5006),
(70003, 2480.4, '2012-10-10', 3009, 5003),
(70012, 250.45, '2012-06-27', 3008, 5002),
(70011, 75.29, '2012-08-17', 3003, 5007),  
(70013, 3045.6, '2012-04-25', 3002, 5001);

select * from orders;

-- Task 4 - Sub-Query
-- Write a query to display all the orders from the orders table issued by the salesman 'Paul Adam'.
select * 
from orders
where salesman_id = 
(select salesman_id
from salesman
where name = 'Paul Adam');


-- Task 5 
-- Write a query to display all the orders which values are greater than the average order value for 10th October 2012
--5.1: Find the average order value for 10th October 2012

select * from orders;


select * 
from orders 
where purch_amt > (select AVG(purch_amt)
from orders
where ord_date = '2012-10-10');


-- Task 6
-- Write a query to find all orders with order amounts which are above-average amounts for their customers.
Select * 
from orders o
where purch_amt > (Select  AVG(purch_amt) 
					from orders i
					where o.customer_id = i.customer_id
					);