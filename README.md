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























– question 2
Create an ER diagram for the given employee database.






![image](https://user-images.githubusercontent.com/123497764/221151370-44419fcd-cf61-4c62-9a43-b4b7ef595a9d.png)









```
--  QUESTION 3.
 Write a query to fetch EMP_ID, FIRST_NAME, LAST_NAME, GENDER, and DEPARTMENT from the employee record table, and make a list of employees and details of their department.

SELECT EMP_ID, FIRST_NAME,LAST_NAME,GENDER,DEPT DEPARTMENT
FROM EMP_RECORD_TABLE;

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
 
 
 
 
 
 -- QUESTION 5
Write a query to concatenate the FIRST_NAME and the LAST_NAME of employees in the Finance department from the employee table and then give the resultant column alias as NAME.
 
SELECT CONCAT(FIRST_NAME,LAST_NAME)
FROM EMP_RECORD_TABLE
WHERE DEPT='FINANCE';




-- QUESTION 6;
Write a query to list only those employees who have someone reporting to them. Also, show
the number of reporters (including the President);.

SELECT E1.EMP_ID,COUNT(E1.EMP_ID)
FROM EMP_RECORD_TABLE E1,EMP_RECORD_TABLE E2
WHERE E1.EMP_ID=E2.MANAGER_ID
GROUP BY E1.EMP_ID;




-- QUESTION 7
Write a query to list down all the employees from the healthcare and finance departments
using union. Take data from the employee record table.

SELECT * 
FROM EMP_RECORD_TABLE 
WHERE DEPT IN ('HEALTHCARE', 'FINANCE');


-- QUESTION 8

8. Write a query to list down employee details such as EMP_ID, FIRST_NAME, LAST_NAME,
ROLE, DEPARTMENT, and EMP_RATING grouped by dept. Also include the respective
employee rating along with the max emp rating for the department.

SELECT EMP_ID,FIRST_NAME,LAST_NAME,ROLE,DEPT,EMP_RATING,
(SELECT MAX(EMP_RATING) FROM EMP_RECORD_TABLE WHERE DEPT=E1.DEPT),
 MAX_RATING
FROM EMP_RECORD_TABLE E1
ORDER BY DEPT;










-- QUESTION 9
Write a query to calculate the minimum and the maximum salary of the employees in each
role. Take data from the employee record table.

SELECT DEPT,MAX(SALARY),MIN(SALARY)
FROM EMP_RECORD_TABLE
GROUP BY DEPT;




-- QUESTION 10
Write a query to assign ranks to each employee based on their experience. Take data from
the employee record table.

SELECT EMP_ID, FIRST_NAME,LAST_NAME ,EXP
FROM EMP_RECORD_TABLE
ORDER BY EXP DESC;




– question 11
 Write a query to create a view that displays employees in various countries whose salary is more than six thousand. Take data from the employee record table.

CREATE VIEW rich_emp AS
SELECT emp_id,country,salary
FROM emp_record_table
WHERE salary>6000;
SELECT * FROM rich_emp;











– question 12
Write a nested query to find employees with experience of more than ten years. Take data from the employee record table.


SELECT emp_id,exp 
FROM (SELECT *
	 FROM emp_record_table
     WHERE exp>10) e;



     
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

SELECT ROLE_CHECKER('E006')


select * from data_science_team



– question 15
Create an index to improve the cost and performance of the query to find the employee whose FIRST_NAME is ‘Eric’ in the employee table after checking the execution plan.


CREATE INDEX INDEX1
ON emp_record_table(first_name);

SELECT * 
FROM emp_record_table
WHERE first_name='eric';



– question 16
Write a query to calculate the bonus for all the employees, based on their ratings and salaries (Use the formula: 5% of salary * employee rating).



SELECT first_name,salary,(salary*emp_rating*0.05) as bonus
FROM emp_record_table

– question 17
Write a query to calculate the average salary distribution based on the continent and country. Take data from the employee record table.

select * from emp_record_table
SELECT first_name,salary,country,continent,
AVG(salary) OVER(PARTITION BY continent) avg_cont_sal,salary,
AVG(salary) OVER(PARTITION BY country) avg_country_sal
FROM emp_record_table;


```
