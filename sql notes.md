-   A **relation** - A set of individual but related data entries; analogous to a database table.
-   A **relationship** is an association between the data stored in those relations.
-   **SQL statement**- A SQL command used to access/use the database or the data within that database via the SQL language.
-   **SQL query**-  A subset of a "SQL Statement". A query is a way to search, or lookup data within a database, as opposed to updating or changing data.
-   What is a **database**?
    -   A structured set of data stored on a computer.
    -   One of the main purposes is to maintain the integrity and quality of the data that it is storing 
-   **Relational database**
    -   A database organized according to the relational model of data.  The relational model defines a set of relations(tables) and describes their relationships between them in order to determine how the data stored in them can interact.
    -   Helps cut down on redundancy and provides a useful data structure to interact with
    -   Tables can be used to represent real world abstractions of business logic of an application, such as a customer or an order. Once created, these tables can be used to store our data relevant to that particular abstraction.  Columns are what we use to give tables their structure. Rows can be called tuples.
    
-   What is a **Relational Database Management System (RDBSM)?**
    -   a software application or system which allows a user, or application, to interact with a relational database by issuing commands using syntax  that conforms to a certain set of conventions or standards.  All use the declarative language, SQL
        -   ex/ PostgreSQL
-   **Client-Server architecture**- 
    -   Interface or clients interact with a RDBMS
        -   access the database from a programming language through a GUI app that allows access and administration, or through command- line interface
        -   They all interact with the database by issuing a request (declaration) and recieving a response 
        -   Client-server is an architectural design used by most relational databases
        -   Different levels of abstraction can exist in client-server model
        -   In postgreSQL you have the PostgreSQL server and the PostgreSQL Client
        -   PostgreSQL comes packaged with client applications which allow you to interact with PostgreSQL in various ways by issuing commands via the command line. 
            -   Use of wrappers around SQL commands such as createdb, dropdb, psql (PostgreSQL interactive console)
                -   You can issue psql console meta-commands or run SQL statements using standard SQL syntax from the psql console 

-   **ERD**
    -   Entity-Relationship (ER) model is **a visual representation of the table's structure and the relationships between logically related tables**. In ER modeling the database structure is represented as a diagram known as ER diagram (ERD). An ER diagram gives a better understanding of the overall database structure.
    -   Reduce complexity and saves time 

-   **Schema**
    -   Schema + data provide us with structured data that we can interact with 
    -   A database schema **defines how data is organized within a relational database**; database structure/ this is inclusive of logical constraints such as, table names, fields,  data types, and the relationships between these entities. 
    -   DCL is also part of schema (access restriction/permissions) 
    -   Each column contains data of one specific kind for all of the individuals.  Each row represents a single set of related data, while the columns represent a standardized way to store data for that particular attribute.



 **Three levels of schema/ abstraction**

*conceptual* - A high-level design focused on identifying entities and their relationships. Abstract way to visualize entities and their relationships.  Not thinking about how things are stored in database at all.  ERD diagrams (Crow's foot notation)

*logical* - implementation details with no specific database in mind. A list of attributes and data types but not database specific. Language agnostic. SQL standard 

*physical* - A low-level database-specific design focused on implementation. Psql/mysql/etc.  Attributes, data-types, constraints, relationships (KEYS). Map high level entities into specific tables/ column/ data types 

**three types of relationships that can be shown in a database diagram**

type of cardinality that refers to **a relationship between two entities in an entity relational diagram**

1. • One-to-one (1:1): An occurrence of entity A can relate, at most, to one occurrence of entity B, and an occurrence of entity B can relate, at most, to one occurrence of entity A. For example, a husband can have only one wife, and a wife only one husband(but in my country its one to many).

   • One-to-many (1:N): One occurrence of entity A can relate to many occurrences of entity B, but an occurrence of B can relate to only one occurrence of A. For example, each pet has one owner, but each owner can have one or more pets.

   • Many-to-many (M: N): An occurrence of entity A can relate to multiple occurrences of entity B, while an occurrence of entity B can relate to many occurrences of entity A. For example, a doctor-patient relationship, each doctor sees many patients and each patient sees many doctors.

**Cardinality**

The number of objects on each side of the relationship.

In database design, cardinality and modality are two modelling concepts which are used for analyzing entities, attributes and relationship structure in the database

Cardinality shows the largest number of occurrences allowed in a relationship, not the smallest. This is usually expressed as one to many. In simple terms, cardinality refers to the relationship between a row of one table and a row of another table, the only two options for cardinality are one or many.

![img](https://miro.medium.com/v2/resize:fit:1400/1*Tubs10YRvMvjj869at5ouQ.png)

One to one- 

*Person can have one nose, and vise versa*

One to many-

*Person can have many emails, but not the other way around*

Many to Many-

*Person in sports sports can have many people people can play many sports*

This new table is called an **intermediate table** (join/ linking/junction table).

**Modality**

The modality of a relationship indicates if that relationship is required or not. If a relationship has a modality of 1, the smallest number of instances that can be on that side of a relationship is 1.



![img](https://miro.medium.com/v2/resize:fit:902/1*gsYA1v0xda6_czj7Xy7Gpg.png)

**What is SQL?**

**SQL** (structured query language) is a language used to manipulate the structure and values of datasets stored in a relational database. It is described as a **special purpose language** because it is typically used only for a very specific purpose: interacting with relational databases, SQL is predominantly a **declarative language** (details are abstracted away by database engine). And due to its simplicity,  SQL databases provide safe and scalable storage for millions of websites and mobile applications.

| sub-language                                                 | controls                       | SQL Constructs                         |
| ------------------------------------------------------------ | ------------------------------ | -------------------------------------- |
| **DDL** or data definition language ( defining data and attributes/ schema) | relation structure and rules   | `CREATE`, `DROP`, `ALTER`              |
| **DML** or data manipulation language (CRUD) create, read, update, delete data | values stored within relations | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| **DCL** or data control language                             | who can do what                | `GRANT`, `REVOKE`                      |

- DDL modifies *Schema*
  - The Data Definition Language (DDL) define structure of database/ component of SQL is used to create,  modify, and delete databases and tables; that is, the DDL is responsible for describing how data is structure
  - Think of a table in SQL as a type of an entity (ie. Dogs),  and each row in that table as a specific *instance* of that type (ie. A pug, a beagle, a different  colored pug, etc).  This means that the columns would then represent the common properties (attributes) shared by all instances of that entity (ie. Color of fur, length of tail, etc).
    - `ALTER TABLE` modifies the characteristics and attributes of a table
- DML modifies *Data*
  - The Data Manipulation Language (DML) retrieve or modify data stored in a database/ component of SQL is used to create, read, update, and delete the actual data in a database. 
    - ex/ `SELECT` merely queries (reads) the data in a database
- *DCL* controls rights and access 
  - What users are allowed to do what when interacting with a database
  - Uses `GRANT` and `REVOKE`
  

**What is a query?**

A query in itself is just a statement which declares what data we are  looking for, where to find it in the database, and optionally, how to transform it before it is returned

**What is a metacommand**

`\d` is a `psql` console command, otherwise known as a meta-command, not part of SQL. As such, it is not part of any SQL sublanguage.  Anything you enter in psql that begins with **an unquoted backslash** is a psql meta-command that is processed by psql itself. These commands make psql more useful for administration or scripting. Meta-commands  are often called slash or backslash commands.  Meta commands are a feature that psql has which allows the user to do powerful operations without querying a database.

**What is a wrapper**

Use of wrappers around SQL commands such as createdb, dropdb, psql (PostgreSQL interactive console)

- psql application command from the terminal

- utility functions are executed from the terminal

- | Client/Application Command-Line Command | Notes                                                        |
  | :-------------------------------------- | :----------------------------------------------------------- |
  | `psql -d sql_book`                      | starts a `psql` session and connect to the *sql_book*database |
  | `createdb sql_book`                     | creates a new database called *sql_book* using a psql utility |
  | `dropdb my_database`                    | permanently deletes the database named *my_database* and all its data |

**What is `NULL`**

This value represents nothing, that is, the absence of any other value. The crucial thing to remember about NULL is that it behaves somewhat differently than the nothing value in other languages.

When a `NULL` value appears to either side of any ordinary comparison operator (such as `=`, `<`, `>=`, etc.), the operator will return `NULL` instead of `true` or `false`. The empty output for the previous statement was an example of how `psql` displays NULL values:

When dealing with `NULL` values, **always** use the `IS NULL` or `IS NOT NULL` constructs: This will give `t` or `f` value

**Create database in terminal: (utility functions from terminal)**

```shell
createdb sql_book #CREATE DATABASE in terminal console (postgres wrapper function or PostgreSQL client application)
```

**Connect to database:**

`psql -d sql_book`

**List all databases:  (SQL statements/command from psql console)**

`\list` or `\l`

**Create a database from PSQL console:**

`CREATE DATABASE another_database;` (Standard SQL command)

- Another_database is the required parameter passed to `CREATE DATABASE`command
- database names should be descriptive and snake_case

**Connect to a different database from PSQL console:**

`\c another_database1` #or `\connect`

*meta commands dont have to end with `;`

**Delete database from PSQL:**

`DROP DATABASE another_database;`

*USE WITH CAUTION* - this will delete all schema and data

**Delete database from terminal:** *From terminal is a wrapper function*

`dropdb yet_another_database`

**Get out od PSQL console:**

`\q`

**Create table in PSQL:**

`CREATE TABLE some_table()`

**Creating a table with columns:** 

*constraints are optional*

`CREATE TABLE table_name (
    column_1_name column_1_data_type [constraints, ...],
    column_2_name column_2_data_type [constraints, ...],
    .
    .
    .
    constraints
);`

ex/

`CREATE TABLE users (
       id serial UNIQUE NOT NULL,
       username char(25),
       enabled boolean DEFAULT TRUE
);`

COLUMN CONSTRAINT:

```
CREATE TABLE products (
    product_no integer UNIQUE,
    name text,
    price numeric
);
```

TABLE CONSTRAINT EQUIVALENT TO COLUMN CONSTRAINT:

```
CREATE TABLE products (
    product_no integer,
    name text,
    price numeric,
    UNIQUE (product_no)  OR UNIQUE(A,C) TO HAVE UNIQUE GROUPS
);
```

If you want Null to count as a value to compare unique with (that is not allow two null values) then use `NULLS NOT DISTINCT`

```
CREATE TABLE products (
    product_no integer UNIQUE NULLS NOT DISTINCT,
    name text,
    price numeric
);
```

**Data Types for Table Creation:**

- A data type classifies particular values that are allowed for that column

| Data Type                                                    | Type      | Value                             | Example Values           |
| ------------------------------------------------------------ | --------- | --------------------------------- | ------------------------ |
| `varchar(length)`                                            | character | up to `length` characters of text | `canoe`                  |
| `text`                                                       | character | unlimited length of text          | `a long string of text`  |
| `integer`                                                    | numeric   | whole numbers                     | `2147483647`, `-1423290` |
| `real`                                                       | numeric   | floating-point numbers            | `24.563`, `-14924.3515`  |
| `decimal(precision, scale)` alias `numeric If you dont specify precision or scale then you can have any number` | numeric   | arbitrary precision numbers       | `123.45`, `-567.89`      |
| `timestamp` or `timestamp with time zone` (or `timestamptz`) data type that will store a timestamp with a timezone. | date/time | date and time                     | `1999-01-08 04:05:06`    |
| `date`                                                       | date/time | only a date                       | `1999-01-08`             |
| `boolean`                                                    | boolean   | true or false                     | `true`, `false`          |

*Full set of data types*

https://www.postgresql.org/docs/current/datatype.html

https://dev.mysql.com/doc/refman/5.7/en/data-types.html

**View all tables in a database:**

`\dt` #`Schema`, `Name`, `Type`, and `Owner`.

Detailed Table in database:

`\d users` #users is the table name 



*Although database schema is largely a DDL (Data Definition Language)  concern, parts of it, such as access and permissions, are determined by  DCL (Data Control Language)



**Altering Data in Schema:**

`ALTER TABLE table_to_change
    stuff_to_change_goes_here
    additional_arguments`

**Rename Table:**

`ALTER TABLE users
      RENAME TO all_users;`

**Rename Column:**

`ALTER TABLE all_users
      RENAME COLUMN username TO full_name;`

**Alter DataType:**

`ALTER TABLE all_users
      ALTER COLUMN full_name TYPE varchar(25);`

**Alter Constraints:**

`UNIQUE` is the one constraint that is never a column constraint; it's always a table constraint.All other constraints are considered to be either table or column  constraints based on how the constraints are defined. If it's done in a `CREATE TABLE` command along with the actual column attributes, it's a column constraint. Otherwise, it's a table constraint. 

1) column constraint- NOT NULL is always a column constraint and the only one we can add as a column constraint to an ALTER TABLE statement 

`ALTER TABLE table_name
      ALTER COLUMN column_name
      SET NOT NULL;`



```sql
ALTER TABLE stars
ADD CHECK (spectral_type IN ('O', 'B', 'A', 'F', 'G', 'K', 'M')),
ALTER COLUMN spectral_type SET NOT NULL;
```



2. table constraint

   `ALTER TABLE table_name
         ADD [ CONSTRAINT constraint_name ]
         constraint_clause;`

   Ex/ 

   ​	`ALTER TABLE contacts ADD CONSTRAINT number_unique UNIQUE (number);`

   3. remove constraint

      `ALTER TABLE table_name
            DROP CONSTRAINT constraint_name;`

      REMOVE NOT NULL 

      ```sql
       ALTER TABLE YourTable ALTER COLUMN YourColumn DROP NOT NULL
      ```
      
      4. Drop Default Clause from `serial`
      
         `ALTER TABLE all_users
               ALTER COLUMN id
               DROP DEFAULT;`

**SET default**

`ALTER TABLE employees ALTER COLUMN vacation_remaining SET DEFAULT 0;`

**Add Check Constraint**

A check constraint is the most generic constraint type. It allows you to specify that the value in a certain column must satisfy a Boolean  (truth-value) expression.

`ALTER TABLE users ADD CHECK (full_name <> '');`

```sql
ALTER TABLE birds ADD CONSTRAINT check_age CHECK (age > 0); (name check)
```

```sql
ALTER TABLE birds ADD CHECK (age > 0); (automatic name)
```

```
CREATE TABLE products (
    product_no integer,
    name text,
    price numeric CHECK (price > 0)
);  *key word CHECK followed by an expression in parentheses*
```

YOU CAN NAME THE CONSTRAINT LIKE THIS:

 key word `CONSTRAINT` followed by an identifier followed by the constraint definition

```
 price numeric CONSTRAINT positive_price CHECK (price > 0)
);  
```

```
CREATE TABLE products (
    product_no integer,
    name text,
    price numeric CHECK (price > 0),
    discounted_price numeric CHECK (discounted_price > 0),
    CHECK (price > discounted_price)
);
```

YOU CAN ALSO REFER TO SEVERAL COLUMNS AND COMPARE

We say that the first two constraints are column constraints, whereas the third one is a table constraint because it is written separately from any one column definition. Column constraints can also be written as table constraints, while the reverse is not necessarily possible, since a column constraint is  supposed to refer to only the column it is attached to. 



It should be noted that a check constraint is satisfied if the check  expression evaluates to true or the null value. Since most expressions will evaluate to the null value if any operand is null, they will not prevent null values in the constrained columns.



**Add Column:**

`ALTER TABLE all_users
      ADD COLUMN last_login timestamp
                 NOT NULL
                 DEFAULT NOW();`



**Remove Column:**

`ALTER TABLE all_users DROP COLUMN enabled;`

**Remove Table:**

`DROP TABLE all_users;`

Like the `CREATE TABLE` statement, the database may throw an error if the specified table does not exist,  and to suppress that error, you can use the `IF EXISTS` clause.

In addition, if you have another table that is dependent on columns in table you are removing (for example,  with a `FOREIGN KEY` dependency) then you will have to either update all dependent tables first to remove  the dependent rows or to remove those tables entirely.

| Action                             | Command                                                      | Notes                                                        |
| ---------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Add a column to a table            | ALTER TABLE table_name ADD COLUMN column_name data_type CONSTRAINTS; | Alters a table by adding a column with a specified data type and optional constraints. `ALTER TABLE` modifies the characteristics and attributes of a table. It does not actually manipulate any data, but instead  manipulates the data definitions. |
| Alter a column's data type         | ALTER TABLE table_name ALTER COLUMN column_name TYPE data_type; | Alters the table by changing the datatype of column.         |
| Rename a table                     | ALTER TABLE table_name RENAME TO new_table_name;             | ALTER COLUMN column_name<br/>TYPE new_data_type<br/>USING column_name::new_data_type |
| Rename a column within a table     | ALTER TABLE table_name RENAME COLUMN column_name TO new_column_name; | Renames a column of the specified table. ALTER COLUMN column_name TYPE new_data_type USING column_name::new_data_type |
| Add column constraint (`NOT NULL`) | ALTER TABLE table_name ALTER COLUMN column_name SET NOT NULL; | Adds a specified constraint to the specified table column. * not null is always a column constraint.  Functionally equivalent to creating a check constraint `CHECK (*`column_name`* IS NOT NULL)` |
| Add table constraint               | ALTER TABLE table_name ADD CONSTRAINT constraint_name constraint_clause; | Adds a specified constraint to the specified table.          |
| Remove a table constraint          | ALTER TABLE table_name DROP CONSTRAINT constraint_name;      | Removes a constraint from the specified table.               |
| Remove a column constraint         | ALTER TABLE table_name ALTER COLUMN column_name DROP CONSTRAINT; | Removes a constraint from the specified column. This syntax is  necessary for `NOT NULL` constraints, which aren't specifically named.     ex/  `ALTER TABLE films DROP CONSTRAINT title_length;` |
| Remove a column from a table       | ALTER TABLE table_name DROP COLUMN column_name;              | Removes a column from the specified table.                   |
| Delete a table from the database   | DROP TABLE table_name;                                       | Permanently deletes the specified table from its database.   |

| Command                                                      | Notes                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| INSERT INTO table_name (column1_name, column2_name, ...) VALUES (data_for_column1, data_for_column2, ...); | creates a new record in *table_name* with the specified columns and their associated values. manipulates the data and not the structure of the data. |
| ALTER TABLE table_name ADD UNIQUE (column_name);             | Adds a constraint to `table_name` that prevent non-unique values from being added to the table for `column_name` |
| ALTER TABLE table_name ADD CHECK (expression);               | Adds a constraint to `table_name` that prevents new rows from being added if they don't pass a *check* based on a specified expression. |

ADD CHECK example

*spectral_type is column_name*

```sql
ALTER TABLE stars
ADD CHECK (spectral_type IN ('O', 'B', 'A', 'F', 'G', 'K', 'M'))
ALTER COLUMN spectral_type SET NOT NULL;
```

**DML data manipulation language**

CRUD operations: (Create, Read, Update, Delete)

-   `INSERT INTO` statements - These add new data into a database table.
-   `SELECT` statements - Also referred to as Queries;  these retrieve existing data from database tables. We've worked with  this type a bit already.
-   `UPDATE` statements - These update existing data in a database table.
-   `DELETE` statements - These delete existing data from a database table.



**Insert Data into Table**

`INSERT INTO table_name
            (column1_name, column2_name,...)
     VALUES (data_for_column1, data_for_column2, ...);`

*must add table name, column name, values

`INSERT INTO users (full_name, enabled)
           VALUES ('John Smith', false);`

specifies which columns have which values and all other will recieve default 

*How to not include **Values** in Insert Statement*

The behavior and syntax of an `INSERT INTO` statement that does not require column names is as follows:

If no columns are specified, the statement behaves as if columns were specified in their default order within the table.

This being considered, each value of a given row within the `VALUES` clause is added to the column mapped to its position within the  sequence of values; if the number of values specified within each row is less than the number of columns in the table, then columns appearing  earlier in the default list are supplied values sequentially.

The use of `DEFAULT` keyword to facilitate auto-incrementing default SQL function `nextval`.

```sql
INSERT INTO birds
    VALUES
    (DEFAULT, 'Charlie', 3, 'Finch'),
    (DEFAULT, 'Allie', 5, 'Owl'),
    (DEFAULT, 'Jennifer', 3, 'Magpie'),
    (DEFAULT, 'Jamie', 4, 'Owl'),
    (DEFAULT, 'Roy', 8, 'Crow');
```

`INSERT INTO users (full_name)
           VALUES ('Jane Smith'), ('Harry Potter');`

This will add multiple fully_name values on separate rows 

**Acceptable Dates in PostgreSQL**

```plaintext
1999-01-08
1999-Jan-08
Jan-08-1999
08-Jan-1999
99-Jan-08
08-Jan-99
Jan-08-99
19990108
```



![Select query with condition](https://d186loudes4jlv.cloudfront.net/sql/images/select_queries/select-query-syntax.png)

**Identifiers vs Keywords**

In a SQL statement such as `SELECT enabled, full_name FROM users;` there are *identifiers* and *keywords*. The identifiers, such as `enabled`, `full_name`, and `users`, identify tables or columns within a table. The keywords, such as `SELECT` and `FROM`, tell PostgreSQL to do something specific.

Generally it's best to try and avoid naming columns the same as keywords for this very reason. If it's unavoidable however, you can double quote the identifier in your statement: `"year"`. PostgreSQL then knows to treat it specifically as an identifier rather than as a keyword.

**Ordering Selected Data**

`SELECT column_name, ...
       FROM table_name
       WHERE condition
       ORDER BY column_name;`

*false comes before true in ordering*

*DEFAULT is ASC (ascending) but we can specify DESC (descending)*

`SELECT full_name, enabled FROM users
ORDER BY enabled DESC;`

or 

`SELECT full_name, enabled FROM users
ORDER BY enabled DESC, id DESC;`

*this will sort the second that have the same values as the first*

**OPERATORS USED IN WHERE CLAUSE** 

*Operators are generally used as part of an expression in a `WHERE` clause.* ex/ `<>` (not equal), `<` (less than).  We may use all sorts of boolean conditions with `WHERE`.  The `WHERE` clause is not only used in ` SELECT` statements, it is also used in `UPDATE`, `DELETE`, etc.!

1.  Comparison
2.  Logical
3.  String Matching

`SELECT full_name, enabled, last_login
       FROM users
       WHERE id >= 2;`

**Comparison**

| Operator     | Description              |
| ------------ | ------------------------ |
| `<`          | less than                |
| `>`          | greater than             |
| `<=`         | less than or equal to    |
| `>=`         | greater than or equal to |
| `=`          | equal                    |
| `<>` or `!=` | not equal                |

**Comparison Predicates**

*behave much as operators but have special syntax.*

```
BETWEEN`, `NOT BETWEEN`, `IS DISTINCT FROM`, `IS NOT DISTINCT FROM, IS NULL, IS NOT NULL
```

You have to use `IS NULL` instead of `= NULL`

**Logical Operators**

1.  `AND`
2.  `OR`
3.  `NOT`

`SELECT * FROM users
         WHERE full_name = 'Harry Potter'
            OR enabled = 'false';`

**STRING MATCHING OPERATORS**

*often carried out using the `LIKE` operator*

| Operator   | Condition                                                    | Example                                                      |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| =          | Case sensitive exact string comparison (*notice the single equals*) | col_name = "abc"                                             |
| != or <>   | Case sensitive exact string inequality comparison            | col_name != "abcd"                                           |
| LIKE       | Case sensitive exact string comparison (ILIKE case insensitive) | col_name LIKE 'ABC'                                          |
| NOT LIKE   | Case insensitive exact string inequality comparison          | col_name NOT LIKE 'ABCD'                                     |
| %          | Used anywhere in a string to match                 a sequence of zero or more characters (only with LIKE or NOT LIKE) | col_name LIKE ''%AT%''                 (matches "AT', "ATTIC", "CAT"                     or even "BATS") |
| _          | Used anywhere in a string to match                 a single character (only with LIKE or NOT LIKE) | col_name LIKE "AN_"                 (matches 'AND", but not "AN") |
| IN (…)     | String exists in a list                                      | col_name IN ("A", "B", "C")                                  |
| NOT IN (…) | String does not exist in a list                              | col_name NOT IN ("D", "E", "F")                              |

**WHERE**

A query can be “qualified” by adding a `WHERE` clause that specifies which rows are wanted. The `WHERE` clause contains a Boolean (truth value) expression, and only rows for  which the Boolean expression is true are returned. The usual Boolean  operators (`AND`, `OR`, and `NOT`) are allowed in the qualification.

Aggregate functions cannot be used in a WHERE clause.. use a subquery

`SELECT * FROM users WHERE full_name LIKE '%Smith%';`

`LIKE %` = Wildcard; Match all users that have a full name with any number of characters followed by "Smith"; case sensitive 

`ILIKE %` = case insensitive 

`LIKE/ ILIKE _` = Wildcard for single character 

`SIMILAR TO`. It works in much the same way as `LIKE`, except that it compares the target column to a Regex (Regular Expression) pattern.

| SELECT Clause                                | Notes                                                        |
| -------------------------------------------- | ------------------------------------------------------------ |
| ORDER BY column_name [ASC, DESC]             | Orders the data selected by a column name within the associated  table. Data can be ordered in descending or ascending order; if neither  are specified, the query defaults to ascending order. The brackets  (`[]`) indicate that you can select `ASC` or `DESC`, but not both. |
| WHERE column_name [>,<, >=, <=, =, <>] value | Filters a query result based on some comparison between a  column's value and a specified literal value. There are several  comparison operators available for use, from "greater than" to "not  equal to". The brackets (`[]`) indicate that you can choose any of the  operators, but only one of them. |
| WHERE expression1 [AND, OR] expression2      | Filters a query result based whether one expression is true  [and,or] another expression is true. The brackets (`[]`) indicate that  you can choose `AND` or `OR`, but not both. |
| WHERE string_column LIKE '%substring'        | Filters a query result based on whether a substring is contained within string_column's data and has any number of characters before  that substring. Those characters are matched using the wildcard `%`. `%` doesn't have to come before a substring, you can also put it after one  as well, matching the substring first and then any number of characters  after that substring. |

**Limit, Offset, Select**

*The `LIMIT` and `OFFSET` clauses of `SELECT` are the base on which pagination is built. Let's look at how it works.*

`SELECT * FROM users LIMIT 1;`

`SELECT * FROM users LIMIT 1 OFFSET 1;` #shows second

`SELECT topic, author, publish_date, category,
       replies_count, likes_count, last_activity_date
    FROM posts
    LIMIT 12
    OFFSET 12;`

**Distinct**

`SELECT DISTINCT full_name FROM users;`

*returns only unique values*

**Functions**

In addition to querying and referencing raw column data with SQL, you can also use *expressions*  to write more complex logic on column values in a query.  These expressions can use mathematical and string functions along with basic arithmetic to transform values when the query is executed,  as shown in this physics example.

1. String

   | Function | Example                                               | Notes                                                        |
   | -------- | ----------------------------------------------------- | ------------------------------------------------------------ |
   | `length` | `SELECT length(full_name) FROM users;`                | This returns the length of every user's name. You could also use `length` in a `WHERE` clause to filter data based on name length. |
   | `trim`   | `SELECT trim(leading ' ' from full_name) FROM users;` | If any of the data in our `full_name` column had a space in front of the name, using the `trim` function like this would remove that leading space. |

2. Date/Time

   | Function    | Example                                                      | Notes                                                        |
   | ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
   | `date_part` | `SELECT full_name, date_part('year', last_login) FROM users;` | `date_part` allows us to view a table that only contains a  part of a user's timestamp that we specify. The example query allows us  to see each user's name along with the year of the `last_login` date. Sometimes having date/time data down to the second isn't needed. |
   | `age`       | `SELECT full_name, age(last_login) FROM users;`              | The `age` function, when passed a single `timestamp` as an argument, calculates the time elapsed between that timestamp and  the current time. The example query allows us to see how long it has  been since each user last logged in. |

   

3. Aggregate

   *Allow you to summarize information about a group of rows of data.*

   An aggregate function is simply a function which takes multiple values, performs some operation on them, and then produces a single value as a result. 

   ex/ **string_agg(column_name, delimiter)**

   ```
   SELECT class, string_agg(name, ‘, ‘) FROM pets GROUP BY class;    class | string_agg 
    — — — — -+ — — — — — — — — — — — — — — — — -
      mammal | coco, cinderella, django, donut
     reptile | tim, charlie, ivan
        bird | polly, olly, oswald
   ```

| Function | Example                              | Notes                                                        |
| -------- | ------------------------------------ | ------------------------------------------------------------ |
| `count`  | `SELECT count(id) FROM users;`       | Returns the number of values in the column passed in as an  argument. This type of function can be very useful depending on the  context. We could find the number of users who have enabled an account,  or even how many users have certain last names if we use the above  statement with other clauses. |
| `sum`    | `SELECT sum(id) FROM users;`         | Not to be confused with `count`. This *sums* numeric type values for all of the selected rows and returns the total. |
| `min`    | `SELECT min(last_login) FROM users;` | This returns the lowest value in a column for all of the  selected rows. Can be used with various data types such as numeric,  date/ time, and string. |
| `max`    | `SELECT max(last_login) FROM users;` | This returns the highest value in a column for all of the  selected rows. Can be used with various data types such as numeric,  date/ time, and string. |
| `avg`    | `SELECT avg(id) FROM users;`         | Returns the average (arithmetic mean) of numeric type values for all of the selected rows. |



**Group By**

`SELECT enabled, count(id) FROM users GROUP BY enabled;`

*One thing to be aware of when using aggregate functions, is that if you include columns in the column list alongside the function, then those  columns **must** also be included in a `GROUP BY` clause. 

The GROUP BY clause makes groups of rows where values in the specified columns are the same. Those groups are then used in the final output of the query.

**FUNCTIONAL DEPENDENCY OF GROUP BY**

*When GROUP BY is present, or any aggregate functions are present, it is not valid for the SELECT list expressions to refer to ungrouped columns except within aggregate functions or when the ungrouped column is functionally dependent on the grouped columns, since there would otherwise be more than one possible value to return for an ungrouped column. A functional dependency exists if the grouped columns (or a subset thereof) are the primary key of the table containing the ungrouped column.*

with **HAVING**

```
SELECT group_by_column, AGG_FUNC(*column_expression*) AS aggregate_result_alias, … FROM mytable WHERE *condition* GROUP BY column **HAVING \group_condition\**;
```

The `HAVING` clause constraints are written the same way as the `WHERE` clause constraints, and are  applied to the grouped rows.

 *`WHERE` won't work bc aggregate functions are not valid in a WHERE clause.*

```
SELECT species, count(id) FROM pets GROUP BY species HAVING count(id) > 1; species | count 
— — — — -+ — — — 
     dog | 2
     cat | 2
     owl | 2
```



**Full Query Order and Description**

## 1. `FROM` and `JOIN`s

The `FROM` clause, and subsequent `JOIN`s are first executed to determine the total working set of data that is being queried.  This includes subqueries in this clause, and can cause temporary tables to be created under the hood containing all the columns and rows of the tables being joined.

## 2. `WHERE`

Keyword/Once we have the total working set of data, the first-pass `WHERE` constraints are applied to the  individual rows, and rows that do not satisfy the constraint (condition must return true in order for the row to be returned) are discarded.  Each of the constraints can only access columns directly from the tables requested in the `FROM` clause.  Aliases in the `SELECT` part of the query are not accessible in most databases since they may include  expressions dependent on parts of the query that have not yet executed.

- `=` in SQL queries is treated as an equality operator (not assignment) , in that it compares things 

## 3. `GROUP BY`

The remaining rows after the `WHERE` constraints are applied are then grouped based on common values in the column specified in the `GROUP BY` clause.  As a result of the grouping, there will only be as  many rows as there are unique vWhat SQL keyword can be used to provide an alias for a table within a SQL statement? alues in that column.  Implicitly, this means that you should only need  to use this when you have aggregate functions in your query.

## 4. `HAVING`

If the query has a `GROUP BY` clause, then the constraints in the `HAVING` clause are then applied to the grouped rows, discard the grouped rows that don't satisfy the constraint.  Like the `WHERE`  clause, aliases are also not accessible from this step in most databases.

## 5. `SELECT`

Keyword, Any expressions in the `SELECT` part of the query are finally computed.

## 6. `DISTINCT`

Of the remaining rows, rows with duplicate values in the column marked as `DISTINCT` will be discarded.

## 7. `ORDER BY`

If an order is specified by the `ORDER BY` clause, the rows are then sorted by the specified data in  either ascending or descending order.  Since all the expressions in the `SELECT` part of the query  have been computed, you can reference aliases in this clause.

## 8. `LIMIT` / `OFFSET`

Finally, the rows that fall outside the range specified by the `LIMIT` and `OFFSET` are discarded,  leaving the final set of rows to be returned from the query.





**UPDATE DATA**

`UPDATE table_name
SET column_name = value, ...
WHERE expression;`

*The `WHERE` clause in the above syntax example is optional. If omitted, PostgreSQL will update **every** row in the target table, so before executing such a query be sure that this is actually what you want to do*

DISABLE USERS- `UPDATE users SET enabled = false;`

`UPDATE users SET enabled = true
             WHERE full_name = 'Harry Potter'
                OR full_name = 'Jane Smith';`

ESSENTIALLY DELETING ONE COLUMN VALUE:

`UPDATE table_name SET column_name1 = NULL
WHERE expression;`

**DELETE DATA**

It is prudent before deleting data, especially with a more complex condition, to run a `SELECT` query first to ensure that the `WHERE` clause is targeting the correct rows.

```sql
SELECT * FROM singers
WHERE occupation
NOT LIKE '%Singer%';
```

`DELETE FROM singers
WHERE occupation
NOT LIKE '%Singer%';`



`DELETE FROM table_name WHERE expression;`

`DELETE FROM users
WHERE full_name='Harry Potter' AND id > 3;`

DELETING ALL ROWS:

`DELETE FROM users;`

*One key difference to keep in mind between how `UPDATE` works and how `DELETE` works: with `UPDATE` you can update one or more columns within one or more rows by using the `SET` clause; with `DELETE` you can only delete one or more entire rows, and not particular pieces of data from within those rows.*

| Statement                                                    | Notes                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| UPDATE table_name SET column_name = value, ... WHERE expression; | Update specified fields within a table. The rows updated are dependent on the `WHERE` clause. We may update all rows by leaving out the `WHERE` clause. The ellipsis (`...`) indicates that we can specify as many `column_name = value` pairs as needed. |
| DELETE FROM table_name WHERE expression;                     | Delete rows in the specified table. Which rows are deleted is dependent on the `WHERE` clause. We may delete all rows by leaving out the `WHERE` clause. |

**ACCEPTABLE BOOLEANS**

Other acceptable literals are `true` or `false` without quote marks; or `'t'`, `'true'`, `'y'`, `'yes'`, `'on'`, `'1`' with quote marks for `true`, and `'f'`, `'false'`, `'n'`, `'no'`, `'off'`, `'0'` with quote marks for `false`.





**NORMALIZATION**

-   The *reason* for normalization is to reduce data redundancy and improve data integrity (**Data integrity is the overall accuracy, completeness, and consistency of data.**)

-   The *mechanism* for carrying out normalization is arranging data in multiple tables and defining relationships between them

- *Database Design* -Think at a higher level of abstraction and define entities and relationships 

- At a high level, the process of database design involves defining **entities** to represent different sorts of data and designing **relationships** between those entities.

   - An entity represents a real world object, or a set of data that we  want to model within our database; we can often identify these as the  major nouns of the system we're modeling.

     ![Simple ERD Diagram](https://d186loudes4jlv.cloudfront.net/sql/images/table_relationships/simple-erd-fixed.png)

*Entity Relationship Diagram, or **ERD**. An ERD is a  graphical representation of entities and their relationships to each  other, and is a commonly used tool within database design.*

 - **Keys**-  Keys are a special type of constraint used to establish relationships and uniqueness. They can be used to *identify a specific row in the current table*, or to *refer to a specific row in another table*. 

   - **Primary**  (unique identifier for a row of data)

     - Tables that share information about a single entity need to have a *primary key* that identifies  that entity *uniquely* across the database.  Using the `JOIN` clause in a query, we can combine row data across two separate tables using this  unique key.
     - essentially equivalent to adding `NOT NULL` and `UNIQUE` constraints to that column *serial also includes NOT NULL*
     - `ALTER TABLE users ADD PRIMARY KEY (id);`
     - Primary keys are, at a high level, a set of one or more columns that,  taken together, can uniquely identify all rows in the table. At a lower  level, they are an attribute of an SQL table - when you create the  table, for instance, you identify one column (or a collection of  columns) as the primary key.
   
   - **Foreign**
   
     - A Foreign Key allows us to associate a row in one table to a row in  another table. This is done by setting a column in one table as a  Foreign Key and having that column reference another table's Primary Key column - **REFERENCES** keyword
   
     - We say this maintains the *referential integrity* between two related tables.
   
     - Recall that a **foreign key column** is a column that stores references to a primary key column elsewhere in a database. Foreign keys usually point to other tables, but there are cases where they will point to rows in the same table.
   
     - As we saw above, foreign key columns **allow NULL values**. As a result, it is often necessary to use `NOT NULL` and a foreign key constraint together.
     
     - `CREATE TABLE orders (
         id serial PRIMARY KEY,
         product_id integer REFERENCES products (id),
       quantity integer NOT NULL
       );`
     
     - `ALTER TABLE orders ADD CONSTRAINT orders_product_id_fkey FOREIGN KEY (product_id) REFERENCES products(id);`
       
         *DEFINITION:*
         
     -  A column that represents a relationship between two rows by pointing to a specific row in another table using its *primary key*. A complete name for these columns is *foreign key column*.
     
     -   A constraint that enforces certain rules about what values are  permitted in these foreign key relationships. A complete name for this  type of constraint is *foreign key constraint*.
   
   - **Referential Integrity**
   
     - Referential integrity is the assurance that a column value within a  record must reference an existing value; if it doesn't then an error is  thrown. In other words, PostgreSQL won't allow you to add a value to the Foreign Key column of a table if the Primary Key column of the table it is referencing does not already contain that value.
     - table relationships must always be consistent

   - The **entity relationships** described above can be classified into three relationship types:

     -   one-to-one

       - A one-to-one relationship between two entities exists when a particular entity instance exists in one table, and it can have only one associated entity instance in another table.

         **Example:** A user can have only one address, and an address belongs to only one user.
   
         * `CREATE TABLE addresses (
             user_id int, -- Both a primary and foreign key
             street varchar(30) NOT NULL,
             city varchar(30) NOT NULL,
             state varchar(30) NOT NULL,
             PRIMARY KEY (user_id),
             FOREIGN KEY (user_id)
                 REFERENCES users (id)
                 ON DELETE CASCADE
           );`
           * `ON DELETE CASCADE` = if the row being referenced is deleted, the row referencing it is also deleted, ALSO `SET NULL` or `SET DEFAULT`
   
     -   one-to-many
   
       - A one-to-many relationship exists between two entities if an entity  instance in one of the tables can be associated with multiple records  (entity instances) in the other table
       - The opposite relationship does not exist; that is, each entity instance  in the second table can only be associated with one entity instance in  the first table.
       - **Example:** A review belongs to only one book. A book has many reviews.
       -  the `PRIMARY KEY` and `FOREIGN KEY` reference different columns, This means that the `FOREIGN KEY` column, `book_id` is not bound by the `UNIQUE` constraint of our `PRIMARY KEY` and so the same value from the `id` column of the `books` table can appear in this column more than once
   
     -   many-to-many (CREATE CROSS REFERENCE TABLE)

       - A many-to-many relationship exists between two entities if for one  entity instance there may be multiple records in the other table, and  vice versa.
       - **Example:** A user can check out many books. A book can be checked out by many users (over time).
       - break apart this many-to-many relationship into two one-to-many  relationships using a third, cross-reference, table (also known as a  join table)
       - Other attributes in these cross reference table (non foreign key columns) pertain to the *association* between two other entities with a many-to-many relationship

![many-to-many cross-reference table](https://d186loudes4jlv.cloudfront.net/sql/images/table_relationships/checkouts-table-references.png)





**ON DELETE CASCADE**

Use the ON DELETE CASCADE option to **specify whether you want rows deleted in a child table when corresponding rows are deleted in the parent table**. If you do not specify cascading deletes, the default behavior of the  database server prevents you from deleting data in a table if other  tables reference it.

The easiest way to prevent these problems is to **always** use the `NOT NULL` and `ON DELETE CASCADE`constraints with foreign keys in join tables. Unless there is a specific requirement to omit these constraints, you should always use them. That way, `NULL` keys are never present in the join table, and it reduces the chances that there will be references to non-existent rows. To further mitigate error, our join tables should also have a `UNIQUE (a_id, b_id)` constraint.



**ADD foreign key to existing table**

`The format for adding a Foreign Key to an existing table is:

ALTER TABLE table_name
      ADD FOREIGN KEY (column_name)
      REFERENCES other_table(other_table_primary_key);`
      

**JOIN**

One of the most important things to remember about **how joins work** is that we set a condition that compares a value from the first table (usually a primary key), with one from the second table (usually a foreign key). If the condition that uses these two values evaluates to true, then the row that holds the first value is joined with the row that holds the second value.

*`JOIN`clause is implemented by using the Primary Key of one table (either `users` or `books`) and the Foreign Key for that table*

-   The name of the first table to join
-   The type of join to use
-   The name of the second table to join
-   The join condition. (after the `ON` keyword)

`SELECT table_nameN.column_name, ...
       FROM table_name1
       join_type JOIN table_name2
                 ON join_condition;`

Join Types

1. INNER
   1. Most common (default join)
   2. joins common elements of the table (intersection where they match on the joined condition)
   3. The `INNER JOIN` is a process that matches rows from the first table and the second table which have  the same key (as defined by the `ON` constraint) to create a result row with the combined columns from both tables.  After the tables are joined, the other clauses we learned previously are then  applied.
2. LEFT OUTER
   1. Will always include the rows from the 'left' table and will return `NULL` if there is no match
3. RIGHT OUTER
   1. Will always include the rows from the 'right' table and will return `NULL` 
4. FULL OUTER (uncommon)
   1. Combination between RIGHT and LEFT JOIN
5. CROSS (uncommon aka Cartesian)

* In most cases this join condition is created using the primary key of one table and the foreign key of the table we want to join it with.

* Doesn't need an `ON` clause because it's all conditions

  * `SELECT * FROM users CROSS JOIN addresses;`

    

ex/

`SELECT colors.color, shapes.shape
       FROM colors
       JOIN shapes
            ON colors.id = shapes.color_id;`

*TRANSIENT TABLE*

![Shapes and Colors, transient join table](https://d186loudes4jlv.cloudfront.net/sql/images/joins/joins-explanation-virtual-join-table.png)

*ACTUAL TABLE*

![Shapes and Colors, resulting data](https://d186loudes4jlv.cloudfront.net/sql/images/joins/joins-explanation-query-result.png)

**Multiple JOINS**

*To join multiple tables in this way, there must be a logical relationship between the tables involved*

`SELECT users.full_name, books.title,
       checkouts.checkout_date
    FROM users
    INNER JOIN checkouts
          ON users.id = checkouts.user_id
    INNER JOIN books
          ON books.id = checkouts.book_id;`

- How does it work?
  - PostgreSQL creates a TRANSIENT TABLE that contains data from both the original table and the table identified by the `JOIN`
    - This transient table contains all the columns from the records in the `FROM` table as well as the columds from the `JOIN` table.
    - The results are then filtered on the `ON` clause
    - If there is a second, then the second is formed with the first transient table 

**ALIASING**

*Aliasing allows us to specify another name for a column or table and  then use that name in later parts of a query to allow for more concise  syntax.*

`SELECT u.full_name, b.title, c.checkout_date
       FROM users AS u
       INNER JOIN checkouts AS c
           ON u.id = c.user_id
       INNER JOIN books AS b
           ON b.id = c.book_id;`

*We can even leave out `AS` completely 

**COLUMN ALIASING**

`SELECT count(id) AS "Number of Books Checked Out"
       FROM checkouts;`

**SUBQUERIES**

Imagine executing a `SELECT` query, and then using the results of that SELECT query as a condition in *another* `SELECT` query. This is called nesting, and the query that is nested is referred to as a **subquery**.

`SELECT u.full_name FROM users u
       WHERE u.id NOT IN (
           SELECT c.user_id FROM checkouts c
       );`



EQUIVALENT TO JOIN EXPRESSION: 

`SELECT u.full_name
       FROM users u
       LEFT JOIN checkouts c ON u.id = c.user_id
       WHERE c.user_id IS NULL;`



**Subquery Expressions** (Inner queries or Nested queries)

Subqueries can exist in 3 ways: 

1. In the SELECT clause 

   1. Ex/

      1. ```sql
         SELECT customer.customer_num,
         	(SELECT SUM(ship_charge) 
         	 	FROM orders
         	 	WHERE customer.customer_num = orders.customer_num) 
         			AS total_ship_chg
         	FROM customer 
         
         ```

2. In the FROM clause

   1) EX/

      1) ```sql
         SELECT MAX(bid_counts.count) FROM
           (SELECT COUNT(bidder_id) FROM bids GROUP BY bidder_id) AS bid_counts;
         ```

      2) ```sql
         SELECT sub.*
           FROM (
                 SELECT *
                   FROM tutorial.sf_crime_incidents_2014_01
                  WHERE day_of_week = 'Friday'
                ) sub
          WHERE sub.resolution = 'NONE'
         ```

   2) You must name your subquery (in this case  `sub`) bc its being treated as a table

3. In the WHERE clause or in Conditional Logic -

   1) Most return one row - Scalar Subquery 
   2) `IN` is the only type of conditional logic that will work when the inner query contains multiple results 
   3) Don't name these subqueries bc they're being treated as a value or set of values




PostgreSQL provides a number of expressions that can be used specifically with sub-queries.  Multi-row operators. Outer query houses the inner query. Inner query executes before the outer query, so results of inner are passed to outer. This means that subqueries must actually be able to run on its own (independent)! Once the inner query runs, the outer query will run *using the results from the inner query as its underlying table*:You can use a subquery in SELECT, INSERT, DELETE, or UPDATE.

Subqueries cannot manipulate their results internally, therefore ORDER  BY clause cannot be added into a subquery. You can use an ORDER BY  clause in the main SELECT statement (outer query) which will be the last clause. 



** they all compare values to the results of a subquery**

1. `IN` compares an evaluated expression to every row in the  subquery result. If a row equal to the evaluated expression is found,  then the result of `IN` is 'true', otherwise it is 'false'.

   ```psql
   SELECT name FROM authors WHERE id IN
   (SELECT author_id FROM books
   WHERE title LIKE 'The%');
   ```
   
2. `NOT IN`

   `NOT IN` is similar to `IN` except that the result of `NOT IN` is 'true' if an equal row is **not** found, and 'false' otherwise.

   ```psql
   SELECT name FROM authors WHERE id NOT IN
   (SELECT author_id FROM books
   WHERE title LIKE 'The%');
   ```

3. `SOME`/`ANY`

   `ANY` and `SOME` are synonyms, and can be used interchangeably. These expressions are used along with an operator (e.g. `=`, `<`, `>`, etc). The result of `ANY` / `SOME` is 'true' if *any* true result is obtained when the expression to the left of the operator is evaluated using that operator against the results of the nested  query.

   Note: when the `=` operator is used with `ANY` / `SOME`, this is equivalent to `IN`.

   ```psql
   SELECT name FROM authors WHERE length(name) > ANY
   (SELECT length(title) FROM books
   (# WHERE title LIKE 'The%');
   ```

4. `ALL`

   As with `ANY` / `SOME`, `ALL` is used along with an operator. The result of `ALL` is true only if *all of* the results are true when the expression to the left of the operator is evaluated using that operator against the results of the nested query.

   Note: when the `<>` / `!=` operator is used with `ALL`, this is equivalent to `NOT IN`.

   ```psql
   SELECT name FROM authors WHERE length(name) > ALL
   (SELECT length(title) FROM books
   (# WHERE title LIKE 'The%');
   ```

5. `EXIST`

   `SELECT 1 WHERE EXISTS
   (SELECT id FROM books
   WHERE isbn = '9780316005388');`

   `EXISTS` effectively checks whether *any* rows at all are returned by the nested query. If at least one row is returned then the result of `EXISTS` is 'true', otherwise it is 'false'.
   
   ```sql
   SELECT b.name FROM bidders AS b
   
   WHERE EXISTS (SELECT bidder_id FROM bids WHERE bidder_id = b.id
   
   );
   ```
   
   

**SELECT DISTINCT**

select distinct names 



**CODE EXAMPLES**



`SELECT singers.first_name, singers.last_name, albums.album_name, albums.released
FROM singers JOIN albums
ON singers.id = albums.singer_id
WHERE albums.released >= '1980-01-01'
AND albums.released < '1990-01-01'
AND singers.deceased = false
ORDER BY singers.date_of_birth DESC;`

Joining tables with a mutual table: 

`SELECT orders.*, products.*
FROM orders JOIN order_items
ON orders.id = order_items.order_id
JOIN products
ON order_items.product_id = products.id;`

Orders links to order items which links to products 

*ADD FOREIGN KEY* 

```sql
ALTER TABLE planets
ADD COLUMN star_id integer NOT NULL REFERENCES stars (id);
```

**EXTRAS**

*Lowercase version of a string*

```psql
sql-course=# SELECT lower('AlPhAbEt');
```

*Concatenate Strings using `||`*

```
SELECT` `first_name || ‘ ‘ || last_name ``AS` `full_name
FROM` `student;
```

*Formulas with truncated(to integer) values*

```psql
sql-course=# SELECT trunc(4 * pi() * 26.3 ^ 2);
```



**EXTRA METACOMMANDS**

| Meta Command | Description                                  | Example               |
| ------------ | -------------------------------------------- | --------------------- |
| `\c $dbname` | **C**onnect to database `$dbname`.           | `\c blog_development` |
| `\d`         | **D**escribe available relations             |                       |
| `\d $name`   | **D**escribe relation `$name`                | `\d users`            |
| `\?`         | List of console commands and options         |                       |
| `\h`         | List of available SQL syntax **H**elp topics |                       |
| `\h $topic`  | SQL syntax **H**elp on syntax for `$topic`   | `\h INSERT`           |
| `\q`         | **Q**uit                                     |                       |



**FURTHER PRACTICE**

https://www.postgresql.org/docs/14/index.html

-   Official documentation is an important source of knowledge. When  putting your SQL skills into practice be sure to refer to the [PostgreSQL manual](https://www.postgresql.org/docs/current/index.html) if you get stuck.
-   We offer a variety of [exercises](https://launchschool.com/exercises#180_sql_fundamentals) on different aspects of SQL. Access to the exercises requires [registration](https://launchschool.com/sign_up) (free).
-   If you do find you need more practice, we recommend [SQL Bolt](https://sqlbolt.com/), an interactive tutorial that gives real time feedback and lets you run queries from within the SQL Bolt site. [PostgreSQL Exercises](https://pgexercises.com/) is another similar resource.
-   Another place you can practice your queries is [SQLFiddle](http://sqlfiddle.com/), which gives you a place to setup schema and test out queries all in one convenient location.

**StyleGuide**

https://www.sqlstyle.guide/





**Loading SQL File into Database** 

1. Pipe the SQL file into the `psql` program, using redirection on the command line to stream the SQL file into `psql`'s standard input

`$ psql -d my_database < file_to_import.sql`

2. If you already have a running `psql` session, though, you can import a SQL file using the `\i` meta command:

`my_database=# \i ~/some/files/file_to_import.sql`



**DUMP Make SQL File with all commands to make a file**

`pg_dump -d sql-course -t weather --inserts > dump.sql`

*where `sql-course` is the database and `weather` is the table*

**3 ways to use schema to restrict values**

1. Data type (which can include a length limitation)
2. NOT NULL Constraint
3. Check Constraint



**Keys**

1) A **natural key** is an existing value in a dataset that can be used to uniquely identify each row of data in that dataset. 

2) There are a variety of solutions to these problems, including using more than one existing value together as a **composite key**. 

3) A **surrogate key** is a value that is created solely for the purpose of identifying a row of data in a database table. Because it is created specifically for that purpose, it can avoid many of the problems associated with natural keys.

   1) auto incrementing integer

   2)  It turns out that **serial** columns in PostgreSQL are actually a short-hand for a column definition that is much longer:

      ```sql
      -- This statement:
      CREATE TABLE colors (id serial, name text);
      
      -- is actually interpreted as if it were this one:
      CREATE SEQUENCE colors_id_seq;
      CREATE TABLE colors (
          id integer NOT NULL DEFAULT nextval('colors_id_seq'),
          name text
      );
      
      or increment by 2
      
      CREATE SEQUENCE even_counter INCREMENT BY 2 MINVALUE 2;
      
      CREATE SEQUENCE sequence_name
      START WITH initial_value
      INCREMENT BY increment_value
      MINVALUE minimum value
      MAXVALUE maximum value
      CYCLE|NOCYCLE ;
      
      *Cycle will start over after max value, Nocycle will not 
      ```

*A **sequence** is a special kind of relation that generates a series of numbers. A sequence will remember the last number it generated, so it will generate numbers in a predetermined sequence automatically.*

1. All tables should have a primary key column called `id`.
2. The `id` column should automatically be set to a unique value as new rows are inserted into the table.
3. The `id` column will often be an integer, but there are other data types (such as UUIDs) that can provide specific benefits.

`CREATE SEQUENCE` statements modify the characteristics and attributes of a database by adding a sequence object to the database structure. It does not actually manipulate any data, but instead manipulates the data definitions. As such, `CREATE SEQUENCE` statements are part of the DDL sublanguage.

It could also be argued that `CREATE SEQUENCE` is DML; the sequence object it creates is a bit of data that is used to keep track of a sequence of automatically generated values, so it can be thought of as being part of the data instead of a characteristic of the data. However, all `CREATE`statements (not just `CREATE SEQUENCE`) are generally thought of as DDL.

**UUID**

UUIDs (or *universally unique identifiers*) are very large  numbers that are used to identify individual objects or, when working  with a database, rows in a database. There are a few formats and  different ways to generate these numbers (they don't increment by 1 as  we've been doing). UUIDs are often represented using hexadecimal strings with dashes such as `f47ac10b-58cc-4372-a567-0e02b2c3d479`.

If you run into UUIDs somewhere, remember that they are just really large numbers that are used to identify something uniquely.



*What will the name of the sequence created by the following SQL statement be?*

CREATE TABLE regions (id serial PRIMARY KEY, name text, area integer);

`regions_id_seq`.

**add foreign key**

`ALTER TABLE planets
ADD COLUMN star_id integer NOT NULL REFERENCES stars (id);`

*If column already exists*

`ALTER TABLE table_name
      ADD FOREIGN KEY (column_name)
      REFERENCES other_table(other_table_primary_key);`
      

**drop foreign key**

`ALTER TABLE Orders
 DROP CONSTRAINT FK_PersonOrder; `

**add primary key**

ALTER TABLE Persons
 ADD PRIMARY KEY (ID); 

**drop primary key restraint**

`ALTER TABLE films DROP CONSTRAINT films_pkey;`

**ANOMALIES**

If a contact's name or phone number needs to be changed, we'd need to update every row that contained information about that contact. This creates a situation where it would be easy to make the database inconsistent, which means that it contains more than one answer for a given question. If this occurred, it would be known as an **update anomaly**.

- We can't store the information for a contact without having placed a call to them. This is known as an **insertion anomaly**.
- Likewise, we lose all the information about a contact if we delete the history of calls to them. This is known as a **deletion anomaly**.
- **Normalization** is the process of designing schema that minimize or eliminate the possible occurrence of these anomalies. The basic procedure of normalization involves extracting data into additional tables and using foreign keys to tie it back to its associated data.



**Reserved Words**

For a full list, see http://www.postgresql.org/docs/9.5/static/sql-keywords-appendix.html. Note that there are words on that list that are "non-reserved", which  means they are allowed as table or column names but are known to the SQL parser as having a special meaning.

> As a general rule, if you get spurious parser errors for commands  that contain any of the listed key words as an identifier you should try to quote the identifier to see if the problem goes away.

**ENUMERATED DATA TYPE**

Enumerated data is anything that has finite values... so like 'happy', 'sad', 'ok'

First we have to create a type:

`CREATE TYPE mood AS ENUM ('sad', 'ok', 'happy');`

THEN...

```
CREATE TABLE person (
    name text,
    current_mood mood
);
```

we can use it just like a data_type 

If we recieve an error.. use `USING`

```sql
ALTER TABLE stars
ALTER COLUMN spectral_type TYPE spectral_type_enum
                           USING spectral_type::spectral_type_enum;
```

*The reason for this `USING` clause is that there is no defined way in PostgreSQL to convert `char` values to an enumerated type: the `USING` clause tells PostgreSQL to simply use the existing values from `spectral_type` as though they are the enumerated values.*

**DATA DUMP**

`$ pg_dump --inserts extrasolar > extrasolar.dump.sql`



**INDEXES**

- Indexes are best used in cases where sequential reading is inadequate. For example: columns that aid in mapping relationships (such as Foreign Key columns), or columns that are frequently used as part of an `ORDER BY` clause, are good candidates for indexing.
- They are best used in tables and/ or columns where the data will be read much more frequently than it is created or updated.

When you define a `PRIMARY KEY`constraint, or a `UNIQUE` constraint, on a column you automatically create an index on that column. In fact, the index is the mechanism by which these constraints enforce uniqueness.

`Indexes:  "books_pkey" PRIMARY KEY, btree (id)  "books_isbn_key" UNIQUE CONSTRAINT, btree (isbn) Foreign-key constraints:  "books_author_id_fkey" FOREIGN KEY (author_id) REFERENCES authors(id)`

In the description of the table schema, we can see two entries listed under `Indexes:`, `books_pkey` and `books_isbn_key`. The `btree`part of each entry identifies the *type* of index used (PostgreSQL uses B-tree by default for all indexes, and it is the only type available for unique indexes), followed by the name of the column that is indexed.



To create an index, say we want ot create an index for a foreign key, then we do:

`CREATE INDEX index_name ON table_name (field_name);`

`CREATE INDEX index_name ON table_name (field_name_1, field_name_2);`*more than 1*

ex/ `my_books=# CREATE INDEX ON books (author_id);`

The `books_author_id_idx` index that we added doesn't enforce uniqueness, meaning that the same value can occur multiple times in the indexed column. This is sometimes referred to as a non-unique index.

Partial indexes are built from a subset of the data in a table. The subset of data is defined by a conditional expression, and the index contains entries only for the rows from the table where the value in the indexed column satisfies the condition. Going back to our earlier `author_name` example, we could perhaps index only rows where the value `author_name` column starts with an `A`.

`di` lists indexes and names so we can drop them if we want to

`my_books=# DROP INDEX books_author_id_idx;`



**Query Plan and Explain**

In order to execute each query that it receives, PostgreSQL planner generates a **query plan**.  What the command `EXPLAIN` does is allow you to access and read that query plan.  Devising a good query plan is critical for good performance/ optimization.  We can compare the costs of running different SQL statements, which can help us with optimizing our DB calls.

```
EXPLAIN` can be used in front of a query beginning with `SELECT`, `INSERT`, `DELETE`, `REPLACE`, and `UPDATE
```

`Explain SELECT * FROM books;`

The structure of the query plan is a node-tree. The more 'elements' that there are to your query, the more nodes there will be in the tree. The example above explains a very simple query, so there is only one node in the plan tree. Each node consists of the node type (in this case a sequential scan on the `books` table) along with estimated cost for that node (start-up cost, followed by total cost), the estimated number of rows to be output by the node, and the estimated average width of the rows in bytes.  The output of `EXPLAIN` has one line for each node in the plan tree, showing the basic node type plus the cost  estimates that the planner made for the execution of that plan node.

often joins are more efficient than subqueries

An important thing to remember is that when you use `EXPLAIN`, the query is not actually run. The values that `EXPLAIN` outputs are estimates, based on the planner's knowledge of the schema and assumptions based on PostgreSQL [system statistics](https://www.postgresql.org/docs/current/static/planner-stats.html). In order to assess a query using actual data, you can add the `ANALYZE` option to an `EXPLAIN` command.  The costs are measured in arbitrary units determined by the planner's cost parameters. 

Did you notice how some nodes are nested further in than others? A  nested node represents one that is a child of the one above it. That  means that nested nodes were operations necessary to allow the parent  node(operation) to run its course.

The output of EXPLAIN has one line for each node in the plan tree,  showing the basic node type plus the cost estimates that the planner  made for the execution of that plan node. Additional lines might appear, indented from the node's summary line, to show additional properties of the node. The very first line (the summary line for the topmost node) has the  estimated total execution cost for the plan; it is this number that the  planner seeks to minimize.

Another thing to consider are the units used for describing the  estimated startup and total costs. These units are arbitrary and are  used by PostgreSQL internally to create the query plan. Their main  purpose is to give some measure of the efficiency of using certain  nodes, taking certain operations to execute a SQL statement.

`my_books=# EXPLAIN ANALYZE SELECT books.title FROM books my_books-# JOIN authors ON books.author_id = authors.id my_books-# WHERE authors.name = 'William Gibson';`

Since the SQL statement is actually run when we use `EXPLAIN ANALYZE`, the results we get from our query plan are the actual results, and not  estimates; that includes the costs and the measures of time elapsed per  operation.



*Hash Aggregate*= creates a temporary hash table for referencing rows being scanned.

.

1.  The name of the node used to perform the SQL statement. A node  represents some operation taken to run the SQL statement. An example  would be the name in the first row of our query plan, `Hash Join`
2.  The estimated startup cost and estimated total cost. These can be seen here: `Hash Join  (cost=33.38..62.84 rows=635 width=32)` The first number after `cost` is the estimated startup cost, and the second is the estimated total cost.
3.  The estimated number of rows to be shown when the SQL statement we are explaining is run. This is the number right after `rows=` above.
4.  The width is the estimated amount in bytes taken up by rows for the SQL statement we are explaining.

**SUMMARY**

- *Relational databases* are called relational because they persist data in a set of *relations*, or, as they are more commonly called, *tables*.
- A *relationship* is a connection between entity instances, or rows of data, usually resulting from what those rows of data represent.
- The three levels of schema are *conceptual*, *logical*, and *physical*.
- The three types of relationships are *one-to-one*, *one-to-many*, and *many-to-many*.
- A *conceptual schema* is a high-level design focused on identifying entities and their relationships.
- A *physical schema* is a low-level database-specific design focused on implementation.
- *Cardinality* is the number of objects on each side of the relationship.
- The *modality* of a relationship indicates if that relationship is required or not.
- *Referential integrity* is data that requires all references to be valid. That is, if a value in a column references a value in another column (usually in another table), then that value must exist in the referenced column.

**COPY DATA INTO A FILE**

1) Create new file some_file.csv

2) ex/ bidders.csv

   ```plaintext
   id, name
   1,Alison Walker
   2,James Quinn
   3,Taylor Williams
   4,Alexis Jones
   5,Gwen Miller
   6,Alan Parker
   7,Sam Carter
   ```

3) In the database: 

   ```sql
   \copy bidders FROM 'bidders.csv' WITH HEADER CSV
   ```

**type cast**

A type cast specifies a conversion from one data type to another. PostgreSQL accepts two equivalent syntaxes for type casts:

```sql
expression::type

SELECT * FROM parts WHERE strpos(part_number::text, '3') = 1;
```

Or

```sql
select * from part where  cast(part_number as text) ilike '3%';
```

When a cast is applied to a value expression of a known type, it represents a run-time type conversion. The cast will succeed only if a suitable type conversion operation has been defined. 







SELECT m.title, ((b.domestic_sales + b.international_sales)/1000000) as Gross_sales_millions FROM movies AS m 
JOIN Boxoffice AS b 
ON m.id = b.movie_id;





**USING ROW** 

If you have certain data from a row you can find other data

```sql
SELECT id FROM items
WHERE ROW('Painting', 100.00, 250.00) =
  ROW(name, initial_price, sales_price);
```

Which is the same as 

```sql
SELECT id FROM items
WHERE name = 'Painting' AND
      initial_price = 100.00 AND
      sales_price = 250.00;
```





**USING CASE IN QUERY ** 

```sql
select mems.firstname || ' ' || mems.surname as member, 
	facs.name as facility, 
	case 
		when mems.memid = 0 then
			bks.slots*facs.guestcost
		else
			bks.slots*facs.membercost
	end as cost
        from
                cd.members mems                
                inner join cd.bookings bks
                        on mems.memid = bks.memid
                inner join cd.facilities facs
                        on bks.facid = facs.facid
        where
		bks.starttime >= '2012-09-14' and 
		bks.starttime < '2012-09-15' and (
			(mems.memid = 0 and bks.slots*facs.guestcost > 30) or
			(mems.memid != 0 and bks.slots*facs.membercost > 30)
		)
order by cost desc;          
```



**CORRELATED SUBQUERY**

```sql
select distinct mems.firstname || ' ' ||  mems.surname as member,
	(select recs.firstname || ' ' || recs.surname as recommender 
		from cd.members recs 
		where recs.memid = mems.recommendedby
	)
	from 
		cd.members mems
order by member;

This exercise marks the introduction of subqueries. Subqueries are, as the name implies, queries within a query. They're commonly used with aggregates, to answer questions like 'get me all the details of the member who has spent the most hours on Tennis Court 1'.

In this case, we're simply using the subquery to emulate an outer join. For every value of member, the subquery is run once to find the name of the individual who recommended them (if any). A subquery that uses information from the outer query in this way (and thus has to be run for each row in the result set) is known as a correlated subquery.

```

