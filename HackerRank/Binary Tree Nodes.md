You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.  

![alt text](https://s3.amazonaws.com/hr-challenge-images/12888/1443818507-5095ab9853-1.png)

Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:  

Root: If node is root node.  
Leaf: If node is leaf node.  
Inner: If node is neither root nor leaf node.  
**Sample Input**

![alt text](https://s3.amazonaws.com/hr-challenge-images/12888/1443818467-30644673f6-2.png)

**Sample Output**

1 Leaf  
2 Inner  
3 Leaf  
5 Root  
6 Leaf  
8 Inner  
9 Leaf  

Explanation

The Binary Tree below illustrates the sample:
![alt text](https://s3.amazonaws.com/hr-challenge-images/12888/1443773633-f9e6fd314e-simply_sql_bst.png)

**Solution with table created for MySQL**
````sql
create table tree(N int,P int);
insert into tree values(1,2),(3,2),(6,8),(9,8),(2,5),(8,5),(5,null);

select N, case 
when P is null then "Root" 
when N in(select P from BST) then "Inner" 
else "Leaf" 
end as node 
from BST
order by N;
````

**Link**
https://www.hackerrank.com/challenges/binary-search-tree-1/problem
