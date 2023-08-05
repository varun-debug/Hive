#commands to show databases 
show databases;

#create database
create database hive_db;

#use database
use hive_db;

#command to show tables
show tables;

#command to describe table
describe table_name;

#command to describe formatted table
describe formatted table_name;

#create table in hive
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

#load data from local
load data local inpath 'file:///config/workspace/depart_data.csv' into table department_data;

#Load data from hdfs
load data inpath '/tmp/depart_data.csv' into table department_data;

#
