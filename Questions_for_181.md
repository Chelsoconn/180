1) ```sql 
   CREATE TABLE students 
   ( id serial PRIMARY KEY, 
    name text ); 
    
   CREATE TABLE classes 
   ( id serial PRIMARY KEY, 
    name text, 
    student_id int REFERENCES students (id) ); 
    
    INSERT INTO students (name) VALUES ('Johny'), ('Edd'); 
    INSERT INTO classes (name, student_id)  VALUES ('Math', 1), ('Art', NULL), ('Geography', 1);
   ```

**Will the code result in an error if we attempt to insert `NULL` to a `student_id` column?**

As we can see, the table `classes` defines `student_id` as a foreign key that references the primary key `id` from the students table. A foreign key is an attribute that completes a relationship by identifying the parent entity.  By setting an attribute as a foreign key we can maintain referential integrity in that it ensures that a record must reference an existing value.  Table relationships must always be consistent, and you cannot add a value to a foriegn key column unless it already exists in the referenced column. 

While a primary key is equivalent to adding `NOT NULL` and `UNIQUE` constraints, a foreign key does not inherently add these same constraints.  While it may be wise to define your own `NOT NULL` constraint to the foreign key column, there may be cases where this is not ideal.  For example, if you want to have a class with no current students, a `NULL` value could be useful as a default value of `0` can cause errors in calculations, say in average students per class.  To clarify, aggregate functions will ignore `NULL` values (except for `COUNT(*)`). 

Coming back to our question, we can see that adding the `NULL` value to the `student_id` column would not result in an error, as there was not a `NOT NULL` constraint defined in this foreign key column.



```sql
CREATE TABLE teachers (
	id serial PRIMARY KEY,
	name text,
);

CREATE TABLE classes (
	id serial PRIMARY KEY,
	name text,
	teacher_id int REFERENCES teachers (id) 
		ON DELETE CASCADE
);

INSERT INTO teachers (name) VALUES ('Marry Bee');
INSERT INTO classes (name, teacher_id) VALUES ('Math', 1);
```

**How are relations, relationships, tuples, attributes, and entities represented in the example above?**

Relations are another way of saying "table" in a relational model based database.  As we can see above, we have two tables (relations) defined: `teachers` and `classes`.  

There is also a *relationship* between these relations. A relationship is an association between the data stored in relations.  There are three types of relationships or cardinalities (the number of instances of one entity that are related to instances of another entity) that can be shown in a database: one-to-one, one-to-many, and many- to- many.  The above example exhibits a one- to- many relationship, as there can be many classes with the same teacher, but each class has only one teacher.  We can say this relationship has a modality, which indicates if a relationship is required or not, of 0 on both sides meaning the relationship is optional on both sides.  There can be a class with no teachers, and a teacher with no classes. 

Within `teachers`, there is a primary key column assigned to `id`.  The column `teacher_id` within the `classes` table is defined as the foreign key which references this primary key.  We know that this relationship ensures referential integrity, as a value added to the foriegn key column must be present first in the primary key column. We can also see that an `ON DELETE CASCADE` constraint is added to the foreign key, which ensures that if a row is deleted from the parent table (`teachers`), the rows that reference it in the child table(`classes`) will automatically be deleted. 

A tuple is single row in a database that contains a single record in a relation.  For example, the `teachers` table contains one tuple after the `INSERT` statement is executed. The tuple would contain `id` as `1` and `name` as `Marry Bee`.  Similarly, the `classes` table would contain one tuple after the `INSERT` statement executes.  The tuple would include `name` as `Math` and `teacher_id` as `1`.  We can see that the `teacher_id` column could either contain `NULL` or `1`, but no other values, as this would violate the constraints of the foreign key. 

Attributes in a database are pieces of data that describe a member of an entity (where entity is a conceptual concept that is physically implementated as a table when discussing relational databases).   In regards to physical schema, attributes are the column names in a table.  Let's take a closer look: within `teachers` we have an `id` and a `name` attribute.  Each teacher will, or at least has the potential to, possess a value for these characteristics.  We can limit the values allowed to be stored within these columns through the use of constraints.  These ensure the accuracy and reliability of the data.  For example, `teachers.id` has a `Primary Key` restraint, which essentially provides a `NOT NULL` and `UNIQUE` constraint to the column. 

Now lets go a little deeper in our distinction between relation and entity.  Thus far, I have identified each as a table within a relational database.  If we were discussing the conceptual schema, or the high-level design, an entity would be a real world concept such as a teacher or a class.  A relation is then a low- level implementation that represents the physical schema as a set of tuples (records) that represent a model of an entity.  For example, each tuple from the `teachers` table represents an instance of a teacher entity, and each tuple from the `classes` table represents an instance of a class entity. 



```sql
CREATE TABLE teachers (
	id serial PRIMARY KEY,
	name text,
);

CREATE TABLE classes (
	id serial PRIMARY KEY,
	name text,
	teacher_id int REFERENCES teaachers (id) 
		ON DELETE CASCADE
);
```

**Considering the following code explain how defining keys and constraints ensure data integrity?**

Let's start by discussing data integrity.  This term, in respect to DBMS's, refers to the accuracy and consistency of data stored in a database.  Data integrity is implemented through design and authentification checks, and ensures standardized values according to data models and types.

SQL constraints are a way to implement this by setting rules which are enforced on tables in relational databases to limit the type of data or values that can be inserted, updated or deleted within tables. These constraints ensure the accuracy and the reliability of data stored in the table.  

Normalization is necesarry to reduce redundancy and improve data integrity by arranging data in multiple tables and defining relationships between them.  The low-level mechanism in which we establish these relationships in a database is through keys, which are a special type of constraint that can identify a specific row or refer to a specific row in another table. By creating two tables, `classes` and `teachers`, we can reduce redundancy by using keys to represent rows of information.  For example, if this were represented by a single table, the teacher column could potentially have many rows with the same value, as this is a one-to-many relationship. 

Primary keys identify an entity uniquely across a database, and carry with them the `NOT NULL` and `UNIQUE` constraints.  Foreign keys columns reference the primary key column of (usually) another table via the `REFERENCES` keyword.  The foreign key constraint specifies that the key can only contain values that are in the referenced primary key.  This means that if we attempt to add a value to our foreign key column that is not present already as a primary key in our referenced table, then an error will arise. 

So by defining keys and constraints, we can ensure that any data within our database is the correct data type and within whatever bounds we set, if any, and also that if a value represents another row, then that row is present.  Ensuring data integrity allows for accurate recoverability, increases stability and performance, and improves reusability and maintainability of our database. 



```sql
SELECT teachers.name, 
	FROM teachers
		JOIN classes
			ON teachers.id = classes.teacher_id
				GROUP BY teachers.name
					ORDER BY COUNT(classes.id);
```

**Explain how this SELECT query will be executed?**

1) The `FROM` clause and `JOIN`s will be executed first.  This will determine the total working set of data that is being queried. 

   ```sql
   FROM teachers 
     JOIN classes
      ON teachers.id = classes.teacher_id
   ```

2. The `GROUP BY` clause is then executed, which will result in as many rows as there are unique values in that column.

   ```sql
   GROUP BY teachers.name
   ```

3. The `SELECT` query is then executed 

   ```sql
   SELECT teachers.name
   ```

4. Finally, the `ORDER BY` clause will sort the rows by the specified data

   ```sql
   ORDER BY COUNT(classes.id)
   ```



```sql
CREATE TABLE example (
	id serial PRIMARY KEY,
	title varchar(200) NOT NULL UNIQUE,
	name char(100), 
	age numeric NOT NULL
);
```

**Consider the code below: What are the different data types in this example. Describe each of them and describe the differences between them.**

1) `serial` - The SERIAL data type stores a sequential integer, of the INT data type, that is automatically  assigned by the database server when a new row is inserted. The serial data type has a `NOT NULL` constraint. 

2. `varcher(200)` - String data type that is varying in length up to the given argument; aka Variable Character 

3. `char(100)` - Fixed length string data, any remaining space in the field is padded with blanks up to argument

4. `numeric` - AKA decimal, arbitrary precision numbers. Can take 2 arguments (precision,scale). Precision = total numbers allowed, Scale = numbers after decimal.

   Numeric data types are **numbers stored in database columns**. These data types are typically grouped by: Exact numeric types, values  where the precision and scale need to be preserved. Numeric data types are in two categories: exact and approximate. 

   •	Exact types include integer and decimal data types. 

   •	Approximate types include floating point data types.

   

```sql
CREATE TABLE example(
	some_num numeric(10,2)
);

INSERT INTO example (some_num) VALUES (1);
```

**Will this code raise an error? Why or why not?**

This will not raise an error and will be added to the column as `1.00` as the scale is `2` which will be required, and the amount of digits before the decimal is 1, and 1+2<10 (10 being the precision).

**SQL**'s exact numeric data types consist of **NUMERIC**(p,s) and **DECIMAL**(p,s) subtypes. They are exact, and we define them by precision (p) and scale (s). Precision is an integer that represents the total number of digits allowed in this column. These digits are in a particular radix, or number base – i.e. binary (base-2) or decimal (base-10). They are usually defined with a *decimal* *point*. The scale, also an integer value, represents the number of *decimal* *places* to the right (if positive) or left (if negative; this is rarely used) of the *decimal* *point*.When inserting data into a `NUMERIC` column, remember its precision limits. If you try to insert too large a number, you might get an error. For example, we want to insert the following:

The DECIMAL data type accepts numeric values, for which you may define a precision and a scale in the data type declaration. The precision is a positive integer that indicates the number of digits that the number will contain. The scale is a positive integer that indicates the number of these digits that will represent decimal places to the right of the decimal point. The scale for a DECIMAL cannot be larger than the precision. 

DECIMAL data types can be declared in one of three different ways. The declaration of it controls how the number is presented to an SQL query, but not how it is stored.

-  DECIMAL - Precision defaults to 38, Scale defaults to 0
-  DECIMAL(p) - Scale defaults to 0
-  DECIMAL(p, s) - Precision and Scale are defined by the user



In the above examples, *p* is an integer representing the precision and *s* is an integer representing the scale.

NOTE: If you exceed the number of digits expected to the left of the decimal point, an error is thrown. If you exceed the number of expected digits to the right of the decimal point, the extra digits are truncated.

As long as the length of the number + the number for scale isn't more than the precision.. ie 

Numeric(10,3)

12345678.12

bc this will insert 12345678.120 which will be too any digits for the precision. 





```sql
CREATE TABLE example(
	some_num int,
	some_text text CHECK (some_text > 0)
);

INSERT INTO example (some_num)
	VALUES (11);
```

**Will this code raise an error? Why or why not?**

This will raise an error, as the CHECK constraint uses an operator than is unavailable to the data type text.  An operator is a keyword that helps us to access the data and returns the result based on the  operator’s functionality. SQL provides us with many such operators to  ease the process of data manipulation.

`HINT: No operator matches the given name and argument types. You might need to add explicit type casts.`

`>` Checks if the value of left  operand is greater than the value of right operand, if yes then condition becomes true.

Generally, there are three types of operators that are [used in SQL](https://www.simplilearn.com/tutorials/sql-tutorial/how-to-become-sql-developer).

1. Arithmetic Operators

2. Comparison Operators

3. Logical Operators. 

   Comparison operators in SQL are used to check the equality of two expressions. It checks whether one expression is identical to another.  Comparison operators are generally used in the WHERE clause of a SQL  query. The result of a comparison operation may be TRUE, FALSE or  UNKNOWN. When one or both the expression is NULL, then the operator  returns UNKNOWN. 



```sql 
SELECT NULL IS NOT NULL;
```

**What will the following code return and why?**

It will return `f` as `NULL` is `NULL`.

This value represents nothing, that is, the absence of any other value. The crucial thing to remember about NULL is that it behaves somewhat differently than the nothing value in other languages.

When a `NULL` value appears to either side of any ordinary comparison operator (such as `=`, `<`, `>=`, etc.), the operator will return `NULL` instead of `true` or `false`. The empty output for the previous statement was an example of how `psql` displays NULL values:

When dealing with `NULL` values, **always** use the `IS NULL` or `IS NOT NULL` constructs: This will give `t` or `f` value.

This can be seen if we run the following code:

```sql 
SELECT false = NULL; #NULL (NULL on either side of equality returns NULL)
SELECT NULL = NULL; #NULL (NULL on either side of equality returns NULL)
SELECT false IS NOT NULL; #true (false is not equivalent to NULL)
SELECT true IS NOT NULL; #true (true is not equivalent to NULL)
SELECT NULL IS NULL; #true (IS NULL/IS NOT NULL will give t/f values)
```

The `IS NOT NULL` operator is used to test for non-empty values (NOT NULL values).

The `IS NULL` operator is used to test for empty values (NULL values).

Note that because you’re not retrieving any data from the database and  you’re only comparing values or the absence of values, you don’t need to include a `FROM` clause in this query.

In ruby, when you need a boolean value, `nil` is treated as `false` and values other than  `nil` or `false` are treated as true.





```sql
CREATE TABLE some_table (
	some_num decimal(10,4) DEFAULT 'some text'
	some_t_or_f boolean DEFAULT true
);
```

**Consider the code below. Will this code raise an error? Why or why not?**

ERROR: invalid input syntax for type numeric: "some text"

LINE 2: some_num decimal(10,4) DEFAULT 'some text'

The SQL DEFAULT  constraint is a constraint that can be added to tables to specify a  default value for a column. The default value is **used for the column's value when one is not specified** (for example, when you insert a row into the table without specifying a value for the column). Ex/

```sql
   ID int NOT NULL,
   OrderNumber int NOT NULL,
   OrderDate date DEFAULT GETDATE()
 ); 
```

```sql
 ALTER City SET DEFAULT 'Sandnes'; 
```

```sql
ALTER TABLE Persons
ALTER City DROP DEFAULT; 
```



```sql
CREATE TABLE some_table(
	some_num decimal(10,4),
	some_t_or_f boolean DEFAULT true
);

INSERT INTO some_table (some_num, some_t_or_f)
	VALUES (11, NULL);
```

**What values will be inserted into the table?**

`11` and `NULL`.  Although there is a default constraint that is added to the some_t_or_f column, the value `NULL` explicitly added to the column does not insert the default value.  The default value is only added when you insert a row into the table without specifying a value, but in this case we are specifying the absence of a value. 



```ruby
CREATE TABLE teachers (
	id serial PRIMARY KEY,
	name text,
);

CREATE TABLE classes (
	id serial PRIMARY KEY,
	name text,
	teacher_id int REFERENCES teachers (id) 
		ON DELETE CASCADE
);
```

**Consider the following code. What does ON DELETE CASCADE do in this example?**

Use the ON DELETE CASCADE option to specify whether you want rows deleted in a child table when corresponding rows are deleted in the parent table. If you do not specify cascading deletes, the default behavior of the database server prevents you from deleting data in a table if other  tables reference it.

Foriegn keys maintain referential integrity between two tables by ensuring that a column value within a record must reference an existing value.  For example, if you are adding a value to the `teacher_id` foreign key column in the `classes` table, it wouldn't make sense for that `teacher_id` to not reference some actual row of data in the `teachers` table. An error would be thrown, as there would be no teacher that the `teacher_id` was referencing. 

Now let's say that you want to delete a teacher from the `teachers` table. That teacher would have a specific primary key in the `teachers.id` column.  If that teacher's id was referenced within the `classes.teacher_id` column, an error would be thrown if we were to attempt this deletion as this would compromise the referential integrity.  ON DELETE CASCADE will automatically delete any corresponding rows in the referencing table when a referenced row is deleted in the parent table.



```sql
ERROR:  duplicate key value violates unique constraint "unique_id"
DETAIL:  Key (id)=(1) already exists.
```

**When would PostgreSQL throw this error and why? Explain the information that this error message gives us.**

A single field or group of attributes that uniquely identify a record is referred to as a unique constraint.

UNIQUE: The `id` column also has a `UNIQUE` constraint, which prevents any duplicate values from being entered into that column.

One of the key functions of a database is to maintain the integrity and  quality of the data that it is storing. Keys and Constraints are rules  that define what data values are allowed in certain columns. They are an important database concept and are part of a database's schema  definition.  Defining Keys and Constraints is part of the database design process and ensures that the data within a database is reliable and maintains its  integrity. Constraints can apply to a specific column, an entire table,  more than one table, or an entire schema.

Just as intended, that unique constraint prevented duplicate data in our table.It's not unusual for a column such as `id` to have a `UNIQUE` constraint. Having some sort of 'id' column in a database table is a  common, and useful, practice. Such a column is generally used to store a unique identifier for each row of data. In order for it to work  effectively though, we need to ensure that each value in such a column  is actually unique. Thus far, we've added data in such a way so that  each `id` was unique and each record distinct, but we don't  want to have to manually keep track of every value we add to that  column; using a `UNIQUE` constraint lets PostgreSQL do the work for us.

You can insert NULL values into columns with the UNIQUE constraint  because NULL is the absence of a value, so it is never equal to other  NULL values and not considered a duplicate value. This means that it's  possible to insert rows that appear to be duplicates if one of the  values is NULL .



**Create a table teachers with a column called set_up_date and set it to text. Change the data type in that column to a date data type.**

```sql
CREATE TABLE teachers (
set_up_date text);
```

```sql
ALTER TABLE teachers 
ALTER COLUMN set_up_date
TYPE date;
```

* You may have to use `USING set_up_date::date` after `date`



```sql
my_books=# CREATE TABLE authors (
my_books(#   id serial PRIMARY KEY,
my_books(#   name varchar(100) NOT NULL
my_books(# );
CREATE TABLE
my_books=# CREATE TABLE books (
my_books(#   id serial PRIMARY KEY,
my_books(#   title varchar(100) NOT NULL,
my_books(#   isbn char(13) UNIQUE NOT NULL,
my_books(#   author_id int REFERENCES authors(id)
my_books(# );

CREATE TABLE
my_books=# \d books
Table "public.books"
Column     |          Type          |                     Modifiers
- ---------------+------------------------+----------------------------------------------------
id             | integer                | not null default nextval('books_id_seq'::regclass)
title          | character varying(100) | not null
isbn           | character(13)          | not null
author_id      | integer                |
Indexes:
"books_pkey" PRIMARY KEY, btree (id)
"books_isbn_key" UNIQUE CONSTRAINT, btree (isbn)
"books_author_id_idx" btree (author_id)
Foreign-key constraints:
"books_author_id_fkey" FOREIGN KEY (author_id) REFERENCES authors(id)
```

**Consider the table below: What indexes does this table have and what type of algorithms has been used for the indexing? Explain how they have been created:**

What is an index?

Indexes are used to retrieve data from the database more quickly than otherwise. The users cannot see the indexes, they are just used to speed up searches/queries.  Updating a table with indexes takes more time than updating a table without (because the indexes also need an update). So, only create indexes on columns that will be frequently searched against.

```sql
CREATE INDEX index_name
ON table_name (column1, column2, ...);
```

```sql
DROP INDEX index_name ON table_name;
```

```sql
ALTER TABLE table_name
DROP INDEX index_name;
```

When you define a `PRIMARY KEY`constraint, or a `UNIQUE` constraint, on a column you automatically create an index on that column. In fact, the index is the mechanism by which these constraints enforce uniqueness.

Indexes are best used in cases where sequential reading is inadequate. For example: columns that aid in mapping relationships (such as Foreign Key columns), or columns that are frequently used as part of an `ORDER BY` clause, are good candidates for indexing

In the description of the table schema, we can see three entries listed under `Indexes:`

`"books_pkey"` - Created automatically by SQL because this column was defined as a Primary Key

`"books_isbn_key"` - Created automatically cy SQL because this column was defined with the `UNIQUE` constraint 

`"books_author_id_idx"` - Indexes are not automatically created for FK's, but are good candidates as FK's aid in mapping. This must have been explicitly created in the code. 

 The `btree`part of each entry identifies the *type* of index used (PostgreSQL uses B-tree by default for all indexes, and it is the only type available for unique indexes), followed by the name of the column that is indexed.

`"books_pkey" PRIMARY KEY, btree (id)
"books_isbn_key" UNIQUE CONSTRAINT, btree (isbn)
"books_author_id_idx" btree (author_id)`

A B-tree index creates a multi-level tree structure that breaks a database down into fixed-size blocks or pages. Each level of this tree can be used to link those pages via an address location, allowing one page (known as a node, or internal page) to refer to another with leaf pages at the lowest level.



(16)**If we create a table with an id column and specify it as serial, and we look at the schema of that table, what will be shown as a Type of id? Why? **

The SERIAL data type stores a sequential integer, of the `INT` data type that is automatically assigned by the database server when a new row is inserted. 

SERIAL values in a column are not automatically unique, but they are by definition `NOT NULL`. You must apply a unique index or primary key constraint to this column to prevent duplicate serial numbers. 

**SERIAL creates a regular SQL sequence** and implies DEFAULT nextval(<seqname>) , caching the results for reuse in the current session.

*A **sequence** is a special kind of relation that generates a series of numbers. A sequence will remember the last number it generated, so it will generate numbers in a predetermined sequence automatically.*

1. All tables should have a primary key column called `id`.
2. The `id` column should automatically be set to a unique value as new rows are inserted into the table.
3. The `id` column will often be an integer, but there are other data types (such as UUIDs) that can provide specific benefits.

`CREATE SEQUENCE` statements modify the characteristics and attributes of a database by adding a sequence object to the database structure. It does not actually manipulate any data, but instead manipulates the data definitions. As such, `CREATE SEQUENCE` statements are part of the DDL sublanguage.

It could also be argued that `CREATE SEQUENCE` is DML; the sequence object it creates is a bit of data that is used to keep track of a sequence of automatically generated values, so it can be thought of as being part of the data instead of a characteristic of the data. However, all `CREATE`statements (not just `CREATE SEQUENCE`) are generally thought of as DDL.

The default serial starting number is 1, but you can assign an initial value, *n*, when you create or alter the table. 

- You must specify a positive number for the starting number. 
- If you specify zero (0) for the starting number, the value that is used is the maximum positive value that already exists in the SERIAL column + 1. 



(17)

 ```sql
 SELECT age, full_name FROM students
 WHERE id < 2;
 ```

**What type of statement is this code presenting? Explain all components of this statement. **

`SELECT`

SQL query to select data in a database. This is type of SQL statement that allows users to search data in a database and return a result set of records from one or more tables. 

`age, full_name`

There are identifiers and keywords in SQL statements. Identifiers are the names of tables and columns, and it is best to refrain from naming these identifers with keyword names. If this is unavoidable, we must use double quotes around the identifier name so PostgreSQL treats it as intended. These specific identifiers are attributes/columns of the `students` table.  The `SELECT` clause specifies one or more columns to be retrieved.

`FROM`

This clause is a `SELECT` statement option that allows users to specify which table they wish to query data. There can be optional `JOIN` subclauses to specify the complete dataset the user wishes to query. 

`students`

This is another identifier that specifies the table the user wishes to query and is found in the `FROM` clause.  

`WHERE`

We can qualify a query by adding a `WHERE` clause.  This will identify which rows are desired. It is important to note that aggregate functions cannot be included in the `WHERE` clause.  The use of a subquery would be useful in these situations. `WHERE` clauses can be utilized in `SELECT`, `UPDATE`, and `DELETE` statements. 

`id < 2`

The `WHERE` clause will include an expression which will evaluate to a Boolean value.  The rows in which this expression evaluate to true are included.  Comparison predicates, logical operators, and string matching operators are all useful in these expressions. This expression uses the comparison operator `<` to determine if the value assigned to the `id` attribute for the specific row is less than the integer `2`.  If this evaluates to `true`, the row will be included in our result table. 

`;`

The semicolon is the standard way to separate SQL statements.  It is used as a statement terminator. 

(18)



```sql
SELECT year FROM schedule WHERE year > 2010;
```

**Why will this code result in an error? Why or why not? **

If the datatype of year is `INTEGER` then no error will be raised.  If `year` is of the `TEXT` datatype, then we will have to use year::integer > 2010 to ensure that the year is first temporarily converted to an INTEGER for comparison in the WHERE clause. Because `year` is technically an SQL keyword, we should use double quotes around `year` to ensure SQL treats it as an identifier.



(19)

```sql
SELECT name, age FROM students WHERE age = NULL;
```

**Will this result in an error? Why or why not? If not what will be the output of that code?**

This will not result in an error.  `NULL` represents the absence of a value in SQL.  In the above example the comparison equal operator is used in the `WHERE` clause.  The intention is to compare the value of `age` for that specific row to `NULL`.  Instead of a true/false BOOLEAN value being returned, `NULL` is returned (even if the value of `age` for that column is `NULL`).  

The code will output:

```sql
 name | age 
------+-----
```

This is because if `NULL` is on either side of a comparison operator, `NULL` will always be returned.  To rectify this code, `IS` should replace the `=` operator.  That is, the `WHERE` clause should look like this:

```sql
WHERE age IS NULL;
```

If we want to check if a value is not `NULL`, then `IS NOT NULL` should be used. This will ensure that a BOOLEAN value is returned.  

If we change our code to this:

```sql
SELECT name, age FROM students WHERE age IS NULL;
```

then we will return the name and age column values for all rows in which `age` is `NULL`.



(20)

```sql
SELECT full_name FROM students WHERE full_name ILIKE '%Johanson';
```

**Which of the following names would be returned and why?**

- Johanson
- 'Johanson Branson'
- 'Eva B. Johanson'
- 'johanson'

The names Johanson, Eva B. Johanson, and johanson will be returned.  `ILIKE` is a case insensitive string matching operator (keyword).  This is used alongside `%` which acts as a placeholder.  It can represent zero or more characters, so any name that ends with/is`Johanson` or `johanson` will be returned.  



(21)

```sql
name   |   age   |   participated
---------------------------------
'Ann'  |   13    |   t
'Ben'  |   12    |   
'Emma' |   15    |   f
'Kat'  |   12    |   f
```

**Write a query that retrieves all the names of kids for whom the value of participated column is not true. **

```sql
SELECT name FROM students WHERE participated != true;  #OR
SELECT name FROM students WHERE participated <> true;
```

Both `!=` and `<>`are comparison operators for 'not equal'.



(22)

```sql
ERROR:  column "users.full_name" must appear in the GROUP BY clause or be used in an aggregate function
```

**What does this error message tell us? Write a statement that could cause an error like that and describe ways to resolve this error. **

This message tells us that a `GROUP BY` clause was used in the query and the column `full_name` from the `users` table was not present in the `GROUP BY` clause, was not in an aggregate function, and/or was not functionally dependant on the grouped columns. 

Lets examine how `GROUP BY` works:

Data will aggregated by whatever is specified in the `GROUP BY` clause. For example, if the initial query was as follows:

```sql
SELECT full_name, age FROM users
GROUP BY age;
```

SQL would group together all the rows in which the value in the age column was the same. Then what would become of the `full_name` column? This is where the problem lies.  There is more than one possible value that would be returned from the column that is not grouped.  This ambiguity is what causes the error statement. 



- The easiest way to fix this code would be to add the `full_name` attribute to the `GROUP BY` clause.  One single value would be returned for each row, and an error would not be returned. 

```sql
SELECT full_name FROM users 
GROUP BY full_name;
```



- Another way to remedy this would be to perform an aggregate function on the ungrouped column. This would perform an operation on a group of rows and return a single value.

Let's try this:

```sql
SELECT count(full_name), age FROM users 
GROUP BY age;
```

This code will count the number of values in the `full_name` columns that have the same value in the `age` column.  This works because now we have a single value (an integer in the full_name row) for a single row in the `age` column.  



- I also want to examine functional dependancy as a way to circumvent using an aggregate function on ungrouped columns.  

```sql
SELECT full_name FROM users
GROUP BY id;
```

A functional dependancy exists if the grouped column is a Primary Key (PK) of the table in which the ungrouped column is present. For example, the `full_name` column will always have a single value if we group by the PK, because the PK `id` uniquely identifies the `full_name` attribute. Therefor there will be no ambiguity and only one possible value will be returned in each row in the `full_name` column.



(23)

````sql
```jsx
id |    name    |    year_of_birth    |    grade
-------------------------------------------------
1  |  'Eddie'   |   1986-01-01        |   A
2  |  'Maggie'  |   1975-04-11        |   B+
3  |  'Elenore' |   1995-03-13        |   A-
```
````

- **Write a query that returns names of students who were born in April**

  ```sql
  SELECT name FROM students 
  WHERE date_part('month', year_of_birth) = 4
  ```

  

- **Write a query that returns names of students who were born on 11th of April**

  ```sql
  SELECT name FROM students 
  WHERE date_part('month', year_of_birth) = 4 AND 
  date_part('day', year_of_birth) = 11;
  ```

  

- **Write a query that returns all students who were born in 1986**

  ```sql
  SELECT name FROM students  
  WHERE date_part('year', year_of_birth) = 1986;
  ```

  

- **Write a query that returns the oldest person**

  ```sql
  SELECT name FROM students 
  ORDER BY year_of_birth ASC
  LIMIT 1;
  ```

  *oldest person will have the earliest DOB so they will be listed first in ASC order



(24)

**What syntax would you use to remove all rows from an imaginative students table? Present a code that illustrates that. **

```sql'
DELETE FROM students;
```

`DELETE` is part of SQL sub-language DML, or data manipulation language.  The SQL constructs of DML include `SELECT`,`INSERT`,`UPDATE`, and `DELETE`.  `DELETE` is the `d`in the acronym CRUD, which makes up DML.  `DELETE` will delete entire rows of data from a database table.  We can specify which rows to delete through the use of a `WHERE` clause, or leave this out (as shown above) to delete all rows. Once run, this statement is irreversable.  Having the data backed up and/or running a `SELECT` query on rows intended to be deleted would be helpful to ensure only data that is unwanted is deleted.



(25)

**Why do we need to create multiple tables instead of just keeping all the data in one table?**

Normalization is a procedure in which data is organized in a database.  This data organization is carried out through the creation of tables and establishing relationships between these tables. Why is this crucial in regards to databases? Wouldn't a single table with all of our data suffice? 

Imagine having a single table in a database with seemingly endless rows and columns.  What problems could arise? To start, this could be very overwhelming and easily disorganized. There is also the issue of redundancy, which is something that should be avoided in any code if possible.  

Let's say we have the names, ages, and addresses of customers and they each order different products with product numbers, names, locations,etc.  Each time a product is purchased, all of this data is re-entered into our database.  This could lead to input errors and would make any updates laborous. Our data integrity is at risk of being compromised, as maintaining accuracy and consistency is difficult with this lack of data organization.

Now lets conceptualize a schema, or organization/structure of a database, that will work better for us.  This is the mechanism in which we carry out normalization. Creating an entity-relationship-diagram (ERD) will allow us to visualize our database and table structure, and the relationships between them. This high level of abstraction will enable us to make the best decisions logically for our data organization. Entities (real world objects) will later help define our relations, or tables, and their relationships will assist us with our data definitions. 

If we revisit our contrived single table example, we can better understand how normalization helped us reduce reduncancy and improved data integrity.  I'm going to describe our physical schema. We created three separate tables: customers, orders, and products. Each of these tables contains a primary key which will uniquely identify a row in our table. Our relationship between `customers` and `products` is a many-to-many relationship (cardinality), so we have an orders table to join them.  This join table will have two Foreign Keys (`customer_id`/`product_id`) that will reference the Primary Keys in our customers (`customers.id`) and orders (`orders.id`) tables. Now instead of re-entering customer information and product information each time an order is placed, we can just add a row with integers into our `orders` table.  This drastically decreased redundancy and allows us to update customer and product information quickly. 

Through the implementation of Primary and Foreign Keys, we've also ensured that our data has referential integrity.  A value in our referencing table (child table) cannot reference a value that is not present in our referenced table (parent table).  In practice, our `users` JOIN table in our example cannot hold values in the `customer_id`/`product_id` (FK's) columns that are not present in their respective `customers.id`/`products.id` (PK's) columns .  In this way, table relationships will remain intact and consistent. 



(26)

```sql
id |    name    |    year_of_birth    |    grade |  class
-----------------------------------------------------------
1  |  'Eddie'   |   1986-01-01        |   A      |  Math
2  |  'Maggie'  |   1975-04-11        |   B+     |  History
3  |  'Elenore' |   1995-03-13        |   A-     |  French
```

- **We no longer want to have classes at the same table as students. What are the steps you would take to create another table `classes` and create a relationship between `students` and `classes`.**

  ```sql
  ALTER TABLE students DROP COLUMN class; 
  
  CREATE TABLE classes (                  
    id serial PRIMARY KEY,
    name text
  );
  
  INSERT INTO classes (name) VALUES 
    ('Math'),
    ('History'),
    ('French');
    
  ALTER TABLE students ADD COLUMN class_id integer REFERENCES classes(id);
  
  UPDATE students SET class_id = 1 WHERE id = 1;
  UPDATE students SET class_id = 2 WHERE id = 2;
  UPDATE students SET class_id = 3 WHERE id = 3;
  ```

  

- **Create `classes` table and the relationship between `classes` and `students`.**

The relationship is defined by a PK in the classes table and a FK referencing that PK in the students table.  The cardinality (number of objects on each side of the relationship) thus far is a one-to-many relationship, where a class can have many students, but a student can only have one class. The modality of the students table and the classes table is 0 as a student does not need to be in a class and a class does not need to have any students.  Modality is defined as whether the relationship is required or not.  A modality of `0` means that is is not required, while `1` means it is required. 



(27)

**What benefits does presenting cardinality give us? How may the information that representing cardinality in our diagrams be useful for the database design?**

Cardinality is a modeling concept that indicates the largest number of objects allowed on either side of the relationship.  The only two choices are one or many. When implementing this modeling concept in the physical schema, it is the relationship between a row (instance) in one table (entity) and a row in another table through Primary and Foreign Keys. This is important because it is a link, or tangible relationship, from one entity to another. 

- One-to-One- A student has one id number and an id number has one student. We may even decide that these two tables are better as one after some thought. 

  ```sql
  CREATE TABLE id_number (
    id serial PRIMARY KEY,
    id_num integer
  );
  
  CREATE TABLE student (
    id serial PRIMARY KEY REFERENCES id_number(id),
    name text
  );
  ```

  

- one- to - many - A teacher/class relationship.  A teacher can have many classes and the class can have one teacher. (Assume no teachers assistants)

 ```sql
 CREATE TABLE teachers (
   id serial PRIMARY KEY,
   name text
 );
 
 CREATE TABLE classes (
   id serial PRIMARY KEY,
   class_name text,
   teacher_id integer REFERENCES teachers(id)
 );
 ```



- many- to- many- customers can purchase many products and products can be bought by many customers 

  ```sql
  CREATE TABLE customers (
    id serial PRIMARY KEY,
    cust_name text 
  );
  
  CREATE TABLE products (
    id serial PRIMARY KEY,
    prod_name text
  );
  
  CREATE TABLE orders(
    id serial PRIMARY KEY,
    customer_id integer REFERENCES customers(id),
    product_id integer REFERENCES products(id)
  );
  ```

  

As we can see, understanding the cardinality will dictate the design details of our database.  A one-to-one relationship can mean that our primary key is the same column as our foreign key. A one-to-many will help us determine which table should have a foreign key and how that will reference our other table.  It is important to note that the FK column does not have a UNIQUE constraint so many instances of that entity can have the same value (referencing the 'one' cardinality).  A many-to-many relationship will tell us that a JOIN table is necessary, and that there will be foreign keys referencing the two participants. Other attributes/columns in our JOIN table will be relevent to both entities.



(28)

**Consider the ERD below. Describe the relationships between those entities:**

![img](https://fine-ocean-68c.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fb174c93e-368b-42ea-a33a-08c5339b7543%2FUntitled.png?table=block&id=45e76212-c132-4e65-95f1-0a8557c5d587&spaceId=88e19fde-7b54-4f65-9c44-d9e4fc3f307b&width=1280&userId=&cache=v2)

The cardinality is a one- to-many relationship. A Primary Key in the `Director` table will reference a Foreign Key in the `Film` table. 



(29)

**Consider the following diagram. Describe what is the cardinality between entities?**

![img](https://fine-ocean-68c.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F2a74d67d-7f6f-4909-be4a-e6f7d1d39978%2FUntitled.png?table=block&id=32bc0ead-56f6-4c15-bffc-71f9f512b410&spaceId=88e19fde-7b54-4f65-9c44-d9e4fc3f307b&width=1280&userId=&cache=v2)

The cardinality of `students` and `university` is one-to-many with the FK in `university` referencing the PK in `student`. The modality is `1` for both which means that the relationship is required for `students` and `university`.

The cardinality of `student` and `scholarship` is many- to- many. There will be PK's in both tables and a JOIN table will have two FK's that reference the two tables. The modality is `1` for `student` and `0` for `scholarship`.  The scholarship must have a student, but the student does not have to have a scholarship.

The cardinality of `scholarship` and `university` is one-to-many with the FK in `scholarship` referencing the PK in `university`. The modality is `1` for both which means that the relationship is required for `scholarship` and `university`. Universities must have scholarships, and scholarships must belong to a university.



(30)

```sql
SELECT * FROM customers;
customer_id | name  
-------------+-------
           1 | Johny
           2 | Ben
           3 | Gary

SELECT * FROM orders;
order_id | customer_id | orders 
----------+-------------+--------
        1 |           1 | book
        2 |           2 | mug
        3 |           3 | chair

\d orders 

Column    |  Type   | Collation | Nullable |                 Default                  
-------------+---------+-----------+----------+------------------------------------------
 order_id    | integer |           | not null | nextval('orders_order_id_seq'::regclass)
 customer_id | integer |           |          | 
 orders      | text    |           |          | 
Indexes:
    "orders_pkey" PRIMARY KEY, btree (order_id)
Foreign-key constraints:
    "orders_customer_id_fkey" FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
```

**What will happen if we run the following statement? Why? **

```sql
DELETE FROM customers WHERE customer_id = 3;
```

```sql
ERROR:  update or delete on table "customers" violates foreign key constraint "orders_customer_id_fkey" on table "orders"
DETAIL:  Key (customer_id)=(3) is still referenced from table "orders".
```

This error will be raised because `orders.customer_id` was defined as a Foreign Key without an `ON DELETE CASCADE` constraint.  The child table, `orders`, contains a column `customer_id` which references the parent table,`customers` Primary Key column (`customers.customer_id`).

If we delete a customer from our `customers` table, we could not reference that customer in the `orders` table. Because there is already a reference to the customer with a `customer_id` of 3 in the `orders` table, PostgreSQL will raise and error and leave the tables as is.  

This ensures that the referential integrity is maintained between the two tables, which is a crucial to database design.



(32)

```sql
CREATE TABLE students (
	id serial PRIMARY KEY,
	name varchar(100) 
);   

CREATE TABLE addresses (
	student_id int, 
	address text,
	city text,
	PRIMARY KEY (student_id),
	FOREIGN KEY (student_id) REFERENCES students (id)
		ON DELETE CASCADE
);
```

**Consider the code below. What type of cardinality does this example present? Explain how did you deduce that.**





https://fine-ocean-68c.notion.site/LS180-906a0630d9d04f43803f149fd91196f0?p=2a398057ddd4464faa19b2eb82f7df52&pm=s
