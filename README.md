# Big Data Hadoop Commands
This file contains commonly used commands for some basic scenarios for the big data open source framework and some other software components that run on top of it.

## HDFS
HDFS is the primary storage powerhouse of the hadoop ecosystem.

***N.B: The hdfs file system is navigated with the default linux command line commands, just prefix with a '-' . Also run commands without the braces i.e {}***

1. Upload a local file  to a HDFS directory\
 `hdfs dfs -put {local-source-file-path} {destination-source-file-path} `

2. Download file from HDFS to a local directory.\
  `hdfs dfs -get {destination-source-file-path} {local-source-file-path}`

3. Append the contents of a local file to a file on hdfs\
  `hdfs dfs -appendToFile {local-source-file-path} {destination-source-file-path}`

4. Merge the contents of mutiple files in a hdfs directory and download to a file on a local directory, then view contents to confirm.\
   `hdfs dfs -getmerge {path-to-hdfs-directory-containing-all-files-to-be-merged or different-paths } {path-to loacal-file}`
   `cat {path-to-loacl-file}`
   
5. Merge multiple files on hdfs into one single file on hdfs\
   `hadoop fs -cat {path-to-source-files-seperated-by-a-space-or-path-to-source-folder-containing-all-files/*} | hadoop -put - {path-to-destination-file}`

## HBase
Hbase is a No SQL, column oriented database for the big data hadoop ecosystem.

1. Create a common table\
  `create 'table-name','column-family-name'`
  
***A column family name can be likened to a sub-category of a table containing columns of related information that will likely be queried together***

2. Create a Namespace\
   `create_namespace 'namespace-name'`
   
 ***A namespace is analogous to a function. Used to avoid conflict amognst common table names***  
   
3. Create a table in a namespace\
   `create 'namespace-name:table-name', 'column-family-name'`
   
4. Add data to a table\
   `put 'table-name', 'RowKey', 'column-family-name:column-name', 'value'`
   
5. Query entries to a Rowkey\
   `get 'table-name', 'RowKey'`
   
6. Query entries to a column\
   `get 'table-name', 'column-family-name:column-name'`
   
7. Query table for a perticular value\
   `scan 'table-name', {FILTER=>"ValueFilter(=,'binaryFilter:value')"}`
   
8. Query a particular column for a particular value\
   `scan 'table-name', {FILTER=>"ColumnPrefixFilter('column-name') AND ValueFilter(=,'binaryFilter:value')"}
   
9. Delete a value from a column\
   `delete 'table-name', 'RowKey', 'column-family-name:column-name'`
   
10. Delete all data in a row from differnet columns\
    `deleteall 'table-name', 'RowKey',`
    
11. Delete a whole table\
    `disable 'table-name'`\
    `drop 'table-name'`
    
12. Creating and Dividing a common table into regions and specifying row start keys for each region.\
    `create 'table-name', 'column-family-name', SPILITS => ['first-start-key', 'second-start-key', ...]`

***Specifying n number of start keys creates n+1 number of regions where the first region starts at 0 and ends at the first startkey***


### HIVE
Hive is a data warehouse used to query and analyze data stored in different databases and file systems that with hadoop using an SQL like interface.

1. Get the current date and time \
   `select from_unixtime(unix_timestamp(), dd-MM-yyyy  HH:mm);`
   
2. Create an internal table\
   `create table table-name (column-name data-type, column-name data type, ....) row format delimited fields terminated by ',' stored as textfile ;`
    
***Internal tables are tables that are only accessed within hive while external tables can be accessed outside of hive***

3. Create an external table\
    `create external table <table-name> (column-name data-type, column-name data type, ....) row format delimited fields terminated by ',' stored as textfile; `
    
4. Load data from a local file to hive\
    `load data local inpath <'path-to-local-file'> into table <table-name>;`
    
5. Load data from a hdfs file\
   `load data inpath 'path-to-hdfs-file' into table table-name;`
   
6. Load data immediately from source when creating the table\
    `create table <table-name> (column-name data-type, column-name data type, ....) row format delimited fields terminated by ',' stored as textfile location <'path-to-source-file'>;`
    
7. Load only rows of a table which contain a given column value into another table\
   `insert into <destination-table-name> select * from <source-table-name> where <column-name=value>;`
   
8. Load data from one Hive table to another.\
   `create table <new-table-name> as select * from <source-table-name>`
    
9. Load only rows of a table which contain a given column value into another table\
   `insert into <destination-table-name> select * from <source-table-name> where <column-name=value>;`
   
10. Create a table with the specifications of an existing table\
   `create <new-table-name> like <existing-table-name>;`
   
11. Query table for all rows containing occurence of a particular value in a column\
   `select * from <table-name> where <column-name='value'>;`

12. Associating a Hive table with a Hbase base table on table creation\
   `create external table <external-table-name> (key int, gid map <<column-1-data-type,column-2-data-type>>) stored by 'org.hadoop.hive.hbase.HbaseStorageHandler' with SERDEPROPERTIES ("hbase.columns.mapping" = "<hbase-table-column-family-name:>") TBLPROPERTIES ("hbase.table.name" = "<hbase-table-name>");`
    
    
