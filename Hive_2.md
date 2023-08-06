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
