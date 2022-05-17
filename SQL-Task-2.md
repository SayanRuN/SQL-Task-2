Задача №1

_Создание таблицы_
```
 CREATE TABLE Departments (
   Code INTEGER PRIMARY KEY NOT NULL,
   Name NVARCHAR NOT NULL ,
   Budget REAL NOT NULL 
 );
 
 CREATE TABLE Employees (
   SSN INTEGER PRIMARY KEY NOT NULL,
   Name TEXT NOT NULL ,
   LastName VARCHAR NOT NULL ,--since question 2 asks about removing duplicate - text must be converted if the answer is using distinct
   Department INTEGER NOT NULL , 
   CONSTRAINT fk_Departments_Code FOREIGN KEY(Department) 
   REFERENCES Departments(Code)
 );
```
***

_Внесение значений_
```
INSERT INTO Departments(Code,Name,Budget) VALUES(14,'IT',65000);
INSERT INTO Departments(Code,Name,Budget) VALUES(37,'Accounting',15000);
INSERT INTO Departments(Code,Name,Budget) VALUES(59,'Human Resources',240000);
INSERT INTO Departments(Code,Name,Budget) VALUES(77,'Research',55000);

INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('123234877','Michael','Rogers',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('152934485','Anand','Manikutty',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('222364883','Carol','Smith',37);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('326587417','Joe','Stevens',37);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('332154719','Mary-Anne','Foster',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('332569843','George','O''Donnell',77);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('546523478','John','Doe',59);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('631231482','David','Smith',77);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('654873219','Zacary','Efron',59);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('745685214','Eric','Goldsmith',59);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('845657245','Elizabeth','Doe',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('845657246','Kumar','Swamy',14);
```
***

_Задачи_

1. Select the last name of all employees.
2. Select the last name of all employees, without duplicates.
3. Select all the data of employees whose last name is "Smith".
4. Select all the data of employees whose last name is "Smith" or "Doe".
5. Select all the data of employees that work in department 14.
6. Select all the data of employees that work in department 37 or department 77.
7. Select all the data of employees whose last name begins with an "S".
8. Select the sum of all the departments' budgets.
9. Select the number of employees in each department (you only need to show the department code and the number of employees).
10. Select all the data of employees, including each employee's department's data.
11. Select the name and last name of each employee, along with the name and budget of the employee's department.
12. Select the name and last name of employees working for departments with a budget greater than $60,000.
13. Select the departments with a budget larger than the average budget of all the departments.
14. Select the names of departments with more than two employees.
15. Select the name and last name of employees working for departments with second lowest budget.
16. Add a new department called "Quality Assurance", with a budget of $40,000 and departmental code 11. Add an employee called "Mary Moore" in that department, with SSN 847-21-9811.
17. Reduce the budget of all departments by 10%.
18. Reassign all employees from the Research department (code 77) to the IT department (code 14).
19. Delete from the table all employees in the IT department (code 14).
20. Delete from the table all employees who work in departments with a budget greater than or equal to $60,000.
21. Delete from the table all employees.
***

_Решение_
```
SELECT LastName FROm Employees;

SELECT DISTINCT LastName FROm Employees;

SELECT * FROM Employees
WHERE LastName='Smith';

SELECT * FROM Employees
WHERE LastName='Smith' OR LastName='Doe';

SELECT * FROM Employees
WHERE Department=14;

SELECT * FROM Employees
WHERE Department=37 OR Department=77;

SELECT * FROM Employees
WHERE LastName LIKE 'S%';

SELECT Budget FROM Departments;

SELECT count(e.Department), d.code FROM Employees e, Departments d
WHERE d.code=e.Department
GROUP BY d.code;

SELECT * FROM Departments, Employees
WHERE Employees.Department=Departments.Code;
SELECT e.Name,LastName, d.name, Budget FROM Departments d, Employees e
WHERE d.code=e.Department;

SELECT Employees.Name, lastname,Budget FROM Employees
INNER JOIN Departments
ON Employees.Department = Departments.Code
WHERE Budget>60000;

SELECT * FROM Departments
WHERE Budget >(SELECT AVG(Budget) FROM Departments);

SELECT d.name FROM Departments d
INNER JOIN Employees e
ON d.Code = e.Department
GROUP BY d.name
HAVING count(e.Department)>2;

INSERT INTO Departments (Code, Name, Budget) VALUES (11, 'Quality Assurance', 40000);

INSERT INTO Employees (SSN, Name, LastName, Department) VALUES (847-21-9811, 'Mary', 'Moore', 11);

UPDATE Departments SET budget=budget-(budget*0.1);

UPDATE Employees SET departme
nt=14
WHERE department=77;
DELETE FROM Employees
WHERE department=14;

DELETE FROM Employees
WHERE Department IN(
SELECT Code FROM Departments
WHERE Budget >= 60000);
```
---
---

Задача № 2

_Создание таблицы_
```
 CREATE TABLE Warehouses (
   Code INTEGER PRIMARY KEY NOT NULL,
   Location TEXT NOT NULL ,
   Capacity INTEGER NOT NULL 
 );
 
 CREATE TABLE Boxes (
   Code TEXT PRIMARY KEY NOT NULL,
   Contents TEXT NOT NULL ,
   Value REAL NOT NULL ,
   Warehouse INTEGER NOT NULL, 
   CONSTRAINT fk_Warehouses_Code FOREIGN KEY (Warehouse) REFERENCES Warehouses(Code)
 );
```
***

_Внесение значений_
```
 INSERT INTO Warehouses(Code,Location,Capacity) VALUES(1,'Chicago',3);
 INSERT INTO Warehouses(Code,Location,Capacity) VALUES(2,'Chicago',4);
 INSERT INTO Warehouses(Code,Location,Capacity) VALUES(3,'New York',7);
 INSERT INTO Warehouses(Code,Location,Capacity) VALUES(4,'Los Angeles',2);
 INSERT INTO Warehouses(Code,Location,Capacity) VALUES(5,'San Francisco',8);
 
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES('0MN7','Rocks',180,3);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES('4H8P','Rocks',250,1);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES('4RT3','Scissors',190,4);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES('7G3H','Rocks',200,1);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES('8JN6','Papers',75,1);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES('8Y6U','Papers',50,3);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES('9J6F','Papers',175,2);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES('LL08','Rocks',140,4);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES('P0H6','Scissors',125,1);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES('P2T6','Scissors',150,2);
 INSERT INTO Boxes(Code,Contents,Value,Warehouse) VALUES('TU55','Papers',90,5);
```
***

_Задачи_

1. Select all warehouses.
2. Select all boxes with a value larger than $150.
3. Select all distinct contents in all the boxes.
4. Select the average value of all the boxes.
5. Select the warehouse code and the average value of the boxes in each warehouse.
6. Same as previous exercise, but select only those warehouses where the average value of the boxes is greater than 150.
7. Select the code of each box, along with the name of the city the box is located in.
8. Select the warehouse codes, along with the number of boxes in each warehouse. Optionally, take into account that some warehouses are empty (i.e., the box count should show up as zero, instead of omitting the warehouse from the result).
9. Select the codes of all warehouses that are saturated (a warehouse is saturated if the number of boxes in it is larger than the warehouse's capacity).
10. Select the codes of all the boxes located in Chicago.
11. Create a new warehouse in New York with a capacity for 3 boxes.
12. Create a new box, with code "H5RT", containing "Papers" with a value of $200, and located in warehouse 2.
13. Reduce the value of all boxes by 15%.
14. Apply a 20% value reduction to boxes with a value larger than the average value of all the boxes.
15. Remove all boxes with a value lower than $100.
16. Remove all boxes from saturated warehouses.
***

_Решение_
```
SELECT * FROM warehouses;

SELECT * FROM boxes
WHERE value>150;

SELECT DISTINCT contents FROM boxes;

SELECT avg(value) FROM boxes;

SELECT avg(value), warehouse FROM boxes
GROUP BY warehouse;

SELECT avg(value), warehouse FROM boxes
GROUP BY warehouse
HAVING avg(value)>150;

SELECT b.code, location FROM boxes b
INNER JOIN warehouses w
ON w.code = b.warehouse;

SELECT count(b.warehouse), w.code FROM boxes b
INNER JOIN warehouses w
ON w.code = b.warehouse
GROUP BY w.code;

SELECT count(b.warehouse), w.code FROM boxes b
INNER JOIN warehouses w
ON w.code = b.warehouse
GROUP BY w.code, capacity
HAVING count(b.warehouse)>capacity;


SELECT b.code, location FROM boxes b
INNER JOIN warehouses w
ON w.code = b.warehouse
WHERE w.location='Chicago';

INSERT INTO warehouses VALUES (6,  'New York', 3);

INSERT INTO boxes (code, contents, value, warehouse)
VALUES ('H5RT', 'Documents', 200, 2);

SELECT *, value-(value*15)/100 AS minus_15 FROM boxes;

SELECT value-(value*20)/100 AS minus_20,value, warehouse FROM boxes
WHERE value>152;

DELETE FROM boxes
WHERE value<100;
```
---
---

Задача № 3

_Создание таблицы_
```
CREATE TABLE Pieces (
   Code INTEGER PRIMARY KEY NOT NULL,
   Name TEXT NOT NULL
 );
 
 CREATE TABLE Providers (
  Code TEXT PRIMARY KEY NOT NULL,
  Name TEXT NOT NULL
 );
 
 CREATE TABLE Provides (
   Piece INTEGER  
     CONSTRAINT fk_Pieces_Code REFERENCES Pieces(Code),
   Provider TEXT
     CONSTRAINT fk_Providers_Code REFERENCES Providers(Code),
   Price INTEGER NOT NULL,
   PRIMARY KEY(Piece, Provider)
 );
```
***

_Внесение значений_
```
 INSERT INTO Providers(Code, Name) VALUES('HAL','Clarke Enterprises');
 INSERT INTO Providers(Code, Name) VALUES('RBT','Susan Calvin Corp.');
 INSERT INTO Providers(Code, Name) VALUES('TNBC','Skellington Supplies');
 
 INSERT INTO Pieces(Code, Name) VALUES(1,'Sprocket');
 INSERT INTO Pieces(Code, Name) VALUES(2,'Screw');
 INSERT INTO Pieces(Code, Name) VALUES(3,'Nut');
 INSERT INTO Pieces(Code, Name) VALUES(4,'Bolt');
 
 INSERT INTO Provides(Piece, Provider, Price) VALUES(1,'HAL',10);
 INSERT INTO Provides(Piece, Provider, Price) VALUES(1,'RBT',15);
 INSERT INTO Provides(Piece, Provider, Price) VALUES(2,'HAL',20);
 INSERT INTO Provides(Piece, Provider, Price) VALUES(2,'RBT',15);
 INSERT INTO Provides(Piece, Provider, Price) VALUES(2,'TNBC',14);
 INSERT INTO Provides(Piece, Provider, Price) VALUES(3,'RBT',50);
 INSERT INTO Provides(Piece, Provider, Price) VALUES(3,'TNBC',45);
 INSERT INTO Provides(Piece, Provider, Price) VALUES(4,'HAL',5);
 INSERT INTO Provides(Piece, Provider, Price) VALUES(4,'RBT',7);
```
***

_Задачи_

1. Select the name of all the pieces.
2. Select all the providers' data.
3. Obtain the average price of each piece (show only the piece code and the average price).
4. Obtain the names of all providers who supply piece 1.
5. Select the name of pieces provided by provider with code "HAL".
6. For each piece, find the most expensive offering of that piece and include the piece name, provider name, and price (note that there could be two providers who supply the same piece at the most expensive price).
7. Add an entry to the database to indicate that "Skellington Supplies" (code "TNBC") will provide sprockets (code "1") for 7 cents each.
8. Increase all prices by one cent.
9. Update the database to reflect that "Susan Calvin Corp." (code "RBT") will not supply bolts (code 4).
10. Update the database to reflect that "Susan Calvin Corp." (code "RBT") will not supply any pieces (the provider should still remain in the database).
***

_Решение_
```
SELECT * FROM pieces;

SELECT * FROM providers;

SELECT piece, avg(price) FROM provides
GROUP BY piece;
SELECT pp.name FROM provides p, providers pp
WHERE pp.code=p.provider AND p.piece=1;
SELECT name FROM pieces

INNER JOIN provides
ON pieces.code = provides.piece
WHERE provider='HAL';

SELECT ps.name, pr.name, pd.price FROM pieces ps, providers pr, provides pd
WHERE ps.code=pd.piece AND pr.code=pd.provider AND pd.price=(SELECT max(price) FROM provides WHERE ps.code=provides.piece);

INSERT INTO provides (piece, provider, price) VALUES (1, 'TNBC', 7);

UPDATE provides SET price=price+1;

DELETE FROM provides
WHERE piece=4 AND provider='RBT';

DELETE FROM provides
WHERE provider='RBT';
```