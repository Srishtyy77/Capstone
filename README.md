# Capstone
Data_eng
Data Engineering Introduction: • You have been hired as a new data engineer at Analytixlabs. Your first major task is to work on data engineering project for one of the big corporation’s employees data from the 1980s and 1995s. All the database of employees from that period are provided six CSV files. In this project, you will design data model with all the tables to hold data, import the CSVs into a SQL database, transfer SQL database to HDFS/Hive, and perform analysis using Hive/Impala/Spark/SparkML using the data and create data and ML pipelines. Project Description: In this project, you are required to create end to end data pipeline and analyzing the data. Technology Stack: you are required to work on below technology Stack.

MySQL (to create database)
Linux Commands
Sqoop (Transfer data from MySQL Server to HDFS/Hive)
HDFS (to store the data)
Hive (to create database)
Impala (to perform the EDA)
SparkSQL (to perform the EDA)
SparkML (to perform model building)
Project Objective: As part of this project, you are required to work on

Create data model as per your understanding from the data (you are required include tables names, relation between tables, column names, data types, primary & foreign keys etc.) Tip: You can create ER diagram either in EXCEL or using the link https://www.quickdatabasediagrams.com/ (Preferably in this app)
Create database & tables in MySQL server as per the above ER Diagram
Create Sqoop job to transfer the data from MySQL to HDFS (Data required to store in Parque/Avro/Json format)
Create database in Hive as per the above ER Diagram and load the data into Hive tables
Work on Exploratory data analysis as per the analysis requirement using Impala and Spark SQL (expecting to get the data from hive tables).
Build ML Model as per the requirement.
Create entire data pipeline and ML pipe line
Upload the entire project repository including source code to Github (you are required to create github account if you don’t have it)
SQL commmands

***** Creating tables

Create table titles( title_id Varchar(20) unique not null, title varchar(30) not null ); create table employees( emp_no int primary key, emp_title_id varchar(10) not null, birth_date DATE not null, first_name varchar(20) not null, last_name varchar(20) not null, sex varchar(2) not null, hire_date DATE not null, no_of_projects int not null, last_performance_rating varchar(4)not null, left_ tinyint(1) not null, last_date DATE); create table salaries( emp_no int unique not null, salary int not null ); create table department_employees ( emp_no int not null, dept_no varchar(10) not null ); create table department_manager ( dept_no Varchar(10) not null, emp_no int not null ); create table departments ( dept_no varchar(10) unique not null, dept_name varchar(30) not null );
load data local infile '/home/anabig114213/Data/titles.csv' into table titles fields terminated by ',' ignore 1 rows;                                     
load data local infile '/home/anabig114213/Data/employees.csv' into table employees fields terminated by ',' ignore 1 rows;                                     
load data local infile '/home/anabig114213/Data/salaries.csv' into table salaries fields terminated by ',' ignore 1 rows;                                     
load data local infile '/home/anabig114213/Data/dept_emp.csv' into table department_employees fields terminated by ',' ignore 1 rows;                                     
load data local infile '/home/anabig114213/Data/dept_manager.csv' into table department_manager fields terminated by ',' ignore 1 rows;                                     
load data local infile '/home/anabig114213/Data/departments.csv' into table departments fields terminated by ',' ignore 1 rows; 
sqoop import-all-tables --connect jdbc:mysql://ip-10-1-1-204.ap-south-1.compute.internal:3306/anabig114213 --username anabig114213 --password Bigdata123 --compression-codec=snappy --as-avrodatafile --warehouse-dir /user/anabig114213/EXLProject --m 1 --driver com.mysql.jdbc.Driver  
HIVE/IMPALA     

Create table titles( title_id Varchar(20) , title varchar(30))
STORED AS PARQUET LOCATION "/user/anabig114213/EXLProject/titles";
--
create table employees( emp_no int ,  emp_title_id varchar(10) ,  birth_date varchar(15),  first_name varchar(20) ,  last_name varchar(20) ,  sex varchar(2) ,  hire_date varchar(15) ,  no_of_projects int ,  last_performance_rating varchar(4) ,  left_ tinyint ,  last_date Varchar(15))
STORED AS PARQUET LOCATION "/user/anabig114213/EXLProject/employees";
--
create table salaries( emp_no int , salary int)
STORED AS PARQUET LOCATION "/user/anabig114213/EXLProject/salaries";
--
create table department_employees ( emp_no int, dept_no varchar(10))
STORED AS PARQUET LOCATION "/user/anabig114213/EXLProject/department_employees";
--
create table department_manager ( dept_no Varchar(10), emp_no int)
STORED AS PARQUET LOCATION "/user/anabig114213/EXLProject/department_manager";
--
create table departments ( dept_no varchar(10), dept_name varchar(30))
STORED AS PARQUET LOCATION "/user/anabig114213/EXLProject/departments";

