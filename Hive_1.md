# commands to show databases 
show databases;

# create database
create database hive_db;

# use database
use hive_db;

# command to show tables
show tables;

# command to describe table
describe table_name;

# command to describe formatted table
describe formatted table_name;

# create table in hive
create table department_data
(
dept_id int,
dept_name string,
manager_id int,
salary int)
row format delimited
fields terminated by ',';

describe department_data;

describe formatted department_data;

# load data from local
load data local inpath 'file:///config/workspace/depart_data.csv' into table department_data;

# Load data from hdfs
load data inpath '/tmp/depart_data.csv' into table department_data;

# command to create external tables
create external table department_data_external
    (
    dept_id int,
    dept_name string,
    manager_id int,
    salary int
     )
    row format delimited
    fields terminated by ','
    location '/input_data/';

# create array 
create table employee
     (
     emp_id int,
     name string,
     skills array<string>
     )
     row format delimited
     fields terminated by ','
     collection items terminated by ':';

# to see the column names used in hive
set hive.cli.print.header=true;

# use of array to show 1st element of the col
 select name,
    skills[0] as Primary_Skill
    from employee;

# multiple operation like sort or contains in array col
select emp_id,
     name,
     size(skills) as total_size,
     array_contains(skills,"HADOOP") as knows_hadoop,
     sort_array(skills) as sorted_skills
     from employee;
