# Create table sales_data_v2(sales_data_raw.csv)
create table sales_data_v2
     (
     p_type string,
     total_sales int
     )
     row format delimited
     fields terminated by ',';

# Create the backup copy of the table
create table sales_data_v2_bkup as select * from sales_data_v2;

# create the table using csv tab serde along with the properties(csv_file.csv)
create table csv_table
     (
     name string,
     location string
     )
     row format serde 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
     with serdeproperties (
     "separatorChar" = ",",
     "quoteChar" = "\"",
     "escapeChar" = "\\"
     )
     stored as textfile
     tblproperties ("skip.header.line.count"="1");

# create the table for json serde file(json_file.json) no need to give extra collections or properties for json serde it automatically reconizes the format 
create table json_table
     (
     name string,
     id int,
     skills array<string>)
     row format serde 'org.apache.hive.hcatalog.data.JsonSerDe'
     stored as textfile;

# Operation on json 
select skills[0] as primary_skills from json_table;

# link to download jar file
https://repo1.maven.org/maven2/org/apache/hive/hcatalog/hive-hcatalog-core/0.14.0/

# add jar file to hive shell
add jar file:///config/workspace/hive-hcatalog-core-0.14.0.jar;

# store in the parquet format
 create table sales_data_v2
     (
     p_type string,
     total_sales int
     )
     row format delimited 
     fields terminated by ',';

load data local inpath 'file:///config/workspace/sales_data_raw.csv' into table sales_data_v2;

create table sales_data_pq_final
     (
     p_type string,
     total_sales int
     )
     stored as parquet;

from sales_data_v2 insert overwrite table sales_data_pq_final select *;
