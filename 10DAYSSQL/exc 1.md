![image](https://user-images.githubusercontent.com/73824871/122379844-8a12c880-cf67-11eb-82fd-8cab2c47fad9.png)

## Tables with data
````sql
CREATE TABLE Manufacturers (
    Code INT PRIMARY KEY,
    Name VARCHAR(255) NOT NULL
);

CREATE TABLE Products (
	Code INT PRIMARY KEY,  
    Name VARCHAR(255) NOT NULL ,  
    Price decimal NOT NULL ,  
    Manufacturer INTEGER NOT NULL,
    foreign key(manufacturer) REFERENCES Manufacturers(Code)
) ENGINE=INNODB;

INSERT INTO Manufacturers(Code,Name) VALUES(1,'Sony');
INSERT INTO Manufacturers(Code,Name) VALUES(2,'Creative Labs'),(3,'Hewlett-Packard'),(4,'Iomega'),(5,'Fujitsu'),(6,'Winchester');

INSERT INTO Products(Code,Name,Price,Manufacturer) VALUES(1,'Hard drive',240,5),(2,'Memory',120,6),(3,'ZIP drive',150,4),(4,'Floppy disk',5,6),(5,'Monitor',240,1),(6,'DVD drive',180,2),(7,'CD drive',90,2), (8,'Printer',270,3),(9,'Toner cartridge',66,3),(10,'DVD burner',180,2);
````

## QUESTIONS and SOLUTION

### 1.1 Select the name and price of all products with a price larger than or equal to $180, and sort first by price (in descending order), and then by name (in ascending order).
````sql
select name, Price from Products where Price>=180 order by price desc, name;
````

### 1.2 Select the average price of each manufacturer's products, showing only the manufacturer's code.
````sql
select manufacturer, avg(price) from products group by manufacturer;
````

### 1.3 Select the average price of each manufacturer's products, showing the manufacturer's name.
````sql
SELECT 
    manufacturer, m.name, AVG(price)
FROM
    products AS p
        INNER JOIN
    manufacturers AS m ON m.code = p.code
GROUP BY manufacturer;
````

### 1.4 Select the names of manufacturer whose products have an average price larger than or equal to $150.
````sql
SELECT 
    m.name, AVG(price) AS mean
FROM
    products AS p
        INNER JOIN
    manufacturers AS m ON m.code = p.code
GROUP BY manufacturer
HAVING mean >= 150;
````
### 1.5 Select the name and price of the cheapest product.
````sql
SELECT 
    name, min(price)
FROM
    products AS p;
````
### 1.6 Select the name of each manufacturer along with the name and price of its most expensive product.
````sql
SELECT 
    m.name, p.name, MAX(p.price)
FROM
    manufacturers AS m
        INNER JOIN
    products AS p ON m.code = p.code; 
````
### 1.7 Add a new product: Loudspeakers, $70, manufacturer 2.
````sql
insert into products values(11, "Loudspeakers", 70, 2);
````
### 1.8 Update the name of product 8 to "Laser Printer".
````sql
UPDATE products 
SET 
    name = 'Laser Printer'
WHERE
    code = 8;
````
### 1.9 Apply a 10% discount to all products.
````sql
SELECT 
    code, name, ROUND((price * 0.9), 1) AS discounted_pirce
FROM
    products;
````
### 1.10 Apply a 10% discount to all products with a price larger than or equal to $120.
````sql
SELECT 
    name, ROUND((price * 0.9), 1) AS discounted_pirce
FROM
    products
WHERE
    price >= 120;
````

#### **Excercise Source**: "https://github.com/shekharbiswas/10DAYSQL/tree/main/SQL_exercise_01"
