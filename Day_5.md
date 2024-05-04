# Day 5
## SSMS Tasks

### Task 7 - Write a query to find all orders attributed to a salesman in Paris
~~~sql
select * 
from orders
where salesman_id in(select salesman_id
	from salesman
	where city = 'Paris');
~~~

### Create Table Orders

~~~sql
CREATE TABLE customer (
    customer_id INT PRIMARY KEY,
    cust_name VARCHAR(255),
    city VARCHAR(255),
    grade INT NULL,
    salesman_id INT
);
INSERT INTO customer (customer_id, cust_name, city, grade, salesman_id) VALUES
(3002, 'Nick Rimando', 'New York', 100, 5001),
(3005, 'Graham Zusi', 'California', 200, 5002),
(3001, 'Brad Guzan', 'London', NULL, 5005),
(3004, 'Fabian Johns', 'Paris', 300, 5006),
(3007, 'Brad Davis', 'New York', 200, 5001),
(3009, 'Geoff Camero', 'Berlin', 100, 5003),
(3008, 'Julian Green', 'London', 300, 5002),
(3003, 'Jozy Altidor', 'Moscow', 200, 5007);
~~~


### Task 8: Write a query to find the name and id of all salesmen who had more than one customer
~~~sql
--Subquery - 1
select salesman_id, count(customer_id) as number
from customer
group by salesman_id
having Count(customer_id)>1; --5001 and 5002

--Subquery 2
select salesman_id, name
from salesman
where salesman_id IN (5001, 5002);


select salesman_id, name
from salesman
where salesman_id IN (select salesman_id
	from customer
	group by salesman_id
	having Count(customer_id)>1);
~~~

### Task 9: Write a query to display only those customers whose grade are, in fact, higher than every customer in New York. All or Any
~~~sql
select *
from customer
where grade > all(
	select grade
	from customer
	where city = 'New York');
~~~

### Task 10: Write a query to find all orders with an amount smaller than any amount for a customer in London.
~~~sql
--Sub Query 1:find ppl in London
select * 
from customer
where city = 'London';--3001 and 3008

--Sub Query 2:  find the min value order
select * 
from orders
where customer_id in(3001, 3008); --250.45 and 270.65

--Sub Query 3: Find the order below that min
select * 
from orders 
where purch_amt < 250.45;

--Final Query
select *
from orders
where purch_amt < ANY(select purch_amt
	                  from orders
	                  where customer_id in(select customer_id
						                   from customer
						                   where city = 'London'));
~~~


## ERD Diagrams Table

### Create Tables referring the ERDs

~~~sql
--ERD Diagrams Tables 

CREATE TABLE [Student](
	[StudentID] Varchar(255),
	[StudentName] Varchar(255),
	PRIMARY KEY([StudentID])
);

INSERT INTO Student (StudentID, StudentName)
VALUES ('S001', 'Alice'),
       ('S002', 'Bob'),
       ('S003', 'Charlie');

CREATE TABLE [Professor](
	[ProfessorID] Varchar(255),
	[ProfessorName] Varchar(255),
	[Department] Varchar(255),
	PRIMARY KEY ([ProfessorID])
);

INSERT INTO Professor (ProfessorID, ProfessorName, Department)
VALUES ('P001', 'Dr. Brown', 'Mathematics'),
       ('P002', 'Dr. Smith', 'Physics');
 

CREATE TABLE [Course](
	[CourseID] Varchar(255),
	[CourseName] Varchar(255),
	[ProfessorID] Varchar(255),
	PRIMARY KEY ([CourseID]),
	Foreign Key ([ProfessorID]) References Professor([ProfessorID])
);

INSERT INTO Course (CourseID, CourseName, ProfessorID)
VALUES ('C001', 'Math 101', 'P001'),
       ('C002', 'Physics 101', 'P002');

CREATE TABLE [Enrollment](
	[EnrollmentID] Varchar(255),
	[CourseID] Varchar(255),
	[StudentID] Varchar(255),
	PRIMARY KEY ([EnrollmentID]),
	FOREIGN KEY ([CourseID]) References Course([CourseID]),
	FOREIGN KEY ([StudentID]) References Student([StudentID])
);

INSERT INTO Enrollment (EnrollmentID, CourseID, StudentID)
VALUES ('E001', 'C001', 'S001'),
       ('E002', 'C002', 'S002'),
       ('E003', 'C002', 'S001'),
       ('E004', 'C001', 'S003');

 
select * from Student;
 
Select * from Professor;
 
Select * from Course;
 
select * from Enrollment;
~~~

## Functions of SQL

### Create Table
~~~sql
CREATE TABLE EmployeeData (
	EmployeeID INT PRIMARY KEY,
	FirstName VARCHAR(50),
	LastName VARCHAR(50),
	Salary INT,
	StartDate DATE
);


INSERT INTO EmployeeData (EmployeeID, FirstName, LastName, Salary, StartDate) VALUES
(1, 'John', 'Doe', 70000, '2020-05-01'),
(2, 'Jane', 'Smith', 85000, '2018-08-15'),
(3, 'Emily', 'Jones', 94000, '2019-12-30'),
(4, 'Chris', 'Brown', 62000, '2021-03-22');
~~~


### Task 1: Sort the employees by the length of their first names in descending order
~~~sql
select * 
from EmployeeData
order by LEN(FirstName) DESC;
~~~

### Task 4: Write a query to calculate the tenure of each employee in complete years as of today.
~~~sql
SELECT *, DATEDIFF(YEAR, StartDate, GETDATE()) AS TenureInYears
FROM EmployeeData;
~~~

### Task 5:Assume a yearly salary increase of 3% for each employee. Write a query to calculate their new salary rounded to the nearest whole number.
~~~sql
SELECT * , FLOOR(0.03*SALARY+SALARY) AS NEW_SALARY
FROM EmployeeData;
~~~
