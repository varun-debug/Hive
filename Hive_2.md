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

# create the table using serde propertices(csv_file.csv)
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
