# Postgres 🐘
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
