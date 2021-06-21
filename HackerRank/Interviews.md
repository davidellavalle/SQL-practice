Samantha interviews many candidates from different colleges using coding challenges and contests. Write a query to print the contest_id, hacker_id, name, and the sums of total_submissions, total_accepted_submissions, total_views, and total_unique_views for each contest sorted by contest_id. Exclude the contest from the result if all four sums are 0.  

Note: A specific contest can be used to screen candidates at more than one college, but each college only holds 1 screening contest.  

**Input Format**  

The following tables hold interview data:  

Contests: The contest_id is the id of the contest, hacker_id is the id of the hacker who created the contest, and name is the name of the hacker.  
![image](https://user-images.githubusercontent.com/73824871/122764890-3a523b00-d2a0-11eb-846e-170992459a1c.png)

Colleges: The college_id is the id of the college, and contest_id is the id of the contest that Samantha used to screen the candidates.  
![image](https://user-images.githubusercontent.com/73824871/122764918-40e0b280-d2a0-11eb-861b-a9786d569ec8.png)

Challenges: The challenge_id is the id of the challenge that belongs to one of the contests whose contest_id Samantha forgot, and college_id is the id of the college where the challenge was given to candidates.   
![image](https://user-images.githubusercontent.com/73824871/122764940-476f2a00-d2a0-11eb-8602-06047ea5a109.png)

View_Stats: The challenge_id is the id of the challenge, total_views is the number of times the challenge was viewed by candidates, and total_unique_views is the number of times the challenge was viewed by unique candidates. 
![image](https://user-images.githubusercontent.com/73824871/122764960-4dfda180-d2a0-11eb-8307-7f1f88482a9c.png)

Submission_Stats: The challenge_id is the id of the challenge, total_submissions is the number of submissions for the challenge, and total_accepted_submission is the number of submissions that achieved full scores.   
![image](https://user-images.githubusercontent.com/73824871/122764994-55bd4600-d2a0-11eb-9736-16b8b7d736ba.png)

**Sample Input**  

Contests Table:![image](https://user-images.githubusercontent.com/73824871/122765021-5a81fa00-d2a0-11eb-91aa-f23ac57682a3.png)  
  Colleges Table:![image](https://user-images.githubusercontent.com/73824871/122765031-5e158100-d2a0-11eb-98bd-3908f7289997.png)  
  Challenges Table: ![image](https://user-images.githubusercontent.com/73824871/122765053-64a3f880-d2a0-11eb-81da-47fb6014bb13.png)  
 View_Stats Table:![image](https://user-images.githubusercontent.com/73824871/122765073-68d01600-d2a0-11eb-915a-f0d14c09f6f9.png)  
  Submission_Stats Table: ![image](https://user-images.githubusercontent.com/73824871/122765092-6e2d6080-d2a0-11eb-923d-7f78c36399b4.png)  


**Sample Output**  

66406 17973 Rose 111 39 156 56  
66556 79153 Angela 0 0 11 10  
94828 80275 Frank 150 38 41 15  
Explanation  

The contest 66406 is used in the college 11219. In this college 11219, challenges 18765 and 47127 are asked, so from the view and submission stats:  

Sum of total submissions 27 + 56 + 28 = 111  

Sum of total accepted submissions 10 + 18 + 11 = 39  

Sum of total views 43 + 72 + 26 + 15 = 156  

Sum of total unique views 10 + 13 + 19 + 14 = 56  

Similarly, we can find the sums for contests 66556 and 94828.


### SOLUTION

Create tables
````sql
CREATE TABLE CONTESTS (
    CONTEST_ID INT,
    HACKER_ID INT,
    NAME VARCHAR(200)
);

INSERT INTO CONTESTS VALUES (66406, 17973, 'ROSE'),(66556, 79153, 'ANGELA'),(94828, 80275, 'FRANK');

SELECT 
    *
FROM
    CONTESTS;

CREATE TABLE COLLEGES (
    COLLEGE_ID INT,
    CONTEST_ID INT
);

INSERT INTO COLLEGES VALUES (11219, 66406),(32473, 66556),(56685, 94828);

SELECT 
    *
FROM
    COLLEGES;

CREATE TABLE CHALLENGES (
    CHALLENGE_ID INT,
    COLLEGE_ID INT
);

INSERT INTO CHALLENGES VALUES (18765, 11219),(47127, 11219),(60292, 32473),(72974, 56685);

SELECT 
    *
FROM
    CHALLENGES;

CREATE TABLE VIEW_STATS (
    CHALLENGE_ID INT,
    TOTAL_VIEWS INT,
    TOTAL_UNIQUE_VIEWS INT
);

INSERT INTO VIEW_STATS VALUES (47127, 26, 19), (47127, 15, 14), (18765, 43, 10), (18765, 72, 13), (75516, 35, 17),(60292, 11, 10),(72974, 41, 15), (75516, 75, 11);

SELECT 
    *
FROM
    VIEW_STATS;

CREATE TABLE SUBMISSION_STATS (
    CHALLENGE_ID INT,
    TOTAL_SUBMISSIONS INT,
    TOTAL_ACCEPTED_SUBMISSIONS INT
);

INSERT INTO SUBMISSION_STATS  VALUES (75516, 34, 12), (47127, 27, 10),(47127, 56, 18), (75516, 74, 12),(75516, 83, 8),(72974, 68, 24),(72974, 82, 14),(47127, 28, 11);

SELECT 
    *
FROM
    SUBMISSION_STATS;
````
    
````
