---
title: MySQL
type: docs
---
# MySQL

## 基本操作
1. Login
    ```sh
    sudo mysql -u root -p
    ```
2. Database
    ```SQL
    mysql> CREATE DATABASE database_name;
    mysql> USE database_name;
    mysql> SHOW databases;
    ```

3. Table
    ```SQL
    -- CREATE TABLE
    mysql> CREATE TABLE table_name (
        -> column_name1 data_type,
        -> column_name2 data_type,
        -> column_name3 data_type,
        -> ...
        -> );

    -- ADD COLUMN
    mysql> ALTER TABLE table_name ADD column_name datatype;

    -- ALTER COLUMN TYPE
    mysql> ALTER TABLE table_name ALTER COLUMN column_name datatype;

    -- DROP COLUMN
    mysql> ALTER TABLE table_name DROP COLUMN column_name;

    -- DROP TABLE
    mysql> DROP TABLE table_name;

    mysql> SHOW tables;
    mysql> LOAD DATA LOCAL INFILE 'file_path'
        -> INTO TABLE table_name
        -> FIELDS TERMINATED BY ','
        -> IGNORE 1 ROWS;
    mysql> SELECT * FROM table_name LIMIT 10;
    ```

4. 資料查詢
    ```SQL
    mysql> SELECT (DISTINCT) table_column1, table_column2, table_column3...
        -> FROM table_name
        -> WHERE column_name operator value
        
        -> AND column_name2 operator value2
        -> [AND|OR] ...;
        
        -> ORDER BY column_name1 ASC|DESC, column_name2 ASC|DESC...;
    ```

5. SQL 函數
    ```SQL
    mysql> SELECT COUNT((DISTINCT) column_name) FROM table_name;
    ```


## 錯誤解決
1. ERROR 3950 (42000): Loading local data is disabled; this must be enabled on both the client and server side
    ```SQL
    mysql> SHOW global variables LIKE 'local_infile';
    +---------------+-------+
    | Variable_name | Value |
    +---------------+-------+
    | local_infile  |  OFF  |
    +---------------+-------+
    mysql> SET global local_infile=true;
    mysql> QUIT
    ```
    ```sh
    sudo mysql --local_infile=1 -u root -p
    ```
2. ERROR 1290 (HY000): The MySQL server is running with the --secure-file-priv option so it cannot execute this statement.
    ```sh
    cd etc/mysql/
    sudo chmod 644 my.cnf
    sudo nano my.cnf
    ```
    ```toml
    # my.cnf
    [mysqld]
    secure-file-priv = ""
    ```
