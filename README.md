
C:\Users\Minfy>psql --version
psql (PostgreSQL) 17.5

C:\Users\Minfy>psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.


                                              
                                              ^
postgres=# CREATE USER NihaarMinfy WITH PASSWORD 'Nihaar@6';
CREATE ROLE
postgres=# CREATE DATABASE minfy_db OWNER NihaarMinfy
postgres-# GRANT ALL PRIVILEGES ON DATABASE minfy_db TO NihaarMinfy
postgres-# \\q
invalid command \
Try \? for help.
postgres-# \q



C:\Users\Minfy>psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# CREATE USER university_admin WITH PASSWORD 'nihaar';
CREATE ROLE
postgres=# CREATE DATABASE university_db OWNER university_admin;
CREATE DATABASE
postgres=# GRANT ALL PRIVILEGES ON DATABASE university_db TO university_admin;
GRANT
postgres=# \q

C:\Users\Minfy>psql -U university_admin -d university_db
Password for user university_admin:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.



university_db=> \l
                                                                                  List of databases
     Name      |      Owner       | Encoding | Locale Provider |          Collate           |           Ctype            | Locale | ICU Rules |           Access privileges
---------------+------------------+----------+-----------------+----------------------------+----------------------------+--------+-----------+---------------------------------------
 postgres      | postgres         | UTF8     | libc            | English_United States.1252 | English_United States.1252 |        |           |
 template0     | postgres         | UTF8     | libc            | English_United States.1252 | English_United States.1252 |        |           | =c/postgres                          +
               |                  |          |                 |                            |                            |        |           | postgres=CTc/postgres
 template1     | postgres         | UTF8     | libc            | English_United States.1252 | English_United States.1252 |        |           | =c/postgres                          +
               |                  |          |                 |                            |                            |        |           | postgres=CTc/postgres
 university_db | university_admin | UTF8     | libc            | English_United States.1252 | English_United States.1252 |        |           | =Tc/university_admin                 +
               |                  |          |                 |                            |                            |        |           | university_admin=CTc/university_admin
(4 rows)        ^Z^X\q

C:\Users\Minfy>psql -U university_admin -d university_db
Password for user university_admin:

psql: error: connection to server at "localhost" (::1), port 5432 failed: fe_sendauth: no password supplied

C:\Users\Minfy>psql -U postgres
Password for user postgres:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

postgres=# psql -U university_admin -d university_db
postgres-# psql -U university_admin -d university_db
postgres-# \q

C:\Users\Minfy>psql -U university_admin -d university_db
Password for user university_admin:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.


C:\Users\Minfy>psql -U university_admin -d university_db
Password for user university_admin:

psql (17.5)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

university_db=> CREATE TABLE STUDENTS(
university_db(> student_id INTEGER,
university_db(> first_name VARCHAR(50),
university_db(> last_name VARCHAR(50),
university_db(> email VARCHAR(100),
university_db(> dob DATE);
CREATE TABLE
university_db=> \dt


              List of relations
 Schema |   Name   | Type  |      Owner
--------+----------+-------+------------------
 public | students | table | university_admin
(1 row)




university_db=> \d


              List of relations
 Schema |   Name   | Type  |      Owner
--------+----------+-------+------------------
 public | students | table | university_admin
(1 row)


university_db=> ALTER TABLE students ADD COLUMN enrollment_date DATE;
ALTER TABLE


university_db=> \d students


                          Table "public.students"
     Column      |          Type          | Collation | Nullable | Default
-----------------+------------------------+-----------+----------+---------
 student_id      | integer                |           |          |
 first_name      | character varying(50)  |           |          |
 last_name       | character varying(50)  |           |          |
 email           | character varying(100) |           |          |
 dob             | date                   |           |          |
 enrollment_date | date                   |           |          |


university_db=> ALTER TABLE students DROP COLUMN enrollment_date
university_db-> ALTER TABLE students DROP COLUMN enrollment_date;
ERROR:  syntax error at or near "ALTER"
LINE 2: ALTER TABLE students DROP COLUMN enrollment_date;
        ^
university_db=> ALTER TABLE students DROP COLUMN enrollment_date;
ALTER TABLE
university_db=> \d students


                       Table "public.students"
   Column   |          Type          | Collation | Nullable | Default
------------+------------------------+-----------+----------+---------
 student_id | integer                |           |          |
 first_name | character varying(50)  |           |          |
 last_name  | character varying(50)  |           |          |
 email      | character varying(100) |           |          |
 dob        | date                   |           |          |




university_db=> ALTER TABLE students ALTER COLUMN email TYPE VARCHAR(150);
ALTER TABLE
university_db=> \d students


                       Table "public.students"
   Column   |          Type          | Collation | Nullable | Default
------------+------------------------+-----------+----------+---------
 student_id | integer                |           |          |
 first_name | character varying(50)  |           |          |
 last_name  | character varying(50)  |           |          |
 email      | character varying(150) |           |          |
 dob        | date                   |           |          |



university_db=> ALTER TABLE students RENAME COLUMN dob TO d_o_b;
ALTER TABLE
university_db=> \d

              List of relations
 Schema |   Name   | Type  |      Owner
--------+----------+-------+------------------
 public | students | table | university_admin
(1 row)


university_db=> \d students;

                       Table "public.students"
   Column   |          Type          | Collation | Nullable | Default
------------+------------------------+-----------+----------+---------
 student_id | integer                |           |          |
 first_name | character varying(50)  |           |          |
 last_name  | character varying(50)  |           |          |
 email      | character varying(150) |           |          |
 d_o_b      | date                   |           |          |


university_db=> ALTER TABLE students RENAME TO  learners;
ALTER TABLE
university_db=> ALTER TABLE learners RENAME TO students
university_db-> ALTER TABLE learners RENAME TO students;
ERROR:  syntax error at or near "ALTER"
LINE 2: ALTER TABLE learners RENAME TO students;
        ^
university_db=> ALTER TABLE learners RENAME TO students;;
ALTER TABLE
university_db=> \d


              List of relations
 Schema |   Name   | Type  |      Owner
--------+----------+-------+------------------
 public | students | table | university_admin
(1 row)


university_db=> ALTER TABLE students ADD COLUMN phone_number VARCHAR(20);
ALTER TABLE

university_db=> \d
              List of relations
 Schema |   Name   | Type  |      Owner
--------+----------+-------+------------------
 public | students | table | university_admin
(1 row)


university_db=> \d students;


                        Table "public.students"
    Column    |          Type          | Collation | Nullable | Default
--------------+------------------------+-----------+----------+---------
 student_id   | integer                |           |          |
 first_name   | character varying(50)  |           |          |
 last_name    | character varying(50)  |           |          |
 email        | character varying(150) |           |          |
 d_o_b        | date                   |           |          |
 phone_number | character varying(20)  |           |          |


university_db=> ALTER TABLE students DROP COLUMN phone_number;
ALTER TABLE
university_db=> \d students;


                       Table "public.students"
   Column   |          Type          | Collation | Nullable | Default
------------+------------------------+-----------+----------+---------
 student_id | integer                |           |          |
 first_name | character varying(50)  |           |          |
 last_name  | character varying(50)  |           |          |
 email      | character varying(150) |           |          |
 d_o_b      | date                   |           |          |


university_db=> INSERT INTO students
university_db-> VALUES (1,'Nihaar','Reddy','nihaar.reddy@gmail.com','2004-07-12');
INSERT 0 1
university_db=> \d students;


                       Table "public.students"
   Column   |          Type          | Collation | Nullable | Default
------------+------------------------+-----------+----------+---------
 student_id | integer                |           |          |
 first_name | character varying(50)  |           |          |
 last_name  | character varying(50)  |           |          |
 email      | character varying(150) |           |          |
 d_o_b      | date                   |           |          |


university_db=> INSERT INTO students
university_db-> VALUES (2,'uday','uday','uday@gmail.com','2003-10-13');
INSERT 0 1
university_db=> VALUES (3,'sheik','sheik','sheik@gmail.com','2004-11-20');


 column1 | column2 | column3 |     column4     |  column5
---------+---------+---------+-----------------+------------
       3 | sheik   | sheik   | sheik@gmail.com | 2004-11-20
(1 row)


university_db=> INSERT INTO students
university_db-> VALUES (3,'sheik','sheik','sheik@gmail.com','2004-11-20');
INSERT 0 1
university_db=> INSERT INTO students
university_db-> VALUES (4,'sai','sai','sai@gmail.com','2004-11-22');
INSERT 0 1
university_db=> INSERT INTO students
university_db-> VALUES (5,'god','god','god@gmail.com','2004-11-22');
INSERT 0 1
university_db=> SELECT * FROM students;


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          2 | uday       | uday      | uday@gmail.com         | 2003-10-13
          3 | sheik      | sheik     | sheik@gmail.com        | 2004-11-20
          4 | sai        | sai       | sai@gmail.com          | 2004-11-22
          5 | god        | god       | god@gmail.com          | 2004-11-22
(5 rows)


university_db=> SELECT * FROM students where student_id = 1;
 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
(1 row)


university_db=> SELECT first_name, last_name FROM students WHERE last_name = 'sai';
 first_name | last_name
------------+-----------
 sai        | sai
(1 row)


university_db=> SELECT * FROM students WHERE d_o_b >= '2004-07-2004';
ERROR:  date/time field value out of range: "2004-07-2004"
LINE 1: SELECT * FROM students WHERE d_o_b >= '2004-07-2004';
                                              ^
HINT:  Perhaps you need a different "datestyle" setting.
university_db=> SELECT * FROM students WHERE d_o_b >= '2004-07-12';


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          3 | sheik      | sheik     | sheik@gmail.com        | 2004-11-20
          4 | sai        | sai       | sai@gmail.com          | 2004-11-22
          5 | god        | god       | god@gmail.com          | 2004-11-22
(4 rows)


university_db=> SELECT * FROM students WHERE d_o_b BETWEEN '2002-01-01' and '2005-01-01';


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          2 | uday       | uday      | uday@gmail.com         | 2003-10-13
          3 | sheik      | sheik     | sheik@gmail.com        | 2004-11-20
          4 | sai        | sai       | sai@gmail.com          | 2004-11-22
          5 | god        | god       | god@gmail.com          | 2004-11-22
(5 rows)


university_db=> SELECT * FROM students WHERE first_name LIKE 'N%';


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
(1 row)


university_db=> SELECT * FROM students WHERE first_name LIKE 'n%';


 student_id | first_name | last_name | email | d_o_b
------------+------------+-----------+-------+-------
(0 rows)


university_db=> SELECT * FROM students WHERE first_name ILIKE 'n%';


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
(1 row)


university_db=> SELECT * FROM students WHERE student_id IN (1,3,5);


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          3 | sheik      | sheik     | sheik@gmail.com        | 2004-11-20
          5 | god        | god       | god@gmail.com          | 2004-11-22
(3 rows)


university_db=> INSERT INTO students (student_id,first_name,last_name,dob) VALUES
university_db-> (4,'Diana','Prince','2000-01-01');
ERROR:  column "dob" of relation "students" does not exist
LINE 1: ...RT INTO students (student_id,first_name,last_name,dob) VALUE...
                                                             ^
university_db=> INSERT INTO students (student_id,first_name,last_name,d_o_b) VALUES
university_db-> (4,'Diana','Prince','2000-01-01');
INSERT 0 1
university_db=> SELECT * FROM student WHERE student_id = 2;
ERROR:  relation "student" does not exist
LINE 1: SELECT * FROM student WHERE student_id = 2;
                      ^
university_db=> SELECT * FROM students WHERE student_id = 2;


 student_id | first_name | last_name |     email      |   d_o_b
------------+------------+-----------+----------------+------------
          2 | uday       | uday      | uday@gmail.com | 2003-10-13
(1 row)


university_db=> SELECT * FROM students WHERE d_o_b <= '2003-01-01';


 student_id | first_name | last_name | email |   d_o_b
------------+------------+-----------+-------+------------
          4 | Diana      | Prince    |       | 2000-01-01
(1 row)


university_db=> SELECT * FROM students WHERE first_name LIKE 'B%' OR first_name LIKE 'C%';


 student_id | first_name | last_name | email | d_o_b
------------+------------+-----------+-------+-------
(0 rows)


university_db=> SELECT * FROM students WHERE email LIKE '%example.com';


 student_id | first_name | last_name | email | d_o_b
------------+------------+-----------+-------+-------
(0 rows)


university_db=> SELECT * FROM students WHERE email IS NULL;
 student_id | first_name | last_name | email |   d_o_b
------------+------------+-----------+-------+------------
          4 | Diana      | Prince    |       | 2000-01-01
(1 row)


university_db=> UPDATE students
university_db-> SET email = 'newmail@gmail.com'
university_db-> WHERE student_id = 5;
UPDATE 1
university_db=> SELECT * FROM students;


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          2 | uday       | uday      | uday@gmail.com         | 2003-10-13
          3 | sheik      | sheik     | sheik@gmail.com        | 2004-11-20
          4 | sai        | sai       | sai@gmail.com          | 2004-11-22
          4 | Diana      | Prince    |                        | 2000-01-01
          5 | god        | god       | newmail@gmail.com      | 2004-11-22
(6 rows)


university_db=> UPDATE students
university_db-> SET student_id = 5
university_db-> WHERE first_name = 'Diana';
UPDATE 1
university_db=> UPDATE students
university_db-> SET student_id = 6
university_db-> WHERE first_name = 'god';
UPDATE 1
university_db=> SELECT * FROM students;


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          2 | uday       | uday      | uday@gmail.com         | 2003-10-13
          3 | sheik      | sheik     | sheik@gmail.com        | 2004-11-20
          4 | sai        | sai       | sai@gmail.com          | 2004-11-22
          5 | Diana      | Prince    |                        | 2000-01-01
          6 | god        | god       | newmail@gmail.com      | 2004-11-22
(6 rows)


university_db=> UPDATE students
university_db-> SET d_o_b = '2003-02-15'
university_db-> WHERE student_id = 3;
UPDATE 1
university_db=> UPDATE students
university_db-> SET email = 'Diana@gmail.com'
university_db-> WHERE first_name = 'Diane';
UPDATE 0
university_db=> UPDATE students
university_db-> SET email = 'Diana@gmail.com'
university_db-> WHERE first_name = 'Diana';
UPDATE 1
university_db=> SELECT * FROM students;


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          2 | uday       | uday      | uday@gmail.com         | 2003-10-13
          4 | sai        | sai       | sai@gmail.com          | 2004-11-22
          6 | god        | god       | newmail@gmail.com      | 2004-11-22
          3 | sheik      | sheik     | sheik@gmail.com        | 2003-02-15
          5 | Diana      | Prince    | Diana@gmail.com        | 2000-01-01
(6 rows)


university_db=> DELETE FROM students
university_db-> WHERE student_id = 99;
DELETE 0
university_db=> SELECT * FROM students ORDER BY last_name;


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          6 | god        | god       | newmail@gmail.com      | 2004-11-22
          5 | Diana      | Prince    | Diana@gmail.com        | 2000-01-01
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          4 | sai        | sai       | sai@gmail.com          | 2004-11-22
          3 | sheik      | sheik     | sheik@gmail.com        | 2003-02-15
          2 | uday       | uday      | uday@gmail.com         | 2003-10-13
(6 rows)


university_db=> SELECT * FROM students ORDER BY last_name DES C;
ERROR:  syntax error at or near "DES"
LINE 1: SELECT * FROM students ORDER BY last_name DES C;
                                                  ^
university_db=> SELECT * FROM students ORDER BY last_name DESC;


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          2 | uday       | uday      | uday@gmail.com         | 2003-10-13
          3 | sheik      | sheik     | sheik@gmail.com        | 2003-02-15
          4 | sai        | sai       | sai@gmail.com          | 2004-11-22
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          5 | Diana      | Prince    | Diana@gmail.com        | 2000-01-01
          6 | god        | god       | newmail@gmail.com      | 2004-11-22
(6 rows)


university_db=> SELECT * FROM students;


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          2 | uday       | uday      | uday@gmail.com         | 2003-10-13
          4 | sai        | sai       | sai@gmail.com          | 2004-11-22
          6 | god        | god       | newmail@gmail.com      | 2004-11-22
          3 | sheik      | sheik     | sheik@gmail.com        | 2003-02-15
          5 | Diana      | Prince    | Diana@gmail.com        | 2000-01-01
(6 rows)


university_db=> SELECT * FROM students ORDER BY D_O_B;


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          5 | Diana      | Prince    | Diana@gmail.com        | 2000-01-01
          3 | sheik      | sheik     | sheik@gmail.com        | 2003-02-15
          2 | uday       | uday      | uday@gmail.com         | 2003-10-13
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          4 | sai        | sai       | sai@gmail.com          | 2004-11-22
          6 | god        | god       | newmail@gmail.com      | 2004-11-22
(6 rows)


university_db=> SELECT * FROM students ORDER BY last_name DESC,first_name ASC;


 student_id | first_name | last_name |         email          |   d_o_b
------------+------------+-----------+------------------------+------------
          2 | uday       | uday      | uday@gmail.com         | 2003-10-13
          3 | sheik      | sheik     | sheik@gmail.com        | 2003-02-15
          4 | sai        | sai       | sai@gmail.com          | 2004-11-22
          1 | Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
          5 | Diana      | Prince    | Diana@gmail.com        | 2000-01-01
          6 | god        | god       | newmail@gmail.com      | 2004-11-22
(6 rows)


university_db=> SELECT * FROM students ORDER BY d_o_b LIMIT 2;


 student_id | first_name | last_name |      email      |   d_o_b
------------+------------+-----------+-----------------+------------
          5 | Diana      | Prince    | Diana@gmail.com | 2000-01-01
          3 | sheik      | sheik     | sheik@gmail.com | 2003-02-15
(2 rows)

                SELECT * FROM students ORDER BY student_id LIMIT 2 OFFSET 1;rsity_db=>
 student_id | first_name | last_name |      email      |   d_o_b
------------+------------+-----------+-----------------+------------
          2 | uday       | uday      | uday@gmail.com  | 2003-10-13
          3 | sheik      | sheik     | sheik@gmail.com | 2003-02-15
(2 rows)


university_db=> INSERT INTO students VALUES (7,'sheik','sheik','sheik@gmail.com','2003-01-02');
INSERT 0 1
university_db=> SELECT DISTINCT first_name, last_name, email, d_o_b FROM students;


 first_name | last_name |         email          |   d_o_b
------------+-----------+------------------------+------------
 sheik      | sheik     | sheik@gmail.com        | 2003-01-02
 Diana      | Prince    | Diana@gmail.com        | 2000-01-01
 god        | god       | newmail@gmail.com      | 2004-11-22
 sheik      | sheik     | sheik@gmail.com        | 2003-02-15
 uday       | uday      | uday@gmail.com         | 2003-10-13
 Nihaar     | Reddy     | nihaar.reddy@gmail.com | 2004-07-12
 sai        | sai       | sai@gmail.com          | 2004-11-22
(7 rows)


university_db=> SELECT DISTINCT first_name FROM students;
 first_name
------------
 sheik
 sai
 Diana
 uday
 god
 Nihaar
(6 rows)


university_db=> SELECT DISTINCT first_name, last_name FROM students;
 first_name | last_name
------------+-----------
 god        | god
 Diana      | Prince
 sheik      | sheik
 sai        | sai
 Nihaar     | Reddy
 uday       | uday
(6 rows)


university_db=> SELECT COUNT(*) AS total_count FROM students;
 total_count
-------------
           7
(1 row)


university_db=> SELECT COUNT(email) AS student_with_email FROM students;
 student_with_email
--------------------
                  7
(1 row)


university_db=> SELECT COUNT(DISTINCT last_name) AS Unique_last_name FROM students;
 unique_last_name
------------------
                6
(1 row)


university_db=> SELECT last_name, COUNT(*) AS number_of_students \FROM students
invalid command \FROM
Try \? for help.
university_db-> SELECT last_name, COUNT(*) AS number_of_students FROM students
university_db-> GROUP BY last_name
university_db-> ORDER BY student_id DESC;
ERROR:  syntax error at or near "SELECT"
LINE 2: SELECT last_name, COUNT(*) AS number_of_students FROM studen...
        ^
university_db=> SELECT last_name, COUNT(*) AS number_of_students FROM students
university_db-> GROUP BY last_name
university_db-> ORDER BY student_id DESC;
ERROR:  column "students.student_id" must appear in the GROUP BY clause or be used in an aggregate function
LINE 3: ORDER BY student_id DESC;
                 ^
university_db=> SELECT last_name, COUNT(*) AS number_of_students FROM students
university_db-> GROUP BY last_name
university_db-> ORDER BY number_of_students DESC;
 last_name | number_of_students
-----------+--------------------
 sheik     |                  2
 sai       |                  1
 Reddy     |                  1
 uday      |                  1
 god       |                  1
 Prince    |                  1
(6 rows)


university_db=> SELECT last_name, COUNT(*) AS number_of_students
university_db-> FROM students
university_db-> GROUP BY last_name
university_db-> HAVING COUNT(*) > 1
university_db-> ORDER BY number_of_students DESC;


 last_name | number_of_students
-----------+--------------------
 sheik     |                  2
(1 row)


university_db=> SELECT first_name, COUNT(*) AS number_of_students
university_db-> FROM students
university_db-> GROUP BY first_name
university_db-> ;


 first_name | number_of_students
------------+--------------------
 sheik      |                  2
 sai        |                  1
 Diana      |                  1
 uday       |                  1
 god        |                  1
 Nihaar     |                  1
(6 rows)


university_db=> DROP TABLE IF EXISTS students;
DROP TABLE
university_db=> \d students;
Did not find any relation named "students".
university_db=> CREATE TABLE students (
university_db(> student_id INTEGER,
university_db(> first_name VARCHAR(50) NOT NULL,
university_db(> last_name VARCHAR(50) NOT NULL,
university_db(> email VARCHAR(100) UNIQUE,
university_db(> dob DATE,
university_db(> enrollment_status VARCHAR(10) CHECK (enrollment_status IN ('enrolled','graduated','dropped'))
university_db(> );
CREATE TABLE
university_db=> INSERT INTO students
university_db-> VALUES
university_db-> (1,'Test','test;
university_db'> );
university_db'> ;
university_db'> ';
university_db(> );
ERROR:  syntax error at or near ";"
LINE 6: ';
         ^
university_db=> INSERT INTO students (student_id, last_name, email, dob)
university_db-> VALUES (1,'Test','test@gmail.com','2000-09-09');
ERROR:  null value in column "first_name" of relation "students" violates not-null constraint
DETAIL:  Failing row contains (1, null, Test, test@gmail.com, 2000-09-09, null).
university_db=> INSERT INTO students
university_db-> VALUES
university_db-> (1,'Test','User','test@gmail.com','2003-01-09');
INSERT 0 1
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob) VALUES (2, 'Another', 'User', 'test@test.com', '2001-01-01');
INSERT 0 1
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob) VALUES (2, 'Another', 'User', 'test@gmail.com', '2001-01-01');
ERROR:  duplicate key value violates unique constraint "students_email_key"
DETAIL:  Key (email)=(test@gmail.com) already exists.
university_db=> INSERT INTO students (student_id, first_name, last_name, email, dob, enrollment_status) VALUES (2, 'Another', 'User', 'another@test.com', '2001-01-01', 'pending');
ERROR:  new row for relation "students" violates check constraint "students_enrollment_status_check"
DETAIL:  Failing row contains (2, Another, User, another@test.com, 2001-01-01, pending).
university_db=> SELECT * FROM students;
 student_id | first_name | last_name |     email      |    dob     | enrollment_status
------------+------------+-----------+----------------+------------+-------------------
          1 | Test       | User      | test@gmail.com | 2003-01-09 |
          2 | Another    | User      | test@test.com  | 2001-01-01 |
(2 rows)


university_db=> DROP TABLE IF EXISTS students;
DROP TABLE
university_db=> CREATE TABLE students (
university_db(> student_id SERIAL PRIMARY KEY,
university_db(> first_name VARCHAR(50) NOT NULL,
university_db(> last_name VARCHAR(50) NOT NULL,
university_db(> email VARCHAR(100) UNIQUE,
university_db(> dob DATE,
university_db(> enrollment_status VARCHAR(20) CHECK (enrollment_status IN ('enrolled','graduated','dropped','pending')));
CREATE TABLE
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Alice', 'smith', 'alice.smith@example.com','2000-9-08','enrolled');
INSERT 0 1
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Border', 'land', 'Border.land@example.com','2000-9-08','enrolled');
INSERT 0 1
university_db=> INSERT INTO students (first_name, last_name, email, dob, enrollment_status)
university_db-> VALUES ('Steves', 'jobs', 'Steves.jobs@example.com','2004-12-12','enrolled');
INSERT 0 1
university_db=> SELECT * FROM students;
 student_id | first_name | last_name |          email          |    dob     | enrollment_status
------------+------------+-----------+-------------------------+------------+-------------------
          1 | Alice      | smith     | alice.smith@example.com | 2000-09-08 | enrolled
          2 | Border     | land      | Border.land@example.com | 2000-09-08 | enrolled
          3 | Steves     | jobs      | Steves.jobs@example.com | 2004-12-12 | enrolled
(3 rows)


university_db=> CREATE TABLE courses (
university_db(> course_id SERIAL PRIMARY KKAY;
university_db(> );
ERROR:  syntax error at or near "KKAY"
LINE 2: course_id SERIAL PRIMARY KKAY;
                                 ^
university_db=> CREATE TABLE courses (
university_db(> course_id SERIAL PRIMARY KEY,
university_db(> course_name VARCHAR(100) NOT NULL UNIQUE,
university_db(> credits INTEGER CHECK (credits > 0 AND CREDITS < 10));
CREATE TABLE
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Introduction to SQL', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Database Design', 4);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Web Development', 3);
INSERT 0 1
university_db=> INSERT INTO courses (course_name, credits) VALUES ('Data Structures', 4);
INSERT 0 1
university_db=> CREATE TABLE enrollments (
university_db(> enrollment_id SERIAL PRIMARY KEY,
university_db(> student_id INTEGER NOT NULL,
university_db(> course_id INTEGER NOT NULL,
university_db(> enrollment_date DATE DEFAULT CURRENT_DATE,
university_db(> grade CHAR(1) CHECK (grade IN ('A', 'B', 'C', 'D', 'F', 'W', NULL)),
university_db(> CONSTRAINT fk_student
university_db(> FOREIGN KEY (student_id) REFERENCES students(student_id) ON DELETE CASCADE,
university_db(> CONSTRAINT fk_course
university_db(> FOREIGN KEY (course_id) REFERENCES courses(course_id) ON DELETE RESTRICT,
university_db(> UNIQUE (student_id, course_id));
CREATE TABLE
university_db=> SELECT * FROM courses;
 course_id |     course_name     | credits
-----------+---------------------+---------
         1 | Introduction to SQL |       3
         2 | Database Design     |       4
         3 | Web Development     |       3
         4 | Data Structures     |       4
(4 rows)


university_db=> INSERT INTO enrollments
university_db-> VALUES (999, 2, 'A');
ERROR:  invalid input syntax for type integer: "A"
LINE 2: VALUES (999, 2, 'A');
                        ^
university_db=> INSERT INTO enrollments (student_id, course_id, grade)
university_db-> VALUES (999, 2, 'A');
ERROR:  insert or update on table "enrollments" violates foreign key constraint "fk_student"
DETAIL:  Key (student_id)=(999) is not present in table "students".
university_db=> SELECT * FROM students;
 student_id | first_name | last_name |          email          |    dob     | enrollment_status
------------+------------+-----------+-------------------------+------------+-------------------
          1 | Alice      | smith     | alice.smith@example.com | 2000-09-08 | enrolled
          2 | Border     | land      | Border.land@example.com | 2000-09-08 | enrolled
          3 | Steves     | jobs      | Steves.jobs@example.com | 2004-12-12 | enrolled
(3 rows)


university_db=> INSERT INTO emrollments (student_id, course_id, grade) VALUES
university_db-> (1,5,'A');
ERROR:  relation "emrollments" does not exist
LINE 1: INSERT INTO emrollments (student_id, course_id, grade) VALUE...
                    ^
university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES
university_db-> (1,5,'A');
ERROR:  insert or update on table "enrollments" violates foreign key constraint "fk_course"
DETAIL:  Key (course_id)=(5) is not present in table "courses".
university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES
university_db-> (1,1,'A');
INSERT 0 1
university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES
university_db-> (1,2);
ERROR:  INSERT has more target columns than expressions
LINE 1: INSERT INTO enrollments (student_id, course_id, grade) VALUE...
                                                        ^
university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES
university_db-> (1,2,'NULL');
ERROR:  value too long for type character(1)
university_db=> (1,2);
ERROR:  syntax error at or near "1"
LINE 1: (1,2);
         ^
university_db=> INSERT INTO enrollments (student_id, course_id, grade) VALUES
university_db-> (1,2);
ERROR:  INSERT has more target columns than expressions
LINE 1: INSERT INTO enrollments (student_id, course_id, grade) VALUE...
                                                        ^
university_db=> INSERT INTO enrollments (student_id, course_id) VALUES
university_db-> (1,2);
INSERT 0 1
university_db=> SELECT * FROM enrollments;
 enrollment_id | student_id | course_id | enrollment_date | grade
---------------+------------+-----------+-----------------+-------
             3 |          1 |         1 | 2025-05-30      | A             4 |          1 |         2 | 2025-05-30      |
(2 rows)


university_db=> grade CHAR(1) CHECK (grade IN ('A', 'B', 'C', 'D', 'F', 'W', NULL))
