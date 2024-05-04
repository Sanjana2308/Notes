# Day 3 Notes
## DDL Exercises
### Exercise - 1
We will be using a database with data about some of Pixar's classic movies for most of our exercises. This first exercise will only involve the Movies table, and the default query below currently shows all the properties of each movie. To continue onto the next lesson, alter the query to find the exact information we need for each task.<br>

1. Find the title of each film<br>
Ans.
select title from movies;
<br>
2. Find the director of each film<br>
Ans.
select director from movies;
<br>

3. Find the title and director of each film<br>
Ans.
select title, director from movies;
<br>

4. Find the title and year of each film<br>
Ans.
select title, year from movies;
<br>

4. Find all the information about each film
<br>
Ans.
select * from movies;
<br><br>

### Exercise 2
1. Find the movie with a row id of 6 
<br>
Ans.
SELECT Title FROM movies where Id = 6;
<br><br>

2.  Find the movies released in the years between 2000 and 2010
<br>
Ans.
SELECT * FROM movies where year between 2000 and 2010;
<br><br>

3. Find the movies not released in the years between 2000 and 2010
<br>
Ans.
SELECT * FROM movies where year not between 2000 and 2010;
<br><br>

4. ind the first 5 Pixar movies and their release year
<br>
Ans.
SELECT * FROM movies where id between 1 and 5;
<br><br>

### Exercise 3
1. SELECT * FROM movies where title like "Toy Story%";<br>
2. SELECT * FROM movies where director like "John Lasseter";<br>
3. SELECT title, director FROM movies where director not like "John Lasseter";<br>
4. SELECT * FROM movies where Title like "Wall-_";<br>

### Exercise 4
1. SELECT distinct director
FROM movies
order by Director;

2. SELECT * 
FROM movies
order by year desc
limit 4;

3. SELECT * 
FROM movies
order by title
limit 5;

4. SELECT * 
FROM movies
order by title
limit 5 offset 5;

### Exercise 5

1. SELECT *
FROM north_american_cities
where Country = "Canada";

2. SELECT *
FROM north_american_cities
where country = "United States"
order by latitude desc;

3. SELECT *
FROM north_american_cities
where longitude < (select longitude from north_american_cities where city = 'Chicago')
order by longitude;

4. SELECT *
FROM north_american_cities
where Country = "Mexico"
order by Population desc
limit 2;

5. SELECT *
FROM north_american_cities
where Country = "United States"
order by Population desc
limit 2 offset 2;


### Exercise 6
3. SELECT * 
FROM movies
inner join Boxoffice 
on id = movie_id
order by Rating desc;

### Exercise 7
1. SELECT DISTINCT building FROM employees;

2. select * 
from buildings;
3. 

### Exercise 8

2. SELECT *
from Buildings
left join Employees
on Building_Name = building
where name is null;

### Exercise 9
1.

2. SELECT role, avg(Years_employed)
from Employees
group by Role;

3. SELECT Building,SUM(Years_employed) 
FROM employees
GROUP BY Building;

### Exercise 10
1. SELECT count(Role)
from Employees
group by Role
having Role like "Artist";

2. select Role, count(Role)
from Employees
group by Role;

3. select Role, sum(Years_employed)
from Employees
group by Role
having Role like "Engineer";

<hr>

### Exercise 11
~~~sql
1. SELECT count(Title), Director
from Movies
group by Director;

2. SELECT DIRECTOR,SUM(DOMESTIC_SALES+INTERNATIONAL_SALES) FROM movies LEFT JOIN BOXOFFICE ON ID = MOVIE_ID GROUP BY DIRECTOR;

3. 
~~~

<hr>

### Exercise 12
~~~sql
1. insert into movies values (4, "Toy Story 4", "nag aswin", 2024, 155);
2. 
~~~

### Exercise 13
~~~sql
1. 
delete from movies
where year < 2005; 

2.
delete
from movies 
where Director = "Andrew Stanton";

~~~


