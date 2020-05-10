# ibm_sql_for_data_science
sql for data science course by ibm

## Lab Solutions
The steps to get the answers to the queries:
1) Navigate to the Run SQL page on Db2 on Cloud.

3) Run the queries. Looking at the contents of the Log explains that the SQL
statement that we ran was successful. Here are the results for the queries:

I created the tables for the HR database schema and also learned how to load
data into these tables. Then try and work on a few advanced DML queries that were
introduced in this module. 

### A- Creating tables

CREATE TABLE EMPLOYEES ( <br>
                           <ul> EMP_ID CHAR(9) NOT NULL, <br>
                            F_NAME VARCHAR(15) NOT NULL,<br>
                            L_NAME VARCHAR(15) NOT NULL,<br>
                            SSN CHAR(9),<br>
                            B_DATE DATE,<br>
                            SEX CHAR,<br>
                            ADDRESS VARCHAR(30),<br>
                            JOB_ID CHAR(9),<br>
                            SALARY DECIMAL(10,2),<br>
                            MANAGER_ID CHAR(9),<br>
                            DEP_ID CHAR(9) NOT NULL,<br>
                            PRIMARY KEY (EMP_ID));<br></ul>
                            
  CREATE TABLE JOB_HISTORY (<br>
                            <ul>EMPL_ID CHAR(9) NOT NULL, <br>
                            START_DATE DATE,<br>
                            JOBS_ID CHAR(9) NOT NULL,<br>
                            DEPT_ID CHAR(9),<br>
                            PRIMARY KEY (EMPL_ID,JOBS_ID));<br></ul>
 
 CREATE TABLE JOBS (<br>
                            <ul>JOB_IDENT CHAR(9) NOT NULL, <br>
                            JOB_TITLE VARCHAR(15) ,<br>
                            MIN_SALARY DECIMAL(10,2),<br>
                            MAX_SALARY DECIMAL(10,2),<br>
                            PRIMARY KEY (JOB_IDENT));<br></ul>

CREATE TABLE DEPARTMENTS (<br>
                            <ul>DEPT_ID_DEP CHAR(9) NOT NULL, <br>
                            DEP_NAME VARCHAR(15) ,<br>
                            MANAGER_ID CHAR(9),<br>
                            LOC_ID CHAR(9),<br>
                            PRIMARY KEY (DEPT_ID_DEP));<br></ul>

CREATE TABLE LOCATIONS (<br>
                            <ul>LOCT_ID CHAR(9) NOT NULL,<br>
                            DEP_ID_LOC CHAR(9) NOT NULL,<br>
                            PRIMARY KEY (LOCT_ID,DEP_ID_LOC));<br></ul>
                            
                            
### B - Loading data from csv files
### C - Manipularing data uding queries 
  #### Query 1: Retrieve all employees whose address is in Elgin,IL
  
  select F_NAME , L_NAME from employees where address like '%Elgin,IL%';
  
  #### Query 2: Retrieve all employees who were born during the 1970's.
  
  select F_NAME , L_NAME from employees where B_DATE LIKE '197%';
  
  #### Query 3: Retrieve all employees in department 5 whose salary is between 60000 and 70000 .
  
  select F_NAME , L_NAME from employees where DEP_ID  = 5 and (salary between 60000 and 70000);
  
  #### Query 4A: Retrieve a list of employees ordered by department ID
  
  select F_NAME , L_NAME from employees order by dep_id;
  
  #### Query 4B: Retrieve a list of employees ordered in descending order by department ID and within each department ordered alphabetically in descending order by last name.
  
  select F_NAME , L_NAME from employees order by dep_id desc, L_name desc;
  
  #### Query 5A: For each department ID retrieve the number of employees in the department.
  
  select dep_id , count(*) from employees group by dep_id;
  
  #### Query 5B: For each department retrieve the number of employees in the department, and the average employees salary in the department.
  
  select count(*) , avg(salary) from  employees group by dep_id;
  
  #### Query 5C: Label the computed columns in the result set of Query 5B as “NUM_EMPLOYEES” and “AVG_SALARY”.
  
  select count(*)  as NUM_EMPLOYEES , avg(salary)  as AVG_SALARY from  employees group by dep_id;
  
  #### Query 5D: In Query 5C order the result set by Average Salary.
  
  select count(*)  as NUM_EMPLOYEES , avg(salary)  as AVG_SALARY from  employees group by dep_id order by AVG_SALARY ;
  
  #### Query 5E: In Query 5D limit the result to departments with fewer than 4 employees.
  
  select count(*)  as NUM_EMPLOYEES , avg(salary)  as AVG_SALARY from  employees group by dep_id having count(*) < 4 order by AVG_SALARY ;

