# Postgres 
![postgres](https://www.ovhcloud.com/sites/default/files/styles/text_media_horizontal/public/2021-09/ECX-1909_Hero_PostgreSQL_600x400%402x.png)

#### What is a database
 It's a structured collection of data that is organized, stored, and managed to do CRUD operations 

#### What is DBMS
 It stands for Data Base Management System. It's the software that allows CRUD operations. Eg:- MySQL, PostgreSQL

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
BEGIN TRANSACTION;

UPDATE account SET balance = balance -100 WHERE no = '123';
UPDATE account SET balance = balance -200 WHERE no = '321';

COMMIT;

```

> `BEGIN` and `START` has the same functionality

#### Objects
The various database components that store and manage data, such as tables, indexes, functions, etc

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

#### Constraints
Rules that can apply to a column

<p align="left">
  <img src="https://static.javatpoint.com/postgre/images/postgresql-constraints.png" />
</p>

- **Primary Key** : Unique identifier of a row, not null and unique
```sql
CREATE TABLE student(
key SERIAL PRIMARY KEY);
```

- **Unique**: The col contains only unique values
```sql
CREATE TABLE hello(
key INT UNIQUE );
```

- **Not null**: Col can't have null values
```sql
CREATE TABLE hello(
key INT NOT NULL );
```

- **Foreign key** : All values in this column match the value in the other table's column
```sql
CREATE TABLE hello(
key SERIAL PRIMARY KEY,
name VARCHAR(30) REFERENCES customers(name)
);
```

- **Check constraint**: A condition that applies to the data in a column
```sql
CREATE TABLE hello(
key SERIAL PRIMARY KEY,
age INT CHECK (age >= 18)
);
```

- **Exclusion** : It evaluates the comparison of 2 rows in a table
```sql
CREATE TABLE company(
name TEXT,
age INT,
EXCLUDE USING  gist (name WITH =, age WITH <>)
);
```
> Maybe you need to execute the command `CREATE EXTENTION btree_gist`, once per db

#### Main Datatypes 
There are plenty of data types in PostgreSQL. Here are some
<p align="left">
  <img src="https://static.javatpoint.com/postgre/images/postgresql-data-types.png" />
</p>

- **Integer** : 1,4,-2 ...
- **numeric(whole num, floating count)** : 1.42, 4.345
- **bigint** : stores big values
- **real** : wide variety of numbers
- **varchar(n)** : variable-length character string.
- **text** : varchar with no defined length
- **date** : stores date value
- **time** : stores a time of day.
- **timestamp** : stores time and date
- **boolean** : true or false
- **serial** : auto-increment integer
- **json** : stores JSON data
- **jsonb** : binary representation of JSON data
- **UUID** : (Universally Unique Identifiers) Designed to be unique.

#### Clauses
It is the special keyword used in SQL to perform various queries.

- **SELECT** : Used to fetch data from the table
```sql
SELECT col1, col2 FROM table1;
```
```sql
SELECT * FROM table2;
```
```sql
SELECT DISTINCT country FROM customers;
```

- **WHERE** : Filter data based on specific conditions.
```sql
SELECT * FROM orders WHERE date > '2023-01-01'
```

- **ORDER BY** : Used to sort the result set in ascending (default) descending if add `DESC`
```sql
SELECT name, age FROM students ORDER BY age DESC;
```

- **GROUP BY** : Used to group rows that have the same value in specific columns. It often uses SUM, AVG
```sql
SELECT id, SUM(price) AS avg FROM products;
```

- **HAVING** : Used to specify conditions for aggregate values.
```sql
SELECT id, AVG(price) AS avg FROM products GROUP BY id HAVING AVG(price) > 3
```
- **JION** : Used to combine rows from two or more tables based on related columns
	- **INNER JOIN** : returns only the rows that have matching values in both tables.
	```sql
	SELECT Customers.name, Orders.date FROM Customers INNER JOIN Orders ON Customers.id =  Orders.id;
	```
	
	 - **LEFT JOIN** : It's actually `LEFT OUTER JOIN` that return the left table that matches rows in the left table
	```sql
	SELECT Customers.name, Orders.date FROM Customers LEFT JOIN Orders ON Customers.id  = Orders.id;
	```
	
	- **RIGHT JOIN** : It's actually `RIGHT OUTER JOIN` that returns the right table that matches rows in the right table
	```sql
	SELECT Customers.name, Orders.date FROM Customers RIGHT JOIN Orders ON Customers.id = Orders.id;
	```
	
	- **FULL JOIN** : It's actually `LEFT OUTER JION` that returns all rows from both tables and fill in NULL values where no match.
	```sql
	SELECT Customers.name, Orders.date FROM Customers FULL JOIN Orders ON Customers.id = Orders.id;
	```
	
	- **CROSS JOIN** : Combines every row from one table with every row from another table
	```sql
	SELECT * FROM Customers CROSS JOIN Products;
	```

#### CRUD operations
<p align="left">
  <img src="https://static.javatpoint.com/sqlpages/images/crud-operations-in-sql1.jpg" />
</p>

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
WHERE brand = 'Banz' ;
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

<p align="left">
  <img height=300px src="https://preview.redd.it/mdt46lpf413a1.jpg?width=960&crop=smart&auto=webp&s=7cb5d2daf3b6d68ff8d8093c7f942adadee035da" />
</p>

>`DELETE` without `WHERE` removes all the records in a table

- **TRUNCATE** : Remove all the rows in a table
```sql
TRUNCATE TABLE table1
```

#### Operators
<p align="left">
  <img src="https://cdn.educba.com/academy/wp-content/uploads/2020/03/Comparison-Operators-in-SQL.png" />
</p>
We can use different operators after the `WHERE` clause

- `=` equal to
- `<` less than
- `>` greater than
- `<=` less than or equal to
- `>=` greater than or equal to
- `<>` and `!=` not equal to 
- `LIKE` check if the value matches a pattern
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
- `EXISTS` used to test anything in sub-query *It only returns a boolean*
```sql
SELECT name FROM customers 
WHERE EXISTS(
SELECT id FROM orders WHERE id=costomers.id);
```
- `ANY` compare between a single column value and a range value *only returns a boolean*
```sql
SELECT name FROM products 
WHERE id = ANY(
SELECT id FROM customers);
```
- `ALL` compare between a single column value and a range value *only return boolean* and can be used with `SELECT`,`WHERE`,`HIVING`
```sql
SELECT name FROM employees 
WHERE age = ALL(
SELECT age FROM admins);
```

#### Aliasing
Giving a temporary name to a table or column with `AS`

<p align="left">
  <img src="https://s33046.pcdn.co/wp-content/uploads/2020/02/using-sql-as-keyword-and-join-clause--624x335.png" />
</p>

```sql
SELECT first_name AS name FROM Customers;
```

#### CASE expression
It is like an if-then-else statement in SQL
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
It is special functions in SQL that allow performing operations
<p align="left">
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*ru43ZSkVFHrJw3n9sLjBHA.jpeg" />
</p>

- **SUM()** :
```sql
SELECT SUM(price) FROM sales;
```
- **AVG()** :
```sql
SELECT AVG(price) FROM sales;
```
- **COUNT()** : Calculate count, syntax is same as `SUM`
- **MIN()**
- **MAX()**
- **BOOL_AND()** : arguments and return value are bool
- [More inbuilt aggregate functions](https://www.postgresql.org/docs/9.5/functions-aggregate.html)

#### Scalar Functions
Type of functions that take one or more argument and return one argument.
```sql
SELECT UPPER(name) AS uppercase_name FROM employees;
```

#### Role
A concept that controls access and permission for users and groups. 2 types of roles out there
1. **User Roles** : There are roles that correspond to individual users.

```sql
CREATE ROLE myuser LOGIN PASSWORD 'mypassword';
```
this creates a user role named `myuser` with a password. After that, we are granting the privileges to the user in the following code
```sql
GRAND SELECT, INSERT ON mytable TO myuser;
```

2. **Group Roles** : Also known as *role membershp*, these are roles that can have other roles as members

```sql
CREATE ROLE mygroup;
```

Assigning privileges -
```sql
GRAND CREATE ON DATABASE  db_name TO mygroup;
```

#### Grand
<p>
<img height=200 src='https://thumbs.dreamstime.com/b/grants-red-vector-rubber-stamp-grant-grunge-white-background-illustration-145921446.jpg'/>
</p>

It refers to the process of giving specific privileges or permission to users or roles on database objects

```sql
GRAND SELECT ON employees TO report_viewer;
```
In this example, it allows the `report_viewer` to read data but not modify it

```sql
GRANT SELECT ON ALL TABLES IN SCHEMA public TO same_role;
```
This grants the `SELECT` privilege on all tables in the `public` schema

> **Scalar functions** work on individual values within a row. <br>
> **Aggregate functions** work on a group of rows to produce summary values

#### Closure
The closure allows a function to "remember" the values of variables that were present when the function created, even if the variables are no longer available

#### DML, DDL, DCL

- **DML** : It's stands for *Data Manipulation Language*. A category of SQL statements that are used to manage and manipulate data in DB. Eg :- `INSERT`

- **DDL** : Stands for *Data definition Language*. Set of commands that are used to define and manage the structure of DB. Eg :- `CREATE TABLE`

- **DCL** : Stands for *Data Control Languge*. Managing permissions and access control of database objects.

#### Triggers

<p align="left">
   <img src="http://pages.di.unipi.it/ghelli/didattica/bdldoc/B19306_01/server.102/b14220/img/cncpt076.gif" />
</p>

It can automatically execute a set of actions whenever a specific event occurs

- **Creating Triggers** :
  
```sql
CREATE TRIGGER my_trigger 
AFTER INSERT ON my_table
FOR EACH ROW
EXECUTE FUNCTION my_function();
```

- **Trigger Functions** :
  
```sql
CREATE FUNCTION my_function() RETURNS
TRIGGER AS $$
BEGIN 
	INSERT INTO audit_log(action, table_name, changed_row_id)
	VALUES ('INSERT', TG_TABLE_NAME, NEW.id);
	RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```

- **Types of Triggers** : 
 - *BEFORE Triggers* : Fire before the actual data modification.
 - *AFTER Triggers* : Fire after the data modification.
 - *INSTEAD OF Trigger* : Used with views

#### View
<p align="left">
  <img src="https://static.javatpoint.com/sqlserver/images/view-in-sql-server.png" />
</p>

Save query that you can treat as a table.

```sql
CREATE VIEW order_counts AS
SELECT customers.id, customers.name, 
COUNT(orders.id) AS total_orders
FROM customers
LEFT JOIN orders ON customers.id = 
orders.id
GROUP BY customers.id,
customers.name;
```

Now, we can view the named `order_counts` that behaves like a table.
```sql
SELECT * FROM order_counts;
```

#### Indexes
<p align="left">
  <img src="https://miro.medium.com/v2/resize:fit:1400/0*4W8c1ne0Ny0Myy1f.png" />
</p>
Way to optimize the retrieval of data from a database table

```sql
CREATE INDEX idx_last_name ON table_name(last_name);
```

#### Privileges
It control who can access or modify certain DB objects like tables, views, and functions.

```sql
GRAND SELECT ON table_name TO user_or_role;
```

```sql
GRAND ALL ON table_name TO user_or_all;
```

*to remove privileges -*
```sql
REVOKE INSERT ON table_name FROM user_name;
```

#### CASCADE
It used in the context of foreign key context
- **DELETE Cascade** : set `ON DELETE CASECADE` in the child table, then all related records in the child table will delete automatically when delete than in parent table
```sql
CREATE TABLE parent (
parent_id SERIAL PRIMARY KEY
);

CREATE TABLE child(
id SERIAL PRIMARY KEY,
second_id INTEGER REFERENCES parent(id) ON DELETE CASCADE
);
```

- **UPDATE Cascade** : similar to above
```sql
CREATE TABLE orders (
id SERIAL PRIMARY KEY,
cost_id INTEGER REFERENCES customers(id) ON UPDATE CASCADE
);

CREATE TABLE customers(
id SERIAL PRIMARY KEY,
name TEXT
);
```

#### Concurrency
It is the ability of multiple transactions or processes to occur simultaneously without causing conflicts.

Techniques to handle concurrency
1. **Locking** : Involve temporary blocking of access
2. **Isolation Levels** : Define the extent to which transactions are isolated from each other.

#### Locks
Restricts users from modifying a row or a table's content.

- **Shared Lock**
- **Exclusive Lock**
- **Row Level Lock**	
- **Table Level Lock**
- **Page-level Lock**
- **Lock modes**

#### Normalization
<p align="left">
  <img height=300px src="https://img.freepik.com/free-vector/kanban-method-concept-illustration_114360-9827.jpg?w=1380&t=st=1692363376~exp=1692363976~hmac=49034bc72f8ef9fa029d1fd40578636b2bcbdae9e64a9eb43d6654819ab08caa" />
</p>
It refers to the way of organizing the data in a database. There are different *normal forms* that define the level of normalization.
> Normal forms are rules or guidelines that help organize and structure data in a way that reduces redundancy(having the same copies) and improves integrity

1. **First Normal Form (1NF)** : Each column in a table must hold only atomic (indivisible) values, and each row should be unique
> If a cell contains multiple values, then it violates the rule

2. **Second Normal Form (2NF)** : The table must be in 1NF and each non-primary key column must be fully functionally dependent on the primary key
> Primary key should have some relation with each column values

3. **Third Normal Form (3NF)** : The table must be in 2NF and no non-primary key column should depend on another non-primary key column *(transitive dependency)*

#### With 
Used to create Common Table Expressions (CTE)
> `CTE` is a temporary result set that can refer to SELECT, INSERT ...
> It makes complex queries more readable
```sql
WITH DepCount AS (
   SELECT id ,COUNT(*) AS emp_count FROM employees
)

SELECT * FROM DepCount;
```
#### Relations
<p align="left">
  <img src="https://media.istockphoto.com/id/1352564117/vector/database-sql-structured-query-language-people-team-discuss-coding-for-storing-data-in-server.jpg?s=612x612&w=0&k=20&c=eRlvikJYlY8tJ8pVxgZFUv5GLgQbTy_rq18jKLZxq8A=" />
</p>
It can be made with `FOREIGN KEY`

- **One-to-one** : One row in a table is associated with exactly one row in another table
- **One-to-many** : One row is associated with multiple rows in another table
- **Many-to_many** : Multiple rows in a table associated with multiple rows in another table

#### 3 Schema Architecture
also known as the ANSI-SPARC architecture, is a way to organize and manage data in a database system.

1. **External Schema (User View)**:
   This is the schema that users interact with directly.
   ```sql
	SELECT student_name, course_name, grade
	FROM student_grades;
   ```

2. **Conceptual Schema (Logical View)**:
   This schema represents the overall logical structure of the entire database, including the relationships between different pieces of data.
   ```
   CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50)
   );

   CREATE TABLE Courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100)
   );

   CREATE TABLE Grades (
    student_id INT,
    course_id INT,
    grade CHAR(1),
    PRIMARY KEY (student_id, course_id)
   );
   ```

3. **Internal Schema (Physical View)** :
   This is the lowest level of schema, dealing with how the data is physically stored on the hardware. 


