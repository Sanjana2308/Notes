# Day 6

## Type of Joins

~~~sql
CREATE TABLE Employees (
    EmployeeID INT,
    Name VARCHAR(50),
    Salary DECIMAL(10,2),
    DepartmentID INT
);
 
CREATE TABLE Departments (
    DepartmentID INT,
    DepartmentName VARCHAR(50),
    MinSalary DECIMAL(10,2)
);
 
INSERT INTO Employees VALUES (1, 'John Doe', 50000, 101), (2, 'Jane Smith', 40000, 102);
INSERT INTO Departments VALUES (101, 'HR', 45000), (102, 'Marketing', 35000);
 
Select * from Employees
 
Select * from Departments
 
--Example of Inner Join which is not Equi Join
Select Name, Salary, DepartmentName,  MinSalary
From Employees
Inner Join Departments 
on Salary > MinSalary
~~~

### Create Database using commands
~~~sql
CREATE DATABASE fun;--Creating
USE fun;--Switching
USE joins;
Exec sp_renamedb 'fun', 'cool';--Renaming
DROP DATABASE cool;--Dropping
~~~

## Abstract SQL Documentation
### Task 1 : Top 3 Purc_Amt Clue: Read docs
~~~sql
select * 
from Orders 
order by purch_amt desc
OFFSET 0 rows
FETCH NEXT 3 ROWS ONLY;
~~~


### Task 2 : Format date -25 Apr 2012 --Clue: String Functions - Format
~~~sql
select *, FORMAT(ord_date, 'dd MMM yyyy')
from orders
order by purch_amt desc
OFFSET 0 rows
FETCH NEXT 3 ROWS ONLY;
~~~

### Task 3: Modify the statement - Asking the new user - Top n orders
~~~sql
declare @r int = 3;
SELECT *
FROM orders 
ORDER BY purch_amt  
OFFSET 0 ROWS 
FETCH NEXT @r ROWS ONLY;
~~~

## Set Operations: Union , Intersect - common, Except - uncommon

~~~sql
Create Database setoperations;
use setoperations;
 
 
CREATE TABLE Employees (
    EmployeeID INT,
    Name VARCHAR(50),
    Department VARCHAR(50)
);
 
INSERT INTO Employees (EmployeeID, Name, Department) VALUES
(1, 'Alice', 'Engineering'),
(2, 'Bob', 'Marketing'),
(3, 'Charlie', 'Engineering'),
(4, 'Dana', 'HR');
 
 
CREATE TABLE Applicants (
    ApplicantID INT,
    Name VARCHAR(50),
    AppliedFor VARCHAR(50)
);
 
INSERT INTO Applicants (ApplicantID, Name, AppliedFor) VALUES
(5, 'George', 'Engineering'),
(6, 'Helen', 'Marketing'),
(7, 'Ian', 'Marketing'),
(3, 'Charlie', 'Sales');
 
Select * from Employees;
Select * from Applicants;
 
--AnB Intersect
Select Department from Employees
Intersect
Select AppliedFor from Applicants;

-- AUB Union
Select Department from Employees
Union
Select AppliedFor from Applicants;

-- A-B Except
Select Department from Employees
Except
Select AppliedFor from Applicants;

-- B-A Except
Select AppliedFor from Applicants
Except
Select Department from Employees;
~~~

-- Create new tables for tasks on union, intersect and except
~~~sql
CREATE TABLE Products (
ProductID INT,
ProductName VARCHAR(50),
Category VARCHAR(50),
InStock CHAR(3)
);
 
INSERT INTO Products (ProductID, ProductName, Category, InStock) VALUES
(1, 'Laptop', 'Electronics', 'Yes'),
(2, 'Smartphone', 'Electronics', 'No'),
(3, 'Coffee Maker', 'Appliances', 'Yes'),
(4, 'Blender', 'Appliances', 'Yes'),
(5, 'T-shirt', 'Apparel', 'No');

CREATE TABLE Orders (
OrderID INT,
ProductID INT,
CustomerName VARCHAR(50),
Quantity INT);
 
INSERT INTO Orders (OrderID, ProductID, CustomerName, Quantity) VALUES
(100, 1, 'Alice', 1),
(101, 3, 'Bob', 2),
(102, 2, 'Charlie', 1),
(103, 4, 'Dana', 1),
(104, 3, 'Alice', 1);
~~~

### Task 1: List all distinct products that are either in stock or have been arrived (Clue: Sub Query)
~~~sql
select ProductName
from products
where InStock = 'Yes'
Union
select ProductName
from Products
where ProductID In(select ProductID from Orders);
~~~

### Task 2: Identify products that are both in stock and have been ordered
~~~sql
select ProductName
from products
where InStock = 'Yes'
Intersect
select ProductName
from Products
where ProductID In(select ProductID from Orders);
~~~

### Task 3: Find products that are in stock but never have been ordered
~~~sql
select ProductName
from products
where InStock = 'Yes'
Except
select ProductName
from Products
where ProductID In(select ProductID from Orders);
~~~

## Advanced group by and order by


~~~sql
CREATE TABLE EmployeeSales (
    EmployeeID INT,
    Region VARCHAR(50),
    Category VARCHAR(50),
    Quarter VARCHAR(10),
    SalesAmount DECIMAL(10,2)
);
 
INSERT INTO EmployeeSales (EmployeeID, Region, Category, Quarter, SalesAmount)
VALUES
    (101, 'North', 'Electronics', 'Q1', 1200.00),
    (101, 'North', 'Electronics', 'Q2', 1500.00),
    (102, 'North', 'Clothing', 'Q1', 800.00),
    (102, 'North', 'Clothing', 'Q2', 950.00),
    (103, 'South', 'Electronics', 'Q1', 1000.00),
    (103, 'South', 'Clothing', 'Q1', 1200.00),
    (104, 'East', 'Electronics', 'Q2', 1150.00),
    (104, 'East', 'Clothing', 'Q2', 500.00),
    (105, 'West', 'Electronics', 'Q1', 1900.00),
    (105, 'West', 'Clothing', 'Q1', 1100.00),
    (105, 'West', 'Electronics', 'Q2', 2100.00),
    (105, 'West', 'Clothing', 'Q2', 1300.00);

select * from EmployeeSales;
~~~

1. Compound Sort
### Task 1: Sort by Region and then sales amount (Level 1: region, level 2: sales amount)
~~~sql
select * 
from EmployeeSales
order by Region, SalesAmount DESC;
~~~

### Task 2:  Year to date sale - Q1 - today (How much sales?) (Level 1: region, level 2: category)
~~~sql
select Region, Category, SUM(SalesAmount) as SumAmount
from EmployeeSales
group by Region, Category
order by Region, Category;
~~~


### Task 3: Grouping Sets - R-C, R-Q, R, Q

~~~sql
select Region, SUM(SalesAmount)
from EmployeeSales
group by Region;

select Quarter, SUM(SalesAmount)
from EmployeeSales
group by Quarter;

select Quarter, Region, SUM(SalesAmount)
from EmployeeSales
group by Quarter, Region;

select  Region, Quarter, SUM(SalesAmount)
from EmployeeSales
group by Region, Quarter
order by SUM(SalesAmount) DESC;
~~~

~~~sql
--Actual Query
select Region, Category, [Quarter], SUM(SalesAmount) 
from EmployeeSales
group by GROUPING SETS(
	(Region, Category),
	(Region, Quarter),
	(Region),
	(Quarter)
)
order by GROUPING(Region), GROUPING(Category), GROUPING([Quarter]);
~~~

## Exists Keyword
### Table Creation
~~~sql
CREATE DATABASE projects; -- Creating
 
USE projects; -- Switching
 
 
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(50)
);
 
CREATE TABLE projects (
    project_id INT PRIMARY KEY,
    project_name VARCHAR(100),
    employee_id INT,
    start_date DATE,
    FOREIGN KEY (employee_id) REFERENCES employees(employee_id)
);
 
 
INSERT INTO employees (employee_id, name, department) VALUES
(1, 'Alice', 'Engineering'),
(2, 'Bob', 'Engineering'),
(3, 'Charlie', 'HR'),
(4, 'David', 'Marketing');
 
INSERT INTO projects (project_id, project_name, employee_id, start_date) VALUES
(101, 'Alpha', 1, '2021-01-10'),
(102, 'Beta', 2, '2021-03-15'),
(103, 'Gamma', 1, '2021-02-20');

select * from employees;
select * from projects;
~~~

### Task 1: Find employees from the engineering department who are working on any project - Exists
~~~sql
select * 
from employees o
where department = 'Engineering' and  Exists(
	select * 
	from projects i
	where o.employee_id = i.employee_id
);
~~~

~~~sql
INSERT INTO employees (employee_id, name, department) VALUES
(5, 'Sneha', 'Engineering');
~~~

### Task 2: Find employees from the engineering department who are not working on any project - NOT Exists
~~~sql
select * 
from employees o
where department = 'Engineering' and  not Exists(
	select * 
	from projects i
	where o.employee_id = i.employee_id
);
~~~