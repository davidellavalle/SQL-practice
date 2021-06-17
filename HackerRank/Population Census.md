Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.  

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.  

**nput Format**  

![alt text](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

The CITY and COUNTRY tables are described as follows: 

![alt text](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg)


**Solution:**
````sql
select sum(city.population) from city inner join country on CITY.CountryCode = COUNTRY.Code where country.continent = "Asia";
````
