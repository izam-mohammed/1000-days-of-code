# Postgres 
![postgres](https://www.ovhcloud.com/sites/default/files/styles/text_media_horizontal/public/2021-09/ECX-1909_Hero_PostgreSQL_600x400%402x.webp)


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


- **Primary Key** : Unique indentifier of a column, not null and unique
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
SELECT id, AVG(price) AS avg FROM products GROUP BY id HAVING AVG(price) > 3```




