---
title: MySQL
type: docs
---

# MySQL

## Basic Operations

### Login

```sh
sudo mysql -u root -p
```

### Database

```sql
mysql> CREATE DATABASE database_name;
mysql> USE database_name;
mysql> SHOW databases;
```

### Schema

```sql
mysql> DESC table_name;
```

### Table

1. Create table
   ```sql
   mysql> CREATE TABLE table_name (
       -> column_name1 data_type,
       -> column_name2 data_type,
       -> column_name3 data_type,
       -> ...
       -> );
   ```
2. Add column
   ```sql
   mysql> ALTER TABLE table_name ADD column_name datatype;
   ```
3. Alter column type
   ```sql
   mysql> ALTER TABLE table_name ALTER COLUMN column_name datatype;
   ```
4. Drop column
   ```sql
   mysql> ALTER TABLE table_name DROP COLUMN column_name;
   ```
5. Drop table
   ```sql
   mysql> DROP TABLE table_name;
   ```
6. Others
   ```sql
   mysql> SHOW tables;
   mysql> LOAD DATA LOCAL INFILE 'file_path'
       -> INTO TABLE table_name
       -> FIELDS TERMINATED BY ','
       -> IGNORE 1 ROWS;
   mysql> SELECT * FROM table_name LIMIT 10;
   ```

### Data Query

```sql
mysql> SELECT (DISTINCT) table_column1, table_column2, table_column3...
    -> FROM table_name
    -> WHERE column_name operator value

    -> AND column_name2 operator value2
    -> [AND|OR] ...;

    -> ORDER BY column_name1 ASC|DESC, column_name2 ASC|DESC...;
```

### SQL Functions

```SQL
mysql> SELECT COUNT((DISTINCT) column_name) FROM table_name;
```

## Error Solutions

1. ERROR 3950 (42000): Loading local data is disabled; this must be enabled on both the client and server side
   ```sql
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
