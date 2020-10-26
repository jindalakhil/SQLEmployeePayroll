Type '\help' or '\?' for help; '\quit' to exit.
 MySQL  JS > \sql
Switching to SQL mode... Commands end with ;
 MySQL  SQL > \connect ajindal@host
Creating a session to 'ajindal@host'
Please provide the password for 'ajindal@host': ********
MySQL Error 2005: No such host is known 'host'
 MySQL  SQL > \connect ajindal@localhost
Creating a session to 'ajindal@localhost'
Fetching schema names for autocompletion... Press ^C to stop.
Your MySQL connection id is 31 (X protocol)
Server version: 8.0.22 MySQL Community Server - GPL
No default schema selected; type \use <schema> to set one.
 MySQL  localhost:33060+ ssl  SQL > show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| payroll_service    |
| performance_schema |
| sakila             |
| sys                |
| world              |
+--------------------+
7 rows in set (0.0012 sec)
 MySQL  localhost:33060+ ssl  SQL > select payroll_service
                                 -> ;
ERROR: 1054: Unknown column 'payroll_service' in 'field list'
 MySQL  localhost:33060+ ssl  SQL > create table employee_payroll
                                 -> (
                                 -> id INT unsigned NOTNULL AUTO_INCREMENT,
                                 -> \connect ajindal@host^C
 MySQL  localhost:33060+ ssl  SQL > create table employee_payroll
                                 -> (
                                 -> id INT unsigned NOT NULL AUTO_INCREMENT,
                                 -> name VARCHAR(150) NOT NULL,
                                 -> salary Double NOT NULL,
                                 -> start DATE NOT NULL,
                                 -> PRIMARY KEY (id)
                                 -> );
ERROR: 1046: No database selected
 MySQL  localhost:33060+ ssl  SQL > select payroll_service();
ERROR: 1046: No database selected
 MySQL  localhost:33060+ ssl  SQL > select database payroll_service
                                 -> ;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'payroll_service' at line 1
 MySQL  localhost:33060+ ssl  SQL > select databse
                                 -> ;
ERROR: 1054: Unknown column 'databse' in 'field list'
 MySQL  localhost:33060+ ssl  SQL > use payroll_service
Default schema set to `payroll_service`.
Fetching table and column names from `payroll_service` for auto-completion... Press ^C to stop.
 MySQL  localhost:33060+ ssl  payroll_service  SQL > create table employee_payroll ( id INT unsigned NOT NULL AUTO_INCREMENT, name VARCHAR(150) NOT NULL, salary Double NOT NULL, start DATE NOT NULL, PRIMARY KEY (id) );
Query OK, 0 rows affected (1.8944 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > ^C
 MySQL  localhost:33060+ ssl  payroll_service  SQL > insert into employee_payroll(name,salary,start)
                                                  -> Values('Akhil',10000,'2020-09-16'),
                                                  -> ('Deepak',10001,'2020-09-17');
Query OK, 2 rows affected (1.5451 sec)

Records: 2  Duplicates: 0  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > insert into employee_payroll(name,salary,start) Values('AJ',10004,'2020-09-18')
                                                  -> ;
Query OK, 1 row affected (0.1065 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > describe employee_payroll;
+--------+--------------+------+-----+---------+----------------+
| Field  | Type         | Null | Key | Default | Extra          |
+--------+--------------+------+-----+---------+----------------+
| id     | int unsigned | NO   | PRI | NULL    | auto_increment |
| name   | varchar(150) | NO   |     | NULL    |                |
| salary | double       | NO   |     | NULL    |                |
| start  | date         | NO   |     | NULL    |                |
+--------+--------------+------+-----+---------+----------------+
4 rows in set (0.3111 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > insert into employee_payroll(name,salary,start) Values('TEST',10004,'2019-09-18') ;
Query OK, 1 row affected (0.1351 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select * from employee_payroll
                                                  -> where start Between CAST('2019-01-01') AND DATE(NOW);
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ') AND DATE(NOW)' at line 2
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select * from employee_payroll where start Between CAST('2019-01-01' As DATE) AND DATE(NOW());
+----+--------+--------+------------+
| id | name   | salary | start      |
+----+--------+--------+------------+
|  1 | Akhil  |  10000 | 2020-09-16 |
|  2 | Deepak |  10001 | 2020-09-17 |
|  3 | AJ     |  10004 | 2020-09-18 |
|  4 | TEST   |  10004 | 2019-09-18 |
+----+--------+--------+------------+
4 rows in set (0.0432 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > ALTER Table employee_payroll ADD gender char(1) after name;
Query OK, 0 rows affected (4.5544 sec)

Records: 0  Duplicates: 0  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > describe employee_payroll
                                                  -> ;
+--------+--------------+------+-----+---------+----------------+
| Field  | Type         | Null | Key | Default | Extra          |
+--------+--------------+------+-----+---------+----------------+
| id     | int unsigned | NO   | PRI | NULL    | auto_increment |
| name   | varchar(150) | NO   |     | NULL    |                |
| gender | char(1)      | YES  |     | NULL    |                |
| salary | double       | NO   |     | NULL    |                |
| start  | date         | NO   |     | NULL    |                |
+--------+--------------+------+-----+---------+----------------+
5 rows in set (0.1351 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > update employee_payroll set gender = 'F' where name = 'TEST';
Query OK, 1 row affected (0.2689 sec)

Rows matched: 1  Changed: 1  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select * from employee_payroll;
+----+--------+--------+--------+------------+
| id | name   | gender | salary | start      |
+----+--------+--------+--------+------------+
|  1 | Akhil  | NULL   |  10000 | 2020-09-16 |
|  2 | Deepak | NULL   |  10001 | 2020-09-17 |
|  3 | AJ     | NULL   |  10004 | 2020-09-18 |
|  4 | TEST   | F      |  10004 | 2019-09-18 |
+----+--------+--------+--------+------------+
4 rows in set (0.0010 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > update employee_payroll set gender = 'M' where name = 'Akhil' or name = 'AJ' or name = 'Deepak';
Query OK, 3 rows affected (0.0841 sec)

Rows matched: 3  Changed: 3  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select * from employee_payroll;
+----+--------+--------+--------+------------+
| id | name   | gender | salary | start      |
+----+--------+--------+--------+------------+
|  1 | Akhil  | M      |  10000 | 2020-09-16 |
|  2 | Deepak | M      |  10001 | 2020-09-17 |
|  3 | AJ     | M      |  10004 | 2020-09-18 |
|  4 | TEST   | F      |  10004 | 2019-09-18 |
+----+--------+--------+--------+------------+
4 rows in set (0.0333 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > update employee_payroll set salary = 20000 where name = 'TEST';
Query OK, 1 row affected (0.0996 sec)

Rows matched: 1  Changed: 1  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select * from employee_payroll;
+----+--------+--------+--------+------------+
| id | name   | gender | salary | start      |
+----+--------+--------+--------+------------+
|  1 | Akhil  | M      |  10000 | 2020-09-16 |
|  2 | Deepak | M      |  10001 | 2020-09-17 |
|  3 | AJ     | M      |  10004 | 2020-09-18 |
|  4 | TEST   | F      |  20000 | 2019-09-18 |
+----+--------+--------+--------+------------+
4 rows in set (0.0007 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select avg(salary) from employee_payroll where gender = 'M' groub by gender;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'groub by gender' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select avg(salary) from employee_payroll where gender = 'M' GROUP BY gender;
+--------------------+
| avg(salary)        |
+--------------------+
| 10001.666666666666 |
+--------------------+
1 row in set (0.0369 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select avg(salary) from employee_payroll where gender = 'M';
+--------------------+
| avg(salary)        |
+--------------------+
| 10001.666666666666 |
+--------------------+
1 row in set (0.0024 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select avg(salary) from employee_payroll where GROUP BY gender;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'GROUP BY gender' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select avg(salary) from employee_payroll GROUP BY gender;
+--------------------+
| avg(salary)        |
+--------------------+
| 10001.666666666666 |
|              20000 |
+--------------------+
2 rows in set (0.0031 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select gender, avg(salary) from employee_payroll GROUP BY gender;
+--------+--------------------+
| gender | avg(salary)        |
+--------+--------------------+
| M      | 10001.666666666666 |
| F      |              20000 |
+--------+--------------------+
2 rows in set (0.0012 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select gender, Count(name) from employee_payroll GROUP BY gender;
+--------+-------------+
| gender | Count(name) |
+--------+-------------+
| M      |           3 |
| F      |           1 |
+--------+-------------+
2 rows in set (0.0008 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select gender, Count(salary) from employee_payroll GROUP BY gender;

+--------+---------------+
| gender | Count(salary) |
+--------+---------------+
| M      |             3 |
| F      |             1 |
+--------+---------------+
2 rows in set (0.0008 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > select gender, sum(salary) from employee_payroll GROUP BY gender;
+--------+-------------+
| gender | sum(salary) |
+--------+-------------+
| M      |       30005 |
| F      |       20000 |
+--------+-------------+
2 rows in set (0.0031 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > ^C
 MySQL  localhost:33060+ ssl  payroll_service  SQL > ^C
 MySQL  localhost:33060+ ssl  payroll_service  SQL >  select gender, Count(name) from employee_payroll GROUP BY gender;
+--------+-------------+
| gender | Count(name) |
+--------+-------------+
| M      |           3 |
| F      |           1 |
+--------+-------------+
2 rows in set (0.0009 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > +--------+-------------+
                                                  -> | gender | Count(name) |
                                                  -> +--------+-------------+
                                                  -> | M      |           3 |
                                                  -> | F      |           1 |
                                                  -> +--------+-------------+
                                                  -> ;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '+--------+-------------+
| gender | Count(name) |
+--------+-------------+
| M  ' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL >  select gender, Count(name) from employee_payroll GROUP BY gender;
+--------+-------------+
| gender | Count(name) |
+--------+-------------+
| M      |           3 |
| F      |           1 |
+--------+-------------+
2 rows in set (0.0008 sec)
 MySQL  localhost:33060+ ssl  payroll_service  SQL > +--------+-------------+
                                                  -> | gender | Count(name) |
                                                  -> +--------+-------------+
                                                  -> | M      |           3 |
                                                  -> | F      |           1 |
                                                  ->
                                                  -> ;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '+--------+-------------+
| gender | Count(name) |
+--------+-------------+
| M  ' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL > ^C
 MySQL  localhost:33060+ ssl  payroll_service  SQL > alter table employee_payroll add phone_number varchar(250) after name;
Query OK, 0 rows affected (2.8849 sec)

Records: 0  Duplicates: 0  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > alter table employee_payroll add address varchar(250) after phone_number;
Query OK, 0 rows affected (2.9608 sec)

Records: 0  Duplicates: 0  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > alter table employee_payroll add department varchar(150) after address;
Query OK, 0 rows affected (1.9160 sec)

Records: 0  Duplicates: 0  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > alter table employee_payroll update department varchar(150) NOT Null;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'update department varchar(150) NOT Null' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL > alter table employee_payroll update department varchar(150) NOT Null after address;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'update department varchar(150) NOT Null after address' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL > alter table employee_payroll update department varchar(150) NOT NULL;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'update department varchar(150) NOT NULL' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL > alter table employee_payroll update department NOT NULL;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'update department NOT NULL' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL > department varchar(150) NOT NULL;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'department varchar(150) NOT NULL' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL > alter department varchar(150) NOT NULL;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'department varchar(150) NOT NULL' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL > Alter table employee_payroll department varchar(150) NOT NULL;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'department varchar(150) NOT NULL' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL > Alter table employee_payroll modify department varchar(150) NOT NULL;
ERROR: 1138: Invalid use of NULL value
 MySQL  localhost:33060+ ssl  payroll_service  SQL > Alter table employee_payroll rename column salary TO basic_pay;
Query OK, 0 rows affected (1.8670 sec)

Records: 0  Duplicates: 0  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > Alter table employee_payroll add deductions Double NOT NULL AFTER basic_pay;
Query OK, 0 rows affected (2.2504 sec)

Records: 0  Duplicates: 0  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > Alter table employee_payroll add taxable_pay Double NOT NULL AFTER deductions;
Query OK, 0 rows affected (1.9416 sec)

Records: 0  Duplicates: 0  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > Alter table employee_payroll add tax Double NOT NULL AFTER taxable_pay;
Query OK, 0 rows affected (1.8986 sec)

Records: 0  Duplicates: 0  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > Alter table net_pay add tax Double NOT NULL AFTER tax;
ERROR: 1146: Table 'payroll_service.net_pay' doesn't exist
 MySQL  localhost:33060+ ssl  payroll_service  SQL > Alter table employee_payroll add net_pay Double NOT NULL AFTER tax;

Query OK, 0 rows affected (3.6363 sec)

Records: 0  Duplicates: 0  Warnings: 0
 MySQL  localhost:33060+ ssl  payroll_service  SQL > describe employee-payroll
                                                  -> ;
ERROR: 1064: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '-payroll' at line 1
 MySQL  localhost:33060+ ssl  payroll_service  SQL > describe employee_payroll ;
+--------------+--------------+------+-----+---------+----------------+
| Field        | Type         | Null | Key | Default | Extra          |
+--------------+--------------+------+-----+---------+----------------+
| id           | int unsigned | NO   | PRI | NULL    | auto_increment |
| name         | varchar(150) | NO   |     | NULL    |                |
| phone_number | varchar(250) | YES  |     | NULL    |                |
| address      | varchar(250) | YES  |     | NULL    |                |
| department   | varchar(150) | YES  |     | NULL    |                |
| gender       | char(1)      | YES  |     | NULL    |                |
| basic_pay    | double       | NO   |     | NULL    |                |
| deductions   | double       | NO   |     | NULL    |                |
| taxable_pay  | double       | NO   |     | NULL    |                |
| tax          | double       | NO   |     | NULL    |                |
| net_pay      | double       | NO   |     | NULL    |                |
| start        | date         | NO   |     | NULL    |                |
+--------------+--------------+------+-----+---------+----------------+
12 rows in set (0.0395 sec)