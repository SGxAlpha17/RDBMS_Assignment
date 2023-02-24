RDBMS Assignment

– question 1

Create a database named employee, then import data_science_team.csv proj_table.csv and emp_record_table.csv into the employee database from the given resources.




```

CREATE DATABASE employee;
USE employee;

CREATE TABLE Proj_table(
PROJECT_ID varchar(50),
PROJ_Name varchar(50),
DOMAIN varchar(50),
START_DATE date,
CLOSURE_DATE date,
DEV_QTR varchar(50),
STATUS varchar(50));

alter table proj_table
add primary key(PROJECT_ID);



CREATE TABLE emp_record_table(
EMP_ID varchar(50),
FIRST_NAME varchar(50),
LAST_NAME varchar(50),
GENDER varchar(50),
ROLE varchar(50),
DEPT varchar(50),
EXP varchar(50),
COUNTRY varchar(50),
CONTINENT varchar(50),
SALARY int,
EMP_RATING int,
MANAGER_ID varchar(50),
PROJ_ID varchar(50)
);


create table Data_science_team(
EMP_ID varchar(50),
FIRST_NAME varchar(50),
LAST_NAME varchar(50),
GENDER varchar(50),
ROLE varchar(50),
DEPT varchar(50),
EXP int,
COUNTRY varchar(50),
CONTINENT varchar(50)
);


alter table emp_record_table
add foreign key (PROJ_ID) references proj_table(PROJECT_ID);




```






















```
– question 2
Create an ER diagram for the given employee database.

```






![image](https://user-images.githubusercontent.com/123497764/221151370-44419fcd-cf61-4c62-9a43-b4b7ef595a9d.png)









```
--  QUESTION 3.
 Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, and DEPARTMENT from the employee record table, and make a list of employees and details of their department.

SELECT EMP_ID, FIRST_NAME,LAST_NAME,GENDER,DEPT DEPARTMENT
FROM EMP_RECORD_TABLE;

RESULT:
```

<img width="453" alt="Screenshot 2023-02-24 at 4 33 47 PM" src="https://user-images.githubusercontent.com/123497764/221163580-ade44955-4c96-4435-a68f-596b9c50e7c0.png">


```

--  QUESTION 4
4. Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPARTMENT,
and EMP_RATING if the EMP_RATING is:
● less than two
● greater than four
● between two and four



SELECT  EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT DEPARTMENT
FROM emp_record_table
 WHERE EMP_RATING <2;
 
 SELECT  EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT DEPARTMENT
FROM emp_record_table
 WHERE EMP_RATING >4;
 
 SELECT  EMP_ID, FIRST_NAME, LAST_NAME, GENDER, DEPT DEPARTMENT
FROM emp_record_table
 WHERE EMP_RATING BETWEEN 2 AND 4;
 
 RESULT:
 ```
 
 <img width="460" alt="Screenshot 2023-02-24 at 4 31 56 PM" src="https://user-images.githubusercontent.com/123497764/221163279-83bf4977-21c6-40a2-b200-7278c75dce03.png">

<img width="447" alt="Screenshot 2023-02-24 at 4 32 10 PM" src="https://user-images.githubusercontent.com/123497764/221163323-78015762-fd89-4e3b-82de-e803a4a9cbfc.png">
<img width="442" alt="Screenshot 2023-02-24 at 4 32 18 PM" src="https://user-images.githubusercontent.com/123497764/221163345-3d8f799f-deb0-40f9-945c-79db5761945a.png">

 
 
 
 
 ```
 -- QUESTION 5
Write a query to concatenate the FIRST_NAME and the LAST_NAME of employees in the Finance department from the employee table and then give the resultant column alias as NAME.
 
SELECT CONCAT(FIRST_NAME,LAST_NAME)
FROM EMP_RECORD_TABLE
WHERE DEPT='FINANCE';

RESULT:
```
<img width="437" alt="Screenshot 2023-02-24 at 4 27 54 PM" src="https://user-images.githubusercontent.com/123497764/221162380-9ec28978-44d0-4cba-ae09-d3445d1b1438.png">




```
-- QUESTION 6;
Write a query to list only those employees who have someone reporting to them. Also, show
the number of reporters (including the President);.

SELECT E1.EMP_ID,COUNT(E1.EMP_ID)
FROM EMP_RECORD_TABLE E1,EMP_RECORD_TABLE E2
WHERE E1.EMP_ID=E2.MANAGER_ID
GROUP BY E1.EMP_ID;

RESULT:
```
<img width="345" alt="Screenshot 2023-02-24 at 4 27 07 PM" src="https://user-images.githubusercontent.com/123497764/221162171-eeeeecec-c58a-451d-8b88-3deb3b632f81.png">




```
-- QUESTION 7
Write a query to list down all the employees from the healthcare and finance departments
using union. Take data from the employee record table.

SELECT * 
FROM EMP_RECORD_TABLE 
WHERE DEPT IN ('HEALTHCARE', 'FINANCE');

RESULT:
```

<img width="999" alt="Screenshot 2023-02-24 at 4 25 48 PM" src="https://user-images.githubusercontent.com/123497764/221161919-db98b683-853d-4aeb-8299-afb2ee916e0a.png">



```
-- QUESTION 8

8. Write a query to list down employee details such as EMP_ID, FIRST_NAME, LAST_NAME,
ROLE, DEPARTMENT, and EMP_RATING grouped by dept. Also include the respective
employee rating along with the max emp rating for the department.

SELECT EMP_ID,FIRST_NAME,LAST_NAME,ROLE,DEPT,EMP_RATING,
(SELECT MAX(EMP_RATING) FROM EMP_RECORD_TABLE WHERE DEPT=E1.DEPT)
 MAX_RATING
FROM EMP_RECORD_TABLE E1
ORDER BY DEPT;

Result:
```




<img width="725" alt="Screenshot 2023-02-24 at 4 22 25 PM" src="https://user-images.githubusercontent.com/123497764/221161527-2f5d3148-2293-4592-90de-da80bd9f1888.png">






```
-- QUESTION 9
Write a query to calculate the minimum and the maximum salary of the employees in each
role. Take data from the employee record table.

SELECT DEPT,MAX(SALARY),MIN(SALARY)
FROM EMP_RECORD_TABLE
GROUP BY DEPT;

Result:
```

<img width="456" alt="Screenshot 2023-02-24 at 4 01 13 PM" src="https://user-images.githubusercontent.com/123497764/221156797-8e073fd9-756e-4722-9a0b-5b7e080477e8.png">



```
-- QUESTION 10
Write a query to assign ranks to each employee based on their experience. Take data from
the employee record table.

SELECT EMP_ID, FIRST_NAME,LAST_NAME ,EXP
FROM EMP_RECORD_TABLE
ORDER BY EXP DESC;

Result:

```

<img width="448" alt="Screenshot 2023-02-24 at 3 59 43 PM" src="https://user-images.githubusercontent.com/123497764/221156489-7fb9293b-b040-4754-9f7c-92a698128d07.png">


```
– question 11
 Write a query to create a view that displays employees in various countries whose salary is more than six thousand. Take data from the employee record table.

CREATE VIEW rich_emp AS
SELECT emp_id,country,salary
FROM emp_record_table
WHERE salary>6000;
SELECT * FROM rich_emp;



result:

```

<img width="995" alt="Screenshot 2023-02-24 at 3 55 54 PM" src="https://user-images.githubusercontent.com/123497764/221155537-1a739d8a-3d9d-4e7a-8403-cd8c457ea039.png">





```

– question 12
Write a nested query to find employees with experience of more than ten years. Take data from the employee record table.


SELECT emp_id,exp 
FROM (SELECT *
	 FROM emp_record_table
     WHERE exp>10) e;

RESULT:
```
<img width="144" alt="Screenshot 2023-02-24 at 4 34 52 PM" src="https://user-images.githubusercontent.com/123497764/221163829-9c91e0dc-ba67-4d58-af70-de04eba13b38.png">

```

     
– Question 13
Write a query to create a stored procedure to retrieve the details of the employees whose experience is more than three years. Take data from the employee record table.

DELIMITER $$
CREATE PROCEDURE procedure1()
BEGIN 
SELECT * 
FROM emp_record_table
WHERE exp>3;
END $$ DELIMITER ;

call procedure1();

RESULT:
```

<img width="997" alt="Screenshot 2023-02-24 at 4 36 00 PM" src="https://user-images.githubusercontent.com/123497764/221164033-6aa6ba0a-e85a-4b52-8ba4-20a85548d72b.png">






```
– question 14
Write a query using stored functions in the project table to check whether the job profile assigned to each employee in the data science team matches the organization’s set standard.

The standard being: 
For an employee with experience less than or equal to 2 years assign 'JUNIOR DATA SCIENTIST', For an employee with the experience of 2 to 5 years assign 'ASSOCIATE DATA SCIENTIST', For an employee with the experience of 5 to 10 years assign 'SENIOR DATA SCIENTIST', For an employee with the experience of 10 to 12 years assign 'LEAD DATA SCIENTIST', For an employee with the experience of 12 to 16 years assign 'MANAGER'.



DELIMITER $$
CREATE FUNCTION ROLE_CHECKER(
v_empid int) RETURNS BOOLEAN DETERMINISTIC

BEGIN

declare p_exp int;
declare p_role varchar(30);

SELECT exp,role INTO p_exp, p_role
FROM data_science_team
WHERE emp_id=v_empid;


IF (p_exp<=2 AND p_role='JUNIOR DATA SCIENTIST') THEN
RETURN TRUE;
ELSE IF (p_exp<5 AND p_exp>=2 AND p_role= 'ASSOCIATE DATA SCIENTIST') THEN
RETURN TRUE;
ELSE IF (p_exp<10 AND p_exp>=5 AND p_role= 'SENIOR DATA SCIENTIST') THEN
RETURN TRUE;
ELSE IF (p_exp<12 AND p_exp>=10 AND p_role= 'LEAD DATA SCIENTIST') THEN
RETURN TRUE;
ELSE IF (p_exp<16 AND p_exp>=12 AND p_role= 'MANAGER' ) THEN
RETURN TRUE;
ELSE RETURN FALSE;


END IF;
END IF;
END IF;
END IF;
END IF;

END 

$$ DELIMITER ;

SELECT ROLE_CHECKER('E006');


RESULT:
```

<img width="208" alt="Screenshot 2023-02-24 at 4 43 57 PM" src="https://user-images.githubusercontent.com/123497764/221165655-c853af22-84aa-45c8-9ec8-707000bcd0ee.png">

```
– question 15
Create an index to improve the cost and performance of the query to find the employee whose FIRST_NAME is ‘Eric’ in the employee table after checking the execution plan.


CREATE INDEX INDEX1
ON emp_record_table(first_name);

SELECT * 
FROM emp_record_table
WHERE first_name='eric';

RESULT:
```
<img width="991" alt="Screenshot 2023-02-24 at 4 49 05 PM" src="https://user-images.githubusercontent.com/123497764/221166586-521c3b02-81df-4b3c-9b29-4d5fe02ccbe5.png">


```

– question 16
Write a query to calculate the bonus for all the employees, based on their ratings and salaries (Use the formula: 5% of salary * employee rating).



SELECT first_name,salary,(salary*emp_rating*0.05) as bonus
FROM emp_record_table;

RESULT:

```
<img width="211" alt="Screenshot 2023-02-24 at 4 50 14 PM" src="https://user-images.githubusercontent.com/123497764/221166792-2caf6bb2-1354-48a9-b826-aeabe87e0c9d.png">

```

– question 17
Write a query to calculate the average salary distribution based on the continent and country. Take data from the employee record table.

select * from emp_record_table
SELECT first_name,salary,country,continent,
AVG(salary) OVER(PARTITION BY continent) avg_cont_sal,salary,
AVG(salary) OVER(PARTITION BY country) avg_country_sal
FROM emp_record_table;

RESULT:
```

<img width="522" alt="Screenshot 2023-02-24 at 4 52 06 PM" src="https://user-images.githubusercontent.com/123497764/221167149-49c61277-a0ba-47e7-a636-6fd84353dfb9.png">

