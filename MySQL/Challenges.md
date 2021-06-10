Julia asked her students to create some coding challenges. Write a query to print the hacker_id, name, and the total number of challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one student created the same number of challenges, then sort the result by hacker_id. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.  

Input Format  

The following tables contain challenge data:  

![alt text](https://s3.amazonaws.com/hr-challenge-images/19506/1458521004-cb4c077dd3-ScreenShot2016-03-21at6.06.54AM.png)

Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker.   

Challenges: The challenge_id is the id of the challenge, and hacker_id is the id of the student who created the challenge.   

![alt text](https://s3.amazonaws.com/hr-challenge-images/19506/1458521079-549341d9ec-ScreenShot2016-03-21at6.07.03AM.png)  

Sample Input 0

Hackers Table:  
![alt text](https://s3.amazonaws.com/hr-challenge-images/19506/1458521384-34c6866dae-ScreenShot2016-03-21at6.07.15AM.png)

Challenges Table: 
![alt text](https://s3.amazonaws.com/hr-challenge-images/19506/1458521410-befa8e1cd9-ScreenShot2016-03-21at6.07.25AM.png)

Sample Output 0  

21283 Angela 6  
88255 Patrick 5  
96196 Lisa 1  
Sample Input 1  

Hackers Table:  
![alt text](https://s3.amazonaws.com/hr-challenge-images/19506/1458521469-87036deea3-ScreenShot2016-03-21at6.07.48AM.png)
Challenges Table: 
![alt text](https://s3.amazonaws.com/hr-challenge-images/19506/1458521490-358215cf0b-ScreenShot2016-03-21at6.07.58AM.png)
Sample Output 1  

12299 Rose 6  
34856 Angela 6  
79345 Frank 4  
80491 Patrick 3  
81041 Lisa 1  
Explanation  

For Sample Case 0, we can get the following details:   
![alt text](https://s3.amazonaws.com/hr-challenge-images/19506/1458521677-fd04c384c0-ScreenShot2016-03-21at6.07.38AM.png)  

Students  and  both created  challenges, but the maximum number of challenges created is  so these students are excluded from the result.  

For Sample Case 1, we can get the following details:  
![alt text](https://s3.amazonaws.com/hr-challenge-images/19506/1458521836-24039e7523-ScreenShot2016-03-21at6.08.08AM.png)  
Students  and  both created  challenges. Because  is the maximum number of challenges created, these students are included in the result.  

**SOLUTION**  
to run this solution we should change sql mode to only_full_group_by
````sql
select t.hacker_id, t.name, t.total from (select h.hacker_id, h.name, count(c.challenge_id) as total 
from hackers as h inner join challenges as c on h.hacker_id = c.hacker_id group by h.hacker_id, h.name) 
as t group by total having count(total)=1 or count(total) = max(total
````
otherwise
`````sql
select h.hacker_id, h.name, count(c.challenge_id) as total from hackers as h 
inner join challenges as c on h.hacker_id = c.hacker_id group by h.hacker_id 
having total = (select count(c1.challenge_id) from challenges as c1 
group by c1.hacker_id order by count(*) desc limit 1) 
or total not in (select count(c2.challenge_id) from challenges as c2 
group by c2.hacker_id having c2.hacker_id<> h.hacker_id)
order by total desc, hacker_id;
````
or
````sql
select h.hacker_id, h.name, count(c.challenge_id) as total 
from hackers as h inner join challenges as c on h.hacker_id = c.hacker_id group by h.hacker_id,h.name
having total = 
(select count(c1.challenge_id) from challenges as c1 group by c1.hacker_id 
order by count(c1.challenge_id) desc limit 1) or 
total in 
(select t.cnt from (select count(c2.challenge_id) as cnt from  challenges as c2 
group by c2.hacker_id) as t group by t.cnt having count(t.cnt)=1)
order by total desc, h.hacker_id;
````
