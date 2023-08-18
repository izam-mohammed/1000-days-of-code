# Postgres 
![postgres](https://www.ovhcloud.com/sites/default/files/styles/text_media_horizontal/public/2021-09/ECX-1909_Hero_PostgreSQL_600x400%402x.png)

#### What is a database
It's a structured collection of data that is organized, stored, and managed to do CRUD operations

#### What is DBMS
It stands for Data Base Management System. It's the software that allows CRUD operations.
Eg :- MySQL , PostgreSQL

#### Difference between DBMS and RDBMS
In DBMS, the data is stored as a file, whereas in RDBMS, the data is stored in the form of tables

#### Benefits of Postgres
- Open-source and community-driven
- SQL database
- Have advanced features
- Extensibility - allows you to create your own things
- It follows ACID complaints
- Scalability and data integrity

#### Transactions
A group of tasks like insert, update, etc

```SQL
BEGIN TRANSACTION

UPDATE account SET balance = balance -100 WHERE no = '123';
UPDATE account SET balance = balance -200 WHERE no = '321';

COMMIT;

```

#### ACID properties
Its 4 properties of a robust (well-designed and reliable for CRUD)  database
![acid](https://static.javatpoint.com/dbms/images/acid-properties-in-dbms.png)

1. **Atomacity**: All operations in a transaction are either completed or none of them applied at all.
2. **Consistency**: DB should follow predefined rules like `this column should be int`
3. **Isolation**: Each transaction is isolated from others like the scope of a variable
4. **Durability**: Once the transaction is committed, then changes are permanent securely

#### Query 
Request to retrieve or manipulate data stored in a DB
Eg:-
```SQL
SELECT * FROM employee WHERE age>30;
```

#### Table
Collection of related data held in a table format. Table have **rows** and **columns**

#### Constaints
Rules that can apply to a column
![constraints](https://static.javatpoint.com/postgre/images/postgresql-constraints.png)

- **Primary Key** : Unique indentifier of a row, not null and unique
```sql
CREATE TABLE stdent(
key SERIAL PRIMARY KEY);
```

- **Unique**: The col contain only unique values
```sql
CREATE TABLE hello(
key INT UNIQUE );
```

- **Not null**: Col can't have null values
```sql
CREATE TABLE hello(
key INT NOT NULL );
```

- **Foreign key** : All values in this column match value in other table's column
```sql
CREATE TABLE hello(
key SERIAL PRIMARY KEY,
name VARCHAR(30) REFERENCES costomers(name)
);
```

- **Check constraint**: A condition that apply for the data in a column
```sql
CREATE TABLE hello(
key SERIAL PRIMARY KEY,
age INT CHECK (age >= 18)
);
```

- **Exclusion** : It evaluate comparison of 2 rows in a table
```sql
CREATE TABLE company(
name TEXT,
age INT,
EXCLUDE USING  gist (name WITH =, age WITH <>)
);
```
> Maybe you need to execute the command `CREATE EXTENTION btree_gist`, once per db

#### Main Datatypes 
There are plenty of data types in postgreSQL. Here are some
![dtypes](https://static.javatpoint.com/postgre/images/postgresql-data-types.png)

- **Integer** : 1,4,-2 ...
- **numeric(whole num, floating count)** : 1.42, 4.345
- **bigint** : stores big values
- **real** : wide variety of numbers
- **varchar(n)** : variable-length character string.
- **text** : varchar with no defind length
- **date** : stores date value
- **time** : stores a time of day.
- **timestamp** : stores time and date
- **boolean** : true or false
- **serial** : auto increment integer
- **json** : stores json data
- **jsonb** : binary representation of json data
- **UUID** : (Universally Unique Identifiers) Designed to be unique.

#### Clauses
It is special keywords used in SQL to perform various query.

- **SELECT** : Used to fetch data from table
```sql
SELECT col1, col2 FROM table1;
```
```sql
SELECT * FROM table2;
```
```sql
SELECT DISTINCT coutry FROM customers;
```

- **WHERE** : Filter data based on specific condition.
```sql
SELECT * FROM orders WHERE date > '2023-01-01'
```

- **ORDER BY** : Used to sort the result set in ascending (default) descending if add `DESC`
```sql
SELECT name, age FROM students ORDER BY age DESC;
```

- **GROUP BY** : Used to group rows that have the same value in specific columns. It often use SUM,AVG
```sql
SELECT id, SUM(price) AS avg FROM products;
```

- **HAVING** : Used to specify condition for aggregate values.
```sql
SELECT id, AVG(price) AS avg FROM products GROUP BY id HAVING AVG(price) > 3
```
- **JION** : Used to combine rows from two or more table based on related columns
 - **INNER JOIN** : returns only the rows that have matching values in both tables.
```sql
SELECT Customers.name, Orders.date FROM Customers INNER JOIN Orders ON Customers.id =  Orders.id;
```

 - **LEFT JOIN** : Its actually `LEFT OUTER JOIN` that return left table that matching rows in the left table
```sql
SELECT Customers.name, Orders.date FROM Customers LEFT JOIN Orders ON Customers.id  = Orders.id;
```

- **RIGHT JOIN** : Its actually `RIGHT OUTER JOIN` that return right table that matching rows in the right table
```sql
SELECT Customers.name, Orders.date FROM Customers RIGHT JOIN Orders ON Customers.id = Orders.id;
```

- **FULL JOIN** : Its actually `LEFT OUTER JION` that return all rows from both tables and fill in NULL values where no match.
```sql
SELECT Customers.name, Orders.date FROM Customers FULL JOIN Orders ON Customers.id = Orders.id;
```

- **CROSS JOIN** : Combines every row from one table with every row from another table
```sql
SELECT * FROM Customers CROSS JOIN Products;
```

#### CRUD operations
![CRUD](https://static.javatpoint.com/sqlpages/images/crud-operations-in-sql1.jpg)

- **CREATE** : 
```sql
CREATE DATABASE hola;
```
```sql
CREATE TABLE costumers(
id INT PRIMARY KEY,
name VARCHAR(50),
age INT CHECK (age >18)
);
```

- **INSERT INTO** : 
```sql
INSERT INTO cars(brand, model) VALUES ('tesla' ,'gt');
```

- **ALTER** :
```sql
ALTER TABLE hola ADD color VARCHAR(30);
```
```sql
ALTER TABLE hola ALTER color TYPE VARCHAR(20);
```

- **UPDATE** :
```sql
UPDATE cars
SET color = 'red'
WHERE brand = 'banz' ;
```

- **DROP** :
```sql
DROP DATABASE hola;
```
```sql
DROP TABLE table1 ;
```
```sql
ALTER TABLE cars DROP COLUMN model ;
```

- **DELETE** : for delete row
```sql
DELETE FROM cars WHERE brand='volvo';
```

- **TRUNCATE** : Remove all the rows in a table
```sql
TRUNCATE TABLE table1
```

#### Operators
We can use different operators after `WHERE` clause

- `=` eqal to
- `<` less than
- `>` greater than
- `<=` less than or equal to
- `>=` greater than or equal to
- `<>` and `!=` not equal to 
- `LIKE` check if value matches a pattern
 - `_` represents one character
 - `%` represents n number of characters
```sql
SELECT * FROM cars WHERE model LIKE '__ha%';
```
- `ILIKE` same as `LIKE` but Case sensitive
- `AND`, `OR`
- `IN` and `BETWEEN` checks the value in that particular range
- `IS NULL` check null or not
- `NOT` make negative results
- `UNION` combine 2 result set
```sql
SELECT id ,name FROM products 
UNION
SELECT id, name FROM customers
;
```
- `EXISTS` used to test anything in sub-query *It only returns boolean*
```sql
SELECT name FROM customers 
WHERE EXISTS(
SELECT id FROM orders WHERE id=costomers.id);
```
- `ANY` compare between a single column value and a range values *only returns boolean*
```sql
SELECT name FROM products 
WHERE id = ANY(
SELECT id FROM costumers);
```
- `ALL` compare between a single column val and a range value *only return boolean* and can be used with `SELECT`,`WHERE`,`HIVING`
```sql
SELECT name FROM employees 
WHERE age = ALL(
SELECT age FROM admins);
```

#### Aliasing
Giving temporary name to a table or column with `AS`
```sql
SELECT first_name AS name FROM Customers;
```

#### CASE expression
It is like an if-then-else statement in sql
```sql
SELECT product, 
CASE
  WHEN price <30 THEN 'low'
  WHEN price >50 THEN 'high'
ELSE
  'normal'
END AS level
FROM products;
```

#### Aggregate Functions
It is special functions in SQL that allow to perform operations
![aggregate](https://miro.medium.com/v2/resize:fit:640/format:webp/1*ru43ZSkVFHrJw3n9sLjBHA.jpeg)

- **SUM()** :
```sql
SELECT SUM(price) FROM sales;
```
- **AVG()** :
```sql
SELECT AVG(price) FROM sales;
```
- **COUNT()** : Calculate count , syntax is same as `SUM`
- **MIN()**
- **MAX()**
- **BOOL_AND()** : argumets and return value are bool
- [More inbuilt aggregate functions](https://www.postgresql.org/docs/9.5/functions-aggregate.html)

#### Scalar Functions
#### Closure
#### DML,DDL,DCL
#### Triggers
#### Indexes
#### Schema
#### previlages
#### View
#### CASECADE
#### Locks
#### Normalization
#### Relations
#### 3 Schema Architecture
#### Concurrency
#### With python
