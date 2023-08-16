# Inner Join vs Subquery using IN

NOTE: Using Inner_Join is more optimized and readable than using subquery using IN operator


# LEFT Join:

*** Can we solve INNER join question using LEFT join? 

Let's say we have two different tables each with 3 cols and 3 rows. When we perform Inner join then the resultant table is going to contain those rows from BOTH tables that matches the condition. 
But when left join is performed (select * from table1 left join table2 where condition) then the resulting table will look like this -
A resulting table (which can be divided into table1 and table2) where all the columns, rows of table1 is not null or present but for table2 values of only those rows and columns will be not null which falls under the matching condition else those values will be null. For eg - if t1_id matches with t2_id then we will have 3 not null rows and cols of table1 followed by 3 not null rows and cols of table2. But if no match then we will have 3 not null rows and cols of table1 followed by 3 null rows and cols of table2 (since table1 is used first during left join opertaion => it will always be not null)

But since LEFT Join populates null result of 2nd table also, we need to add additional condition 'WHERE country.code IS NOT NULL' so that those rows will be filtered out and sum(popluation) will be calculated, else additional population will be summed for those whose country table values are NULL.



# COUNT(): 

*** How to use count() function as condition:
-->We cannot use count() function in 'where' clause, instead we need to use 'having' clause. count() can be used with ORDER BY clause.
Hackerrank (basic joins) Question: Top Competitors

*** Why this error occurs? 
"ERROR 1055 (42000) at line 1: Expression #1 of SELECT list is not in GROUP BY clause and contains nonaggregated column 'country.name' which is not functionally dependent on columns in GROUP BY clause; this is incompatible with sql_mode=only_full_group_by"

This error occurs when we use group by in query and then try to output some data which has been grouped by and does not hold individual significance. For example - If we group first_name from persons table based on 'first_letter' of first_name then we can print 'first_letter' but we cannot print first_name
In the below query we can successfully query country.continent but we cannot query country.name and it will result in above sql error.
Query- select country.continent, floor(avg(city.population)) from city inner join country on city.countrycode = country.code group by country.continent; [PASS]
Query- select country.name, country.continent, floor(avg(city.population)) from city inner join country on city.countrycode = country.code group by country.continent; [FAIL]


# GROUP BY: 

*** How to select/print multiple columns when group by is used for a column.
--> add those colum also in group by clause
{
select col1, col2 from table group by col1;                    [FAIL]
select col1, col2 from table group by col1, col2;               [PASS]
}


