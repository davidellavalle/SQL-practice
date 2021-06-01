**TOP COMPETITORS**

Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! 
Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. 
Order your output in descending order by the total number of challenges in which the hacker earned a full score. 
If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.

Input Format

 ![alt text](https://s3.amazonaws.com/hr-challenge-images/19504/1458526776-67667350b4-ScreenShot2016-03-21at7.45.59AM.png)
Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker
 ![alt text](https://s3.amazonaws.com/hr-challenge-images/19504/1458526915-57eb75d9a2-ScreenShot2016-03-21at7.46.09AM.png)
Difficulty: The difficult_level is the level of difficulty of the challenge, and score is the score of the challenge for the difficulty level.
![alt text](https://s3.amazonaws.com/hr-challenge-images/19504/1458527032-f9ca650442-ScreenShot2016-03-21at7.46.17AM.png)
Challenges: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge, and difficulty_level is the level of difficulty of the challenge. 
![alt text](https://s3.amazonaws.com/hr-challenge-images/19504/1458527077-298f8e922a-ScreenShot2016-03-21at7.46.29AM.png)
Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge that the submission belongs to, and score is the score of the submission.

````sql
insert into @Hackers Values (5580, 'Rose'), (8439,'Angela'),(27205,'Frank'),(52243,'Patrick'),(52348,'Lisa'),(57645,'Kimberly'),(77726,'Bonnie'),(83082,'Michael'),(86870,'Todd'),(90411,'Joe')
insert into @Difficulty values (1,20),(2,30),(3,40),(4,60),(5,80),(6,100),(7,120)
insert into @Challenges Values (4810,77726,4),(21089,27205,1),(36566,5580,7),(66730,52243,6),(71055,52243,2)
insert into @Submissions Values (68628,77726,36566,30),(65300,77726,21089,10),(40326,52243,36566,77),(8941,27205,4810,4),(83554,77726,66730,30),(43353,52243,66730,0),(55385,52348,71055,20),(39784,27205,71055,23),(94613,86870,71055,30),(45788,52348,36566,0),(93058,86870,36566,30),(7344,8439,66730,92),(2721,8439,4810,36),(523,5580,71055,4),(49105,52348,66730,0),(55877,57645,66730,80),(38355,27205,66730,35),(3924,8439,36566,80),(97397,90411,66730,100),(84162,83082,4810,40),(97431,90411,71055,30)
````


**Solution:**  
````sql
select h.hacker_id, h.name  
from Submissions as s   
inner join Challenges as c on s.challenge_id = c.challenge_id   
inner join Difficulty as d on c.difficulty_level = d.difficulty_level   
inner join Hackers as h on s.hacker_id = h.hacker_id where s.score = d.score   
group by h.hacker_id, h.name   
having count(*)>1   
order by count(*) desc, h.hacker_id;
````
