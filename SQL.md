# SQL

## CREATING DATABASE

```sql
CREATE DATABASE testDB;

//once the database is created you can check it in the list of database by doing 
SHOW DATABASES;// 
```

# **DROP DATABASE**

it is used to drop (Delete) a database.

```sql
DROP DATABASE databasename;
```

# **The SQL BACKUP DATABASE Statement**

Used to backup the sql databases so they don’t get lost when there is any error on the server 

```sql
BACKUP DATABASE databasename

TO DISK = 'filepath'; 
```

# CREATE TABLE

Used to create a table that contains columns and tables 

```sql
CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);
```

### **Create Table Using Another Table**

```sql
CREATE TABLE TestTable AS
SELECT customername, contactname
FROM customers;
```

# **DROP (DELETE) TABLE :**

Deletes only the table

```sql
DROP TABLE table_name;
```

# **SQL TRUNCATE TABLE**

Deletes only the items not the table 

```sql
TRUNCATE TABLE table_name;
```

# **ALTER TABLE**

The `ALTER TABLE` statement is used to add, delete, or modify columns in an existing table.

The `ALTER TABLE` statement is also used to add and drop various constraints on an existing table.

```sql
ALTER TABLE table_name
ADD column_name datatype;
```

### **ALTER TABLE - DROP COLUMN**

```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

### **ALTER TABLE - RENAME COLUMN**

```sql
ALTER TABLE table_name
RENAME COLUMN old_name to new_name;
```

# SQL Constraints

SQL constraints are used to specify rules for the data in a table.

Constraints are used to limit the type of data that can go into a table. This ensures the accuracy and reliability of the data in the table. If there is any violation between the constraint and the data action, the action is aborted.

- [`NOT NULL`](https://www.w3schools.com/sql/sql_notnull.asp) - Ensures that a column cannot have a NULL value
- [`UNIQUE`](https://www.w3schools.com/sql/sql_unique.asp) - Ensures that all values in a column are different
- [`PRIMARY KEY`](https://www.w3schools.com/sql/sql_primarykey.asp) - A combination of a `NOT NULL` and `UNIQUE`. Uniquely identifies each row in a table
- [`FOREIGN KEY`](https://www.w3schools.com/sql/sql_foreignkey.asp) - Prevents actions that would destroy links between tables
- [`CHECK`](https://www.w3schools.com/sql/sql_check.asp) - Ensures that the values in a column satisfies a specific condition
- [`DEFAULT`](https://www.w3schools.com/sql/sql_default.asp) - Sets a default value for a column if no value is specified
- [`CREATE INDEX`](https://www.w3schools.com/sql/sql_create_index.asp) - Used to create and retrieve data from the database very quickly

## **SQL NOT NULL Constraint**

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255) NOT NULL,
    Age int
);
```

## SQL UNIQUE Constraint

The `UNIQUE` constraint ensures that all values in a column are different.

Both the `UNIQUE` and `PRIMARY KEY` constraints provide a guarantee for uniqueness for a column or set of columns.

```sql
CREATE TABLE Persons (
    ID int NOT NULL PRIMARY KEY,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int
);
```

## **SQL FOREIGN KEY Constraint**

The `FOREIGN KEY` constraint is used to prevent actions that would destroy links between tables.

A `FOREIGN KEY` is a field (or collection of fields) in one table, that refers to the [`PRIMARY KEY`](https://www.w3schools.com/sql/sql_primarykey.asp) in another table.

The table with the foreign key is called the child table, and the table with the primary key is called the referenced or parent table.

```sql
CREATE TABLE Orders (
    OrderID int NOT NULL,
    OrderNumber int NOT NULL,
    PersonID int,
    PRIMARY KEY (OrderID),
    FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
);
```

## **SQL CHECK Constraint**

The `CHECK` constraint is used to limit the value range that can be placed in a column.

If you define a `CHECK` constraint on a column it will allow only certain values for this column.

If you define a `CHECK` constraint on a table it can limit the values in certain columns based on values in other columns in the row.

```sql
CREATE TABLE Persons (
    ID int NOT NULL,
    LastName varchar(255) NOT NULL,
    FirstName varchar(255),
    Age int,
    CHECK (Age>=18)
);
```

# SQL Injection

SQL injection is a code injection technique that might destroy your database.

SQL injection is one of the most common web hacking techniques.

SQL injection is the placement of malicious code in SQL statements, via web page input.**SQL Views**

# **SQL Views**

In SQL, a view is a virtual table based on the result-set of an SQL statement.

A view contains rows and columns, just like a real table. The fields in a view are fields from one or more real tables in the database.

You can add SQL statements and functions to a view and present the data as if the data were coming from one single table.

A view is created with the `CREATE VIEW` statement.

```sql
CREATE VIEW [Brazil Customers] AS
SELECT CustomerName, ContactName
FROM Customers
WHERE Country = 'Brazil';
```

# Joins

A `JOIN` clause is used to combine rows from two or more tables, based on a related column between them.

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;
```

### Inner Joins

The `INNER JOIN` keyword selects records that have matching values in both tables.

```sql
SELECT Orders.OrderID, Customers.CustomerName, Orders.OrderDate
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID;
```

SYNTAX:

```sql
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name = table2.column_name;
```

Join is default for the Inner Join so when you write Join , its get to inner join and select only the matching values from tables 

### Left Joins

The LEFT JOIN returns all the values from the Left Table (Table1) to the right Table . The result is 0 records from the right side, if there is no match.

```sql
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name = table2.column_name;
```

### Right Joins

The `RIGHT JOIN` keyword returns all records from the right table (table2), and the matching records from the left table (table1). The result is 0 records from the left side, if there is no match.

```sql
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name = table2.column_name;
```

### Full Outer Joint

The `FULL OUTER JOIN` keyword returns all records when there is a match in left (table1) or right (table2) table records.

```sql
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2
ON table1.column_name = table2.column_name
WHERE condition;
```

### Self Join

A Self join is when a table is joined to itself  — as if the same table is two different tables.

It’s used when the rows inside one table need to be compared **to other rows of the *same* table**.

# **Why do we need self joins?**

To answer questions like:

- “Who is the manager of each employee?” (manager is in the same table)
- “What’s the previous order for this customer?”
- “Which users referred other users?”
- “Which products belong to the same category?”
- “Compare two rows from the same table”

Before window functions existed, self joins were the only way to do “previous row” analysis.

Write a SQL query to find:

- `customer_id`

For customers who:

- Have placed **at least one order**
- But have **never placed a completed order**

```sql
SELECT customer_id
FROM orders
GROUP BY customer_id
HAVING 
    COUNT(*) >= 1
    AND SUM(CASE WHEN status = 'Completed' THEN 1 ELSE 0 END) = 0;

```

# Windows Function

Window functions (also called analytic functions in some databases like Oracle) are a powerful feature in SQL that allow you to perform calculations across a set of rows that are related to the current row, without collapsing the result into a single row like regular aggregate functions do.

OR 

A window function lets you perform calculations over a set of rows that are related to the current row, while still returning one row per original row (no grouping or collapsing like with GROUP BY)

| Goal | Tool |
| --- | --- |
| Top order per customer | `ROW_NUMBER()` |
| 2nd highest salary | `DENSE_RANK()` |
| Running totals | `SUM() OVER` |
| Compare to previous row | `LAG()` |
| De-duplication | `ROW_NUMBER()` |

| Want | Use |
| --- | --- |
| Reduce rows | GROUP BY |
| Keep rows + metrics | WINDOW |
| Multi-step logic | CTE |
| Ranking / ordering logic | WINDOW |

### **Common Window Functions**

| **Category** | **Function Examples** | **Purpose** |
| --- | --- | --- |
| Ranking | ROW_NUMBER(), RANK(), DENSE_RANK(), NTILE(n) | Assign ranks or divide into buckets |
| Aggregation | SUM(), AVG(), COUNT(), MIN(), MAX() | Running totals, moving averages |
| Value access | LAG(column, n), LEAD(column, n) | Access previous/next row values |
| Percentiles | PERCENT_RANK(), CUME_DIST() | Relative position in the set |

```sql
use swiggy;
select * from restaurants;

-- 1. Create new column containing average rating of restaurants throught the dataset
select *,  round(avg(rating) over(),2) as 'avg_rating' from restaurants;

-- 2. Create new column containing average rating_count of restaurants throught the dataset
select *,  round(avg(rating_count) over(),0) as 'avg_rating_count' from restaurants;

-- 3. Create new column containing average cost of restaurants throught the dataset
select *,  round(avg(cost) over(),0) as 'avg_cost' from restaurants;

-- 4. Create column containing average, min, max of cost,rating,rating_count of restaurants throught the dataset
select id, name, city, cuisine, rating,
	round(max(rating) over(), 2) as 'max_rating',
    round(avg(rating) over(), 2) as 'avg_rating',
    round(min(rating) over(), 2) as 'min_rating',
    
    round(max(cost) over(), 2) as 'max_cost',
    round(avg(cost) over(), 2) as 'avg_cost',
    round(min(cost) over(), 2) as 'min_cost'
    
from restaurants;

-- 5. Create column containing average cost of the city where that specific restaurant is from
select *, round(avg(cost) over( partition by city) ) as 'avg_cost' from restaurants;

-- 6. Create column containing average cost of the cuisine which that specific restaurant is serving
select *, round(avg(cost) over( partition by cuisine) ) as 'avg_cost' from restaurants;

-- 7. Create both column together
select *, 
	round(avg(cost) over( partition by city) ) as 'avg_cost_city',
    round(avg(cost) over( partition by cuisine) ) as 'avg_cost_cuisine'
from restaurants;

-- 8. List the restaurants whose cost is more than the average cost of the restaurants?
select * from restaurants where cost > (select avg(cost) from restaurants);
select * from (select *, avg(cost) over() as 'avg_cost' from restaurants) t where t.cost > t.avg_cost; 

-- 10. List the restaurants whose cuisine cost is more than the average cost?
select * from (select *, avg(cost) over(partition by cuisine) as 'avg_cost' from restaurants) t where t.cost > t.avg_cost; 
```

# Rank

```sql
use swiggy;
select * from restaurants;

-- 1. Rank every restaurant from most expensive to least expensive
select * ,rank() over(order by cost desc) as 'rank' from restaurants;

-- 2. Rank every restaurant from most visited to least visited
select * ,rank() over(order by rating_count desc) as 'rank' from restaurants;

-- 3. Rank every restaurant from most expensive to least expensive as per their city
select * ,rank() over(partition by city order by cost desc) as 'rank' from restaurants;

-- 4. Dense-rank every restaurant from most expensive to least expensive as per their city
select * ,
	rank() over(order by cost desc) as 'rank' ,
	dense_rank() over(order by cost desc) as 'dense_rank' 
from restaurants;

-- 5. Row-number every restaurant from most expensive to least expensive as per their city
select * ,
	rank() over(order by cost desc) as 'rank' ,
	dense_rank() over(order by cost desc) as 'dense_rank',
    row_number() over(order by cost desc) as 'row_number' 
from restaurants;

-- 6. Rank every restaurant from most expensive to least expensive as per their city along with its city [Adilabad - 1, Adilabad - 2]
select *, concat(city,' - ' ,row_number() over(partition by city order by cost desc)) as 'rank' from restaurants;

-- 7. Find top 5 restaurants of every city as per their revenue
select * from (select *, 
				cost*rating_count as 'revenue', 
				row_number() over(partition by city order by rating_count*cost desc) as 'rank' from restaurants) t
where t.rank < 6;

-- 8. Find top 5 restaurants of every cuisine as per their revenue
select * from (select *, 
				cost*rating_count as 'revenue', 
				row_number() over(partition by cuisine order by rating_count*cost desc) as 'rank' from restaurants) t
where t.rank < 6;
```

# Advance Window Function

```sql
use swiggy;
select * from restaurants;

-- 1. List the top 5 cuisines as per the revenue generated by top 5 restaurants of every cuisine
select cuisine, sum(rating_count*cost) as 'revenue'from 	
( 	select *, cost*rating_count, 
	row_number() over(partition by cuisine order by cost*rating_count desc) as 'rank'
    from restaurants
) t 
where t.rank < 6
group by cuisine
order by revenue desc;

-- 2. What is the of the total revenue is generated by top 1% restaurants
select sum(cost*rating_count) as 'revenue' from
	(select *, cost*rating_count, row_number() over(order by cost*rating_count desc) as 'rank'
		from restaurants) t
	where t.rank <= 614;

-- 3. Check the same for top 20% restaurants
select sum(cost*rating_count) as 'revenue' from
	(select *, cost*rating_count, row_number() over(order by cost*rating_count desc) as 'rank'
		from restaurants) t
	where t.rank <= 12280;

-- 4. What % of revenue is generated by top 20% of restaurants with respect to total revenue?
with 
	q1 as (select sum(cost*rating_count) as 'top_revenue' from
			(select *, cost*rating_count, row_number() over(order by cost*rating_count desc) as 'rank'
				from restaurants) t
			where t.rank <= 12280),
	q2 as (select sum(cost*rating_count) as 'total_revenue' from restaurants)
    
select (top_revenue/total_revenue)*100 as 'revenue %' from q1,q2;
```

## CTE (Common Table Expression):

**What is it?** Think of a CTE as a **temporary view** that exists only for the duration of a single query. It allows you to give a name to a query result and then reference that name later, just like a regular table.

**Why use it?**

1. **Readability:** It breaks complex logic into linear, readable steps (step 1, step 2, final result).
2. **Organization:** It avoids messy nested subqueries (subqueries inside subqueries inside subqueries).

A CTE always starts with the `WITH` keyword.

### Part 2: Intermediate Usage (Multiple CTEs)

You can define multiple CTEs in a single `WITH` clause by separating them with a comma. This is where the "step-by-step" power shines.

**Scenario:** You want to find departments where the *average* salary is higher than the *company-wide* average salary.

1. **Step 1:** Calculate company average.
2. **Step 2:** Calculate department averages.
3. **Step 3:** Compare them.

```sql
WITH 
    -- Step 1: Get the single number for company average
    company_stats AS (
        SELECT AVG(salary) as avg_all FROM employees
    ),
    
    -- Step 2: Get the list of department averages
    dept_stats AS (
        SELECT department_id, AVG(salary) as avg_dept
        FROM employees
        GROUP BY department_id
    )

-- Step 3: Final Logic
SELECT 
    d.department_id, 
    d.avg_dept
FROM dept_stats d
JOIN company_stats c ON d.avg_dept > c.avg_all;
```

### Part 3: Advanced (Recursive CTEs)

This is the superpower of CTEs. A **Recursive CTE** is a query that **refers to itself**. It is primarily used for hierarchical data (like organizational charts, category trees, or flight paths) or generating sequences.

### Structure of a Recursive CTE

It has three specific parts linked by `UNION ALL`:

1. **Anchor Member:** The starting point (e.g., the CEO, or the number 1).
2. **UNION ALL:** The glue.
3. **Recursive Member:** The query that references the CTE name itself to find the "next level."

```sql

```

# View

```sql
use swiggy;
select * from restaurants;

-- 1. Create the view

drop view if exists rest;
create view rest as (
		select name, city, rating, rating_count as 'orders', 
        cuisine, cost, cost*rating_count as 'revenue' from restaurants);
select * from rest;

-- 2. Create a view for end_user
drop view if exists user_view;
create view user_view as (
		select name, city, rating, rating_count as 'orders', 
        cuisine, cost from restaurants);
select * from user_view;

-- 3. Create a view of sweet dishes
drop view if exists rest_of_sweet_dishes;
create view rest_of_sweet_dishes as (
		select * from restaurants where cuisine in ('Sweets', 'Desserts','Bakery','Ice Cream'));
select * from rest_of_sweet_dishes;

-- 4. Create a view of top 100 restaurants
drop view if exists top_100;
create view top_100 as (
		select * from restaurants order by rating_count desc limit 100);
select * from top_100;

-- 5. Create a view of restaurant atleast 100 people visited
drop view if exists least_100;
create view least_100 as (
		select * from restaurants order by rating_count asc limit 100);
select * from least_100;

-- 6. Create a view of top 1000 most expensive restaurants
drop view if exists top_1000_exp;
create view top_1000_exp as (
		select * from restaurants order by cost desc limit 1000);
select * from top_1000_exp;

-- 7. Create a view for top-rated restaurants in each city
drop view if exists top_rated_rest_per_city;
create view top_rated_rest_per_city as (
		select * from ( 
			select *,  row_number() over(partition by city order by rating*rating_count desc) as 'rank' 
				from restaurants) 
			as ranked_table
		where ranked_table.rank = 1);
select * from top_rated_rest_per_city;
```

# Exporting table

```sql
SELECT * FROM restaurants;

drop table if exists sirsa_restaurants;
drop table if exists city_statistics;
drop table if exists expensive_restaurants;

-- Create a new table names 'sirsa_restaurants' containing restaurants of sirsa only
create table if not exists sirsa_restaurants as SELECT * FROM restaurants where city = 'sirsa';
select * from sirsa_restaurants;

-- Create a new table named 'city_statistics' containing aggregated statistics for each city
create table if not exists city_statistics as 
	SELECT city , avg(rating) as avg_rating, count(*) as num_of_restaurants FROM restaurants group by city;
select * from city_statistics;

-- Create a new table named 'expensive_restaurants' containing restaurants with a cost greater than 500
create table if not exists expensive_restaurants as 
	SELECT * from restaurants where cost > 500;
select * from expensive_restaurants;
```

# Questions

1. Query the list of *CITY* names starting with vowels (i.e., `a`, `e`, `i`, `o`, or `u`) from **STATION**. Your result *cannot* contain duplicates.

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE
    LOWER(CITY) LIKE 'a%' OR
    LOWER(CITY) LIKE 'e%' OR
    LOWER(CITY) LIKE 'i%' OR
    LOWER(CITY) LIKE 'o%' OR
    LOWER(CITY) LIKE 'u%';
```

1. Query the list of *CITY* names from **STATION** which have vowels (i.e., *a*, *e*, *i*, *o*, and *u*) as both their first *and* last characters. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE
    LOWER(LEFT(CITY, 1)) IN ('a', 'e', 'i', 'o', 'u')
    AND
    LOWER(RIGHT(CITY, 1)) IN ('a', 'e', 'i', 'o', 'u');
```

1. Query the list of *CITY* names from **STATION** that *do not start* with vowels. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE LOWER(LEFT(CITY, 1)) NOT IN ('a', 'e', 'i', 'o', 'u');
```

1. Query the list of *CITY* names from **STATION** that *do not end* with vowels. Your result cannot contain duplicates

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE LOWER(RIGHT(CITY, 1)) NOT IN ('a', 'e', 'i', 'o', 'u');
```

1. Query the list of *CITY* names from **STATION** that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

```sql
SELECT DISTINCT CITY
FROM STATION
WHERE
    LOWER(LEFT(CITY, 1)) NOT IN ('a', 'e', 'i', 'o', 'u')
    OR
    LOWER(RIGHT(CITY, 1)) NOT IN ('a', 'e', 'i', 'o', 'u');
```

1. Query the *Name* of any student in **STUDENTS** who scored higher than  *Marks*. Order your output by the *last three characters* of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending *ID*.

```sql
SELECT Name FROM STUDENTS
WHERE Marks > 75
ORDER BY RIGHT(Name, 3), ID;
```

1. Write a query identifying the *type* of each record in the **TRIANGLES** table using its three side lengths. Output one of the following statements for each record in the table:
- **Equilateral**: It's a triangle with  sides of equal length.
- **Isosceles**: It's a triangle with  sides of equal length.
- **Scalene**: It's a triangle with  sides of differing lengths.
- **Not A Triangle**: The given values of *A*, *B*, and *C* don't form a triangle.

```sql
SELECT
    CASE
        WHEN A + B <= C OR A + C <= B OR B + C <= A THEN 'Not A Triangle'
        WHEN A = B AND B = C THEN 'Equilateral'
        WHEN A = B OR B = C OR A = C THEN 'Isosceles'
        ELSE 'Scalene'
    END
FROM TRIANGLES;
```

1. Query a count of the number of cities in CITY having a Population larger than 1000000.

```sql
SELECT COUNT(*)
FROM CITY
WHERE POPULATION > 1000000;
```

1. Query the total population of all cities in **CITY** where *District* is **California**.

```sql
SELECT COUNT(*)
FROM CITY
WHERE POPULATION > 1000000;
```

1. Query the average population for all cities in **CITY**, rounded *down* to the nearest integer.

```sql
SELECT ROUND(AVG(POPULATION)) From CITY;
```

1. Query the difference between the maximum and minimum populations in **CITY**.

```sql
SELECT MAX(POPULATION)-MIN(POPULATION) From CITY;
```

1. Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38.7880  and less than 137.2345 . Truncate your answer to  decimal places.

```sql
SELECT CAST(TRUNC(SUM(LAT_N), 4) AS DECIMAL(18, 4))
FROM STATION
WHERE LAT_N > 38.7880 AND LAT_N < 137.2345;
```

1. Query the smallest *Northern Latitude* (*LAT_N*) from **STATION** that is greater than . Round your answer to  4 decimal places.

```sql
SELECT CAST(ROUND(MIN(LAT_N), 4) AS DECIMAL(18, 4))
FROM STATION
WHERE LAT_N > 38.7880;
```

1. Query the Western Longitude (LONG_W)where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7880 . Round your answer to  4 decimal places.

```sql
SELECT CAST(ROUND(LONG_W, 4) AS DECIMAL(18,4))
FROM STATION
WHERE LAT_N > 38.7880
ORDER BY LAT_N ASC
LIMIT 1;
```

1. Consider P1(a,b) and p2(c,d)  to be two points on a 2D plane.
a  happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
b  happens to equal the minimum value in Western Longitude (LONG_W in STATION).
 c happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
 d happens to equal the maximum value in Western Longitude (LONG_W in STATION).
Query the Manhattan Distance between points  and  and round it to a scale of  decimal places. 

```sql
SELECT CAST(ROUND(
    (MAX(LAT_N) - MIN(LAT_N)) + (MAX(LONG_W) - MIN(LONG_W)), 
    4) AS DECIMAL(18,4)
)
FROM STATION;
```

1. Consider  p1(a,b) and p2(c,d) to be two points on a 2D plane where  are the respective minimum and maximum values of Northern Latitude (LAT_N) and  are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.
Query the Euclidean Distance between points  and  and format your answer to display  decimal digits.

```sql
SELECT ROUND(
    SQRT(
        POWER(MAX(LAT_N) - MIN(LAT_N), 2) + 
        POWER(MAX(LONG_W) - MIN(LONG_W), 2)
    ), 
    4
)
FROM STATION;
```

1. A median is defined as a number separating the higher half of a data set from the lower half. Query the median of the Northern Latitudes (LAT_N) from STATION and round your answer to 4 decimal places

```sql
SELECT ROUND(
         CAST(AVG(LAT_N) AS DECIMAL(12,4)),   -- cast to decimal first
         4
       ) AS median
FROM (
    SELECT LAT_N,
           ROW_NUMBER() OVER (ORDER BY LAT_N ASC)  AS row_asc,
           ROW_NUMBER() OVER (ORDER BY LAT_N DESC) AS row_desc
    FROM STATION
) AS x
WHERE row_asc IN (row_desc, row_desc + 1, row_desc - 1);
```

![Screenshot 2025-10-26 213812.png](Screenshot_2025-10-26_213812.png)

```sql
SELECT F1.X, F1.Y
FROM Functions AS F1
JOIN Functions AS F2 ON F1.X = F2.Y AND F1.Y = F2.X
GROUP BY F1.X, F1.Y
HAVING F1.X < F1.Y OR (F1.X = F1.Y AND COUNT(*) > 1)
ORDER BY F1.X;
```

Write a query to find the median salary from an `employees` table.

```sql
WITH RankedSalaries AS (
    SELECT
        salary,
        ROW_NUMBER() OVER (ORDER BY salary ASC) AS row_num,
        COUNT(*) OVER () AS total_count
    FROM
        employees
)
SELECT
    AVG(salary) AS median_salary
FROM
    RankedSalaries
WHERE
    row_num IN (
        FLOOR((total_count + 1) / 2.0),  
        CEIL((total_count + 1) / 2.0)    
  );
```

1. **(New Concept: Self-Join)**
Write a query to show the name of each employee and the name of their *manager*.
(Hint: You join the `Employees` table to *itself*. Treat the first copy as the "Employee" table and the second copy as the "Manager" table).

```sql
SELECT
    e.name AS employee_name,
    m.name AS manager_name
FROM
    Employees e
LEFT JOIN
    Employees m ON e.manager_id = m.emp_id;
```

1. **(New Concept: String Functions)**
Write a query to find the `email` domain for each employee (e.g., 'company.com', 'gmail.com').
(Hint: You'll need `SUBSTRING` and `POSITION` (or `CHARINDEX`/`INSTR` depending on dialect). Find the position of '@' and take everything after it).

```sql
SELECT
    employee_name,
    SUBSTRING(email FROM POSITION('@' IN email) + 1) AS email_domain
FROM Employees;

```

1. **(New Concept: Date Differences)**
Write a query to find the *duration in days* of all "Completed" projects.
(Hint: Use `end_date - start_date` or `DATEDIFF(end_date, start_date)` depending on the SQL dialect).

```sql
SELECT
    title,
    DATEDIFF(end_date, start_date) AS duration_days
FROM
    Projects
WHERE
    status = 'Completed';
```

1. **(Advanced Aggregation: `SUM` with `CASE`)**
Write a query to count how many "Completed" projects and how many "In Progress" projects *each employee* is assigned to. The output should look like: `name | completed_count | in_progress_count`.
(Hint: Use `SUM(CASE WHEN ... THEN 1 ELSE 0 END)` inside the `SELECT` statement).

```sql
SELECT
    e.name,
    -- Count Completed Projects
    SUM(CASE WHEN p.status = 'Completed' THEN 1 ELSE 0 END) AS completed_count,
    -- Count In Progress Projects
    SUM(CASE WHEN p.status = 'In Progress' THEN 1 ELSE 0 END) AS in_progress_count
FROM
    Employees e
JOIN
    Assignments a ON e.emp_id = a.emp_id
JOIN
    Projects p ON a.project_id = p.project_id -- Need this join to see the status!
GROUP BY
    e.name;
```

1. **(New Concept: `NOT EXISTS`)**
Write a query to find the names of employees who have **not** been assigned to any projects.
(Hint: Use `WHERE NOT EXISTS (SELECT 1 FROM Assignments a WHERE ...)`).

```sql
SELECT 
    e.employee_name
FROM Employees e
WHERE NOT EXISTS (
    SELECT 1
    FROM Assignments a
    WHERE a.employee_id = e.employee_id
);

```

1. **(Null Handling)**
Write a query to list all member names and their `referred_by_id`. If the member does not have a referrer (NULL), display the value `0` instead.

- `COALESCE(x, y)` returns **x if it is NOT NULL**, otherwise y.
- So if `referred_by_id` is NULL, it returns **0**.

```sql
SELECT 
    member_name,
    COALESCE(referred_by_id, 0) AS referred_by_id
FROM Members;
```

1. **(Set Operations)**
Write a query to produce a single list of names that includes **all** `Members` and **all** `Instructors`. Ensure the final list has no duplicates if a name appears in both tables.

- `UNION` automatically **removes duplicates**.
- `UNION ALL` would keep duplicates, but we are not using that.
- Use aliases so both SELECTs return a column with the same name.

```sql
SELECT member_name AS name FROM Members
UNION
SELECT instructor_name AS name FROM Instructors;

```

1. **(Self-Join)**
Write a query to find the name of the member and the name of the person who referred them. Only return members who actually have a referrer.

- This is a **self-join** on the same Members table.
- `m` is the member, `r` is the referrer.
- Using **INNER JOIN** ensures only members who *have* a referrer are included.

```sql
SELECT 
    m.member_name AS member,
    r.member_name AS referrer
FROM Members m
JOIN Members r
    ON m.referred_by_id = r.member_id;

```

1. **(Time-Based Filtering)**
Write a query to find the names of all members who have checked in **before 08:00 AM**. (Assume `checkin_time` is a timestamp column).

- `CAST(timestamp AS TIME)` extracts the time portion.
- We filter those whose time is **before 08:00 AM**.

(You could also use `EXTRACT(HOUR FROM checkin_time)` but above is cleaner.)

```sql
SELECT 
    member_name
FROM Checkins
WHERE CAST(checkin_time AS TIME) < '08:00:00';

```

1. **(Advanced Grouping)**
Write a query to find the number of check-ins for *each hour of the day*. The result should show the `hour_of_day` (e.g., 7, 9, 18) and the `checkin_count`, ordered from earliest hour to latest.

- `EXTRACT(HOUR FROM timestamp)` pulls the hour (0–23).
- We group by this hour to count how many check-ins happened each hour.
- Ordered chronologically from early morning to late night.

```sql
SELECT 
    EXTRACT(HOUR FROM checkin_time) AS hour_of_day,
    COUNT(*) AS checkin_count
FROM Checkins
GROUP BY EXTRACT(HOUR FROM checkin_time)
ORDER BY hour_of_day;

```

1. **(Data Cleaning - String Formatting)**
Write a query to display the `customer_id` and a new column `full_name`. The `full_name` should combine the `first_name` and `last_name` with a space in between, and the entire name must be in **UPPERCASE** (e.g., 'JOHN DOE').

```sql
SELECT
    customer_id,
    UPPER(CONCAT(first_name, ' ', last_name)) AS full_name
FROM
    Customers;
```

1. **(Data Cleaning - Email Extraction)**
Write a query to count how many customers use each email provider. You need to extract the domain part of the email (the part after '@', e.g., 'gmail.com', 'yahoo.com') and count the users for each domain.

```sql
SELECT 
    SUBSTRING(email FROM POSITION('@' IN email) + 1) AS email_domain,
    COUNT(*) AS user_count
FROM Customers
GROUP BY SUBSTRING(email FROM POSITION('@' IN email) + 1)
ORDER BY user_count DESC;

```

1. **(Window Functions - ROW_NUMBER)**
Write a query to find the **most recent** stream for *each* customer. Show `customer_id`, `stream_date`, and `device_type`. If a customer has streamed multiple times, only return the row with the latest date.
- `ROW_NUMBER()` ranks rows **within each customer** by date (latest first).
- `rn = 1` picks only the most recent stream for each customer.

```sql
WITH ranked AS (
    SELECT 
        customer_id,
        stream_date,
        device_type,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id 
            ORDER BY stream_date DESC
        ) AS rn
    FROM Streams
)
SELECT 
    customer_id,
    stream_date,
    device_type
FROM ranked
WHERE rn = 1;

```

1. For each order, show:
- `order_id`
- `customer_id`
- `order_amount`
- **average order amount of that customer**

```sql
SELECT 
    order_id,
    customer_id,
    order_amount,
    AVG(order_amount) OVER (PARTITION BY customer_id) AS average_order_amount_of_customer
FROM orders
ORDER BY order_id;
```

1.  For each customer, rank their orders from **highest to lowest order amount**.

```sql
SELECT 
    customer_id,
    order_id,
    order_amount,
    RANK() OVER (PARTITION BY customer_id ORDER BY order_amount DESC) AS ranked
FROM orders
ORDER BY customer_id, order_amount DESC;
```

1.  Find the **highest order amount per customer** using window functions.

```sql
SELECT 
    customer_id,
    order_id,
    order_amount,
    MAX(order_amount) OVER (PARTITION BY customer_id) AS highest_order_amount_per_customer
FROM orders;
```

1. Find customers whose **latest order amount is greater than their average order amount**.

```sql
WITH ranked_orders AS (
    SELECT 
        *,
        ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_id DESC) AS rn,  -- latest order first
        AVG(order_amount) OVER (PARTITION BY customer_id)                  AS avg_amount
    FROM orders
)
SELECT 
    customer_id,
    order_id          AS latest_order_id,
    order_amount      AS latest_order_amount,
    avg_amount        AS average_order_amount
FROM ranked_orders
WHERE rn = 1                      -- only the latest order per customer
  AND order_amount > avg_amount   -- latest > average
ORDER BY customer_id;
```

1. Remove duplicate orders assuming:
- Duplicate = same `customer_id` and `order_amount`
- Keep only the **latest order**

```sql
WITH ranked AS (
    SELECT 
        *,
        ROW_NUMBER() OVER (
            PARTITION BY customer_id, order_amount 
            ORDER BY order_id DESC
        ) AS rn
    FROM orders
)
SELECT 
    order_id,
    customer_id,
    order_amount
FROM ranked
WHERE rn = 1
ORDER BY order_id;
```

1. **(Advanced Logic - Exclusive Behavior)**
Write a query to find customers who have streamed on 'Mobile' devices but have **never** streamed on 'TV'. Show the `customer_id`.

- We start with customers who **have at least one Mobile stream**.
- Then we use `NOT EXISTS` to ensure they **have zero TV streams**.
- `DISTINCT` removes duplicates since a customer might have multiple Mobile streams.

```sql
SELECT DISTINCT s.customer_id
FROM Streams s
WHERE s.device_type = 'Mobile'
  AND NOT EXISTS (
        SELECT 1
        FROM Streams t
        WHERE t.customer_id = s.customer_id
          AND t.device_type = 'TV'
    );
```

1. **(Calculations - Ratios/Percentages)**
Write a query to calculate the "Churn Rate" for the 'Premium' plan. The churn rate is defined as: *(Number of Cancelled Premium Subs / Total Premium Subs) * 100*. Return the result as a percentage.

```sql
SELECT 
    ( 
        SUM(CASE WHEN status = 'Cancelled' THEN 1 ELSE 0 END) * 100.0
        / COUNT(*)
    ) AS premium_churn_rate
FROM Subscriptions
WHERE plan = 'Premium';
```

- We filter only **Premium** subscriptions.
- `SUM(CASE WHEN status = 'Cancelled' THEN 1 ELSE 0 END)`
    
    → counts how many Premium subscriptions were cancelled.
    
- `COUNT(*)`
    
    → total number of Premium subscriptions.
    
- Divide cancelled / total, then multiply by **100** to get a percentage.
- Cast to `decimal` to avoid integer division (PostgreSQL style).
1. **(Window Functions - Running Total)**
Write a query to calculate the **running balance** for *each* account. The output should show `account_id`, `trans_date`, `amount`, `type`, and a new column `running_total` that sums the amounts cumulatively (ordered by date) for that specific account. (Assume 'Debit' amounts are positive numbers in the table, but logically they deduct money. For this specific question, just sum the `amount` column directly as if all are positive additions, to keep it simple).

```sql
SELECT
    account_id,
    trans_date,
    amount,
    type,
    SUM(amount) OVER (
        PARTITION BY account_id
        ORDER BY trans_date
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
    ) AS running_total
FROM transactions;

```

- `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` → sums all rows from first up to current.
- We simply sum the raw amount as required.

1. **(Window Functions - Percent of Total)**
Write a query to calculate what percentage of an account's *total transaction volume* each specific transaction represents.
Output: `account_id`, `trans_id`, `amount`, and `percentage_of_total` (formatted to 1 or 2 decimal places if possible).
*Formula: (Transaction Amount / Sum of All Transaction Amounts for that Account) * 100.*

```sql
SELECT
    account_id,
    trans_id,
    amount,
    ROUND(
        amount * 100.0 / SUM(amount) OVER (PARTITION BY account_id),
        2
    ) AS percentage_of_total
FROM transactions;

```

- `SUM(amount) OVER (PARTITION BY account_id)` → total volume per account.
- We divide each transaction by this total.
- `ROUND(..., 2)` → gives a clean 2-decimal output.

1. **(Date Math & Window Functions)**
Write a query to find the number of **days elapsed** since the *previous* transaction for each account.
Output: `account_id`, `trans_date`, and `days_since_last_trans`. (For the first transaction of an account, this value should be NULL or 0).

```sql
SELECT
    account_id,
    trans_date,
    trans_date 
      - LAG(trans_date) OVER (PARTITION BY account_id ORDER BY trans_date)
        AS days_since_last_trans
FROM transactions;

```

1. **(Advanced Filtering - "Super Users")**
Write a query to find the `account_id` of accounts that have **only** 'Credit' transactions and **no** 'Debit' transactions.

```sql
SELECT account_id
FROM transactions
GROUP BY account_id
HAVING SUM(CASE WHEN type = 'Debit' THEN 1 ELSE 0 END) = 0;

```

```sql
SELECT DISTINCT account_id
FROM transactions
WHERE account_id NOT IN (
    SELECT account_id FROM transactions WHERE type = 'Debit'
);

```

1. **(Ranking & Filtering)**
Write a query to find specifically the **second most recent** transaction for *each* account.
Output: `account_id`, `trans_date`, `amount`.

```sql
WITH ranked AS (
    SELECT
        account_id,
        trans_date,
        amount,
        ROW_NUMBER() OVER (
            PARTITION BY account_id
            ORDER BY trans_date DESC
        ) AS rn
    FROM transactions
)
SELECT
    account_id,
    trans_date,
    amount
FROM ranked
WHERE rn = 2;

```

## Question

Find customers who:

- Have placed **more than one completed order**
- And whose **latest completed order** happened **at least 30 days after their first completed order**

Return:

- `customer_id`

```sql
WITH completed_orders AS (
    SELECT 
        customer_id,
        order_id,
        order_date
    FROM orders
    WHERE status = 'completed'
),
customer_dates AS (
    SELECT 
        customer_id,
        MIN(order_date) AS first_order_date,
        MAX(order_date) AS latest_order_date,
        COUNT(*) AS order_count
    FROM completed_orders
    GROUP BY customer_id
)
SELECT 
    customer_id
FROM customer_dates
WHERE order_count > 1
  AND latest_order_date >= first_order_date + INTERVAL '30 days'
ORDER BY customer_id;
```

## Alternative: Pure Window Function Approach (No GROUP BY)

```sql
WITH completed_with_rn AS (
    SELECT 
        customer_id,
        order_date,
        ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date) AS rn_asc,
        ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date DESC) AS rn_desc,
        COUNT(*) OVER (PARTITION BY customer_id) AS total_completed_orders
    FROM orders
    WHERE status = 'completed'
),
first_and_latest AS (
    SELECT DISTINCT
        customer_id,
        total_completed_orders,
        FIRST_VALUE(order_date) OVER (PARTITION BY customer_id ORDER BY order_date 
                                      ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS first_order_date,
        FIRST_VALUE(order_date) OVER (PARTITION BY customer_id ORDER BY order_date DESC 
                                      ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS latest_order_date
    FROM completed_with_rn
)
SELECT 
    customer_id
FROM first_and_latest
WHERE total_completed_orders > 1
  AND latest_order_date >= first_order_date + INTERVAL '30 days'
ORDER BY customer_id;
```