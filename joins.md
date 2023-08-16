# Inner Join vs Subquery using IN

Question(1):
Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'. CITY.CountryCode and COUNTRY.Code are matching key columns.

Query using IN operator:
select sum(city.population) from city where city.countrycode IN (select country.code from country where country.continent = 'Asia');

Query using Inner Join
select sum(city.population) from city, country where city.countrycode = country.code and country.continent = ‘Asia’;

NOTE: Using Inner_Join is more optimized and readable than using subquery using IN operator

# Understanding LEFT Join:

Let's say we have two different tables each with 3 cols and 3 rows. When left join is performed (select * from table1 left join table2 where condition) then the resulting table will look like this -
A resulting table which can be divided into table1 and table2 where all the columns, rows of table1 is not null or present but for table2 only those rows and columns will be not null which falls under the matching condition else those values will be null. For eg - if t1_id matches with t2_id then we will have 3 not null rows and cols of table1 followed by 3 not null rows and cols of table2. But if no match then we will have 3 not null rows and cols of table1 followed by 3 null rows and cols of table2 (since table1 is used first during left join opertaion => it will always be not null)

NOTE: Question(1) can be solved using left join: 
SELECT SUM(city.population) 
FROM city
LEFT JOIN country ON city.countrycode = country.code AND country.continent = 'Asia'
WHERE country.code IS NOT NULL

But since LEFT Join populates null result of 2nd table also, we need to add additional condition 'WHERE country.code IS NOT NULL' so that those rows will be filtered out and sum(popluation) will be calculated, else additional population will be summed for those whose country table values are NULL.



