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

Normalization is necesarry to reduce redundancy and improve data integrity by arranging data in multiple tables and defining relationships between them.  The low-level mechanism  in which we establish these relationships in a database is through keys, which are a special type of constraint that can identify a specific row or refer to a specific row in another table. By creating two tables, `classes` and `teachers`, we can reduce redundancy by using keys to represent rows of information.  For example, if this were represented by a single table, the teacher column could potentially have many rows with the same value, as this is a one-to-many relationship. 

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

When dealing with `NULL` values, **always** use the `IS NULL` or `IS NOT NULL` constructs: This will give `t` or `f` value

The `IS NOT NULL` operator is used to test for non-empty values (NOT NULL values).

The `IS NULL` operator is used to test for empty values (NULL values).

Note that because you’re not retrieving any data from the database and  you’re only comparing values or the absence of values, you don’t need to include a `FROM` clause in this query.



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

`"books_pkey" 
"books_isbn_key" 
"books_author_id_idx" `

 The `btree`part of each entry identifies the *type* of index used (PostgreSQL uses B-tree by default for all indexes, and it is the only type available for unique indexes), followed by the name of the column that is indexed.

`"books_pkey" PRIMARY KEY, btree (id)
"books_isbn_key" UNIQUE CONSTRAINT, btree (isbn)
"books_author_id_idx" btree (author_id)`

A B-tree index creates a multi-level tree structure that breaks a database down into fixed-size blocks or pages. Each level of this tree can be used to link those pages via an address location, allowing one page (known as a node, or internal page) to refer to another with leaf pages at the lowest level.



**If we create a table with an id column and specify it as serial, and we look at the schema of that table, what will be shown as a Type of id? Why? **

