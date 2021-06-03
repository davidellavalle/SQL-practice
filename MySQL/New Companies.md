Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy:  
![alt text](https://s3.amazonaws.com/hr-challenge-images/19505/1458531031-249df3ae87-ScreenShot2016-03-21at8.59.56AM.png)

Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code.  

Note:  
- The tables may contain duplicate records.
- The company_code is string, so the sorting should not be numeric. For example, if the company_codes are C_1, C_2, and C_10, then the ascending company_codes will be C_1, C_10, and C_2.  

**Input Format** 
The following tables contain company data:
- Company: The company_code is the code of the company and founder is the founder of the company.
![alt text](https://s3.amazonaws.com/hr-challenge-images/19505/1458531125-deb0a57ae1-ScreenShot2016-03-21at8.50.04AM.png)  
- Lead_Manager: The lead_manager_code is the code of the lead manager, and the company_code is the code of the working company.  
![alt text](https://s3.amazonaws.com/hr-challenge-images/19505/1458534960-2c6d764e3c-ScreenShot2016-03-21at8.50.12AM.png)  
- Senior_Manager: The senior_manager_code is the code of the senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.  
![alt text](https://s3.amazonaws.com/hr-challenge-images/19505/1458534973-6548194998-ScreenShot2016-03-21at8.50.21AM.png)
-Manager: The manager_code is the code of the manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.
![alt text](https://s3.amazonaws.com/hr-challenge-images/19505/1458534988-7fc0af46ce-ScreenShot2016-03-21at8.50.29AM.png)
Employee: The employee_code is the code of the employee, the manager_code is the code of its manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.
![alt text](https://s3.amazonaws.com/hr-challenge-images/19505/1458535002-d47f63cbb4-ScreenShot2016-03-21at8.50.41AM.png)

**Sample Input**  
Company Table:  
![alt text](https://s3.amazonaws.com/hr-challenge-images/19505/1458535049-2a207c44b3-ScreenShot2016-03-21at8.50.52AM.png)  
Lead_Manager Table:  
![alt text](https://s3.amazonaws.com/hr-challenge-images/19505/1458535073-919107f639-ScreenShot2016-03-21at8.51.03AM.png)  
Senior_Manager Table:   
![alt text](https://s3.amazonaws.com/hr-challenge-images/19505/1458535111-b1c48335b3-ScreenShot2016-03-21at8.51.15AM.png)  
Manager Table:  
![alt text](https://s3.amazonaws.com/hr-challenge-images/19505/1458535122-888f4bf340-ScreenShot2016-03-21at8.51.26AM.png)  
Employee Table:  
![alt text](https://s3.amazonaws.com/hr-challenge-images/19505/1458535134-878767e0d9-ScreenShot2016-03-21at8.51.52AM.png)  

**Sample Output**  

C1 Monika 1 2 1 2  
C2 Samantha 1 1 2 2  

**Explanation**  

In company C1, the only lead manager is LM1. There are two senior managers, SM1 and SM2, under LM1. There is one manager, M1, under senior manager SM1. There are two employees, E1 and E2, under manager M1.  
In company C2, the only lead manager is LM2. There is one senior manager, SM3, under LM2. There are two managers, M2 and M3, under senior manager SM3. There is one employee, E3, under manager M2, and another employee, E4, under manager, M3.  

**Solution:**  
1st and longer using inner join
````sql
select d.company_code, d.founder, count(distinct d.lead_manager_code), count(distinct d.senior_manager_code),
count(distinct d.manager_code),count(distinct d.employee_code) from
(select y.company_code, y.founder, y.lead_manager_code,y.senior_manager_code, y.manager_code, employee_code from
(select x.company_code, x.founder, x.lead_manager_code,x.senior_manager_code, manager_code
 from (select t.company_code, t.founder, t.lead_manager_code,senior_manager_code 
from(select c.company_code, founder, lead_manager_code from company c inner join lead_manager lm 
on c.company_code = lm.company_code) as t inner join senior_manager as sm on t.company_code=sm.company_code) as x
inner join manager as m on x.company_code = m.company_code) as y inner join employee e 
on y.company_code=e.company_code) as d group by d.company_code order by d.company_code;
````
2nd and shorter without join but using where statement to join the tables on primary key company_code
````sql
select c.company_code, c.founder, count(distinct l.lead_manager_code), count(distinct s.senior_manager_code),
count(distinct s.senior_manager_code), count(distinct m.manager_code), count(distinct e.employee_code)
from company c, lead_manager l, senior_manager s, manager m, employee e where c.company_code=l.company_code 
and l.company_code=s.company_code and s.company_code = m.company_code and m.company_code=e.company_code 
group by c.company_code, c.founder order by c.company_code;
````
note: without group by we would reach just 1 result

