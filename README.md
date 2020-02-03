# Big-Data-Hadoop-Commands
This file contains commonly used commands for some basic scenarios for the big data open source framework and some other software components that run on top of it.

## HDFS
HDFS is the primary storage powerhouse of the hadoop ecosystem.

***N.B: The hdfs file system is navigated with the default linux command line command, just prefix with a '-' .***

1. Upload a local file  to a HDFS directory
 `hdfs dfs -put {local-source-file-path} {destination-source-file-path} `

2. Download file from HDFS to a local directory.
  `hdfs dfs -get {destination-source-file-path} {local-source-file-path}`

3. Append the contents of a local file to a file on hdfs
  `hdfs dfs -appendToFile {local-source-file-path} {destination-source-file-path}`

4. Merge the contents of mutiple files in a hdfs directory and download to a file on a local directory, then view contents to confirm.
   `hdfs dfs -getmerge {path-to-hdfs-directory-containing-all-files-to-be-merged or different-paths } {path-to loacal-file}`
   `cat {path-to-loacl-file}`
   
5. Merge multiple files on hdfs into one single file on hdfs
   `hadoop fs -cat {path-to-source-files-seperated-by-a-space-or-path-to-source-folder-containing-all-files/*} | hadoop -put - {path-to-destination-file}`

## HBase
Hbase is a No SQL, column oriented database for the big data hadoop ecosystem.

1. Create a common table
  `create 'table-name','column-family-name'`
  
  *** A column family name can be likened to a sub-category of a table containing columns of related information that will kst likely be queried together ***

2. Create a Namespace
   `create_namespace 'namespace-name'`
   
 *** A namespace is analogous to a function. Used to avoid conflict amognst common table names.***  
   
3. Create a table in a namespace
   `create 'namespace-name:table-name', 'column-family-name'`
   
4. Add data to a table
   `put 'table-name', 'RowKey', 'column-family-name:column-name', 'value'`
   
5. Query entries to a Rowkey
   `get 'table-name', 'RowKey'`
   
6. 
