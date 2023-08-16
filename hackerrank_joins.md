Question(1): Population Census
Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'. CITY.CountryCode and COUNTRY.Code are matching key columns.

Query- using IN operator:
select sum(city.population) from city where city.countrycode IN (select country.code from country where country.continent = 'Asia');

Query- using Inner Join:
select sum(city.population) from city, country where city.countrycode = country.code and country.continent = ‘Asia’;

Query- using Left Join:
SELECT SUM(city.population) FROM city LEFT JOIN country ON city.countrycode = country.code AND country.continent = 'Asia' WHERE country.code IS NOT NULL