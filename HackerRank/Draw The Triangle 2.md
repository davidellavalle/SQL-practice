P(R) represents a pattern drawn by Julia in R rows. The following pattern represents P(5):

````
* 
* * 
* * * 
* * * * 
* * * * *
````
Write a query to print the pattern P(20).


**solution**
````sql
set @number = 0;
select repeat("* ", @number := @number+1) from information_schema.tables limit 20; 
````
here:  
**set @number = 0** declares and initialize a variable  

**@number := @number+1** where := is the assignment operator (= is instead the equality operator). Here the variable will increase by 1 infitively  

**limit 20** will arrest the increasing after 20 repeats  

**information_schema.tables** is a dummy table  
