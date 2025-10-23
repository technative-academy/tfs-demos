# DB guide - MySQL edition

> _These notes are not intended as a comprehensive guide to the topic. Their purpose is to guide you through the main areas you should learn about, with resources provided for further exploration. The goal is for you to learn enough to complete the associated challenge._

## Why use a database

When building web applications, we often use a database to store information

We want to store our application data separately from

- application logic such as Python or Node.js
- presentation such as HTML templates

### Advantages

There are a number of advantages for separating information from presentation

- Easier to manage content without changing logic
- Data can be re-used elsewhere
- Data can be managed via an administrative tool such as a content management system with little or no technical knowledge required
- Databases are optimised to store and retrieve data quickly
- Databases help maintain data integrity with constraints and transactions


**Further learning**
- [MySQL introduction](https://dev.mysql.com/doc/refman/8.0/en/introduction.html)
- [What is a database - Wikipedia](https://en.wikipedia.org/wiki/Database)

---

## Database essentials

A database is just a collection of one or more tables of data

- Each table has a number of **columns** also known as fields or attributes
- Each column has a specific **name**
- Each column also has a data **type** such as text, number, date or time
- Data is stored in a table in **rows**
- Each individual column within a row is called a **cell**

Database field names do not usually contain spaces. Conventions usually suggest making them all lower-case and using underscores to separate words

| id | column_1 | column_2 |
|---:|----------|----------|
| 1  | row 1    | cell     |
| 2  | row 2    | lorem    |
| 3  | cell     | ipsum    |

**Further learning**
- [MySQL identifiers and naming](https://dev.mysql.com/doc/refman/8.0/en/identifiers.html)

---

## An example scenario

The following notes will be based around designing a database to meet an example scenario

*Design a database for a web application that records planets, their moons, and space missions that visit those planets. Moons can be assigned to one or more categories such as Ice, Rocky or Volcanic*

This scenario lets us demonstrate one-to-many and many-to-many relationships clearly

---

## Database design process

We can design our database by following a few simple steps

1. Decide on what data you want to store
2. Choose data types for each of these items of information
3. Normalise the data

These notes will then explain how to

1. Create your database
2. Populate your database
3. Query your database

**Further learning**
- [Database design basics](https://support.microsoft.com/en-us/office/database-design-basics-eb2159cf-1e30-401a-8084-bd4f9c9ca1f5)

---

## Storing data

When designing a database, it is important to first decide what data we want to store

If we were to imagine our example data in tabular form, we might have something like this

| id | planet  | moon    | mission     | categories     | date_added          |
|---:|---------|---------|-------------|----------------|---------------------|
| 1  | Jupiter | Europa  | Voyager 1   | Ice, Rocky     | 1979-03-05 12:00:00 |
| 2  | Jupiter | Io      | Voyager 1   | Volcanic       | 1979-03-05 12:05:00 |
| 3  | Saturn  | Titan   | Cassini     | Ice            | 2004-07-01 09:30:00 |
| 4  | Mars    | Phobos  | Mars Express| Rocky          | 2004-01-10 08:00:00 |

This flat table is useful for thinking but contains duplicated information and multiple values inside single cells. We will remove those problems with normalisation

---

## Choosing data types

This step identifies the possible values for the data

Data types control the way the data is stored in the database to make it as efficient and safe as possible

A few example MySQL data types

* String text
  - `CHAR(n)` fixed length up to 255 characters
  - `VARCHAR(n)` variable length up to 65,535 bytes depending on row size
  - `TEXT` for longer text
* Numeric
  - `INT` for whole numbers
  - `BIGINT` for large whole numbers
  - `DECIMAL(p,s)` for exact decimal values
* Date and time
  - `DATE` for calendar dates
  - `DATETIME` for timestamp without timezone
  - `TIMESTAMP` for server-time tracked timestamp

Exact data types can vary depending on the database used

In our example scenario we might use the following data types

- **id** integer
- **name** variable length text
- **planet** variable length text
- **moon** variable length text
- **mission** variable length text
- **categories** text
- **date_added** date and time

Modern defaults you should adopt for MySQL 8

- Use **InnoDB** as the storage engine so that foreign keys and transactions are supported
- Use **utf8mb4** character set and a modern collation such as `utf8mb4_0900_ai_ci` so that all Unicode characters are supported

**Further learning**
- [MySQL data types](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)
- [MySQL character sets](https://dev.mysql.com/doc/refman/8.0/en/charset-general.html)

---

## Data normalisation

To normalise data is to remove the duplication of information so each piece of information is stored only once

Once we have removed repetition of data we have removed the possibility of inconsistencies

This ensures that the integrity of the data is maintained

*What this means*

- Any repetitive data should be stored in a separate database table
- Each table should contain data about one thing only

To normalise data also means to ungroup items of data so each cell contains only a single item of data

*What this means*

- Any cells containing multiple items of data should be broken out into a separate table and linked with foreign keys

**Further reading**
- [Third normal form explained](http://phlonx.com/resources/nf3/)
- [Database normalisation - Wikipedia](https://en.wikipedia.org/wiki/Database_normalization)
- [An introduction to database normalisation](https://www.geeksforgeeks.org/normal-forms-in-dbms/)

### Limiting normalisation

In a fully normalised database there should be no duplication of information

However this can sometimes fragment or over-complicate the data, and unnecessarily separate items of information which then need to be brought together in order to answer queries

The database designer may sometimes prefer to have a database which is not strictly normalised so as to simplify the system or improve query performance

**Further reading**
- [Maybe normalising is not normal - Coding Horror](https://blog.codinghorror.com/maybe-normalizing-isnt-normal/)

---

## Primary keys

In every table, we must identify or create a unique ID known as a primary key

A primary key has three requirements

1. It must always have a value and cannot be left blank
2. Its value must never change
3. It must be unique

A primary key must be a unique value which enables us to identify a single row of data and so access all other data related to it

If none of the items of data are unique they cannot act as a primary key

The simplest primary key is an integer that gets incremented for each new row

Sometimes we will want to reference the primary key from one table in another table in order to identify a relationship between the two. In the second table it is known as a **foreign key**

**Further learning**
- [Primary keys - Wikipedia](https://en.wikipedia.org/wiki/Primary_key)
- [MySQL indexes and primary keys](https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html)

---

## Entities and attributes

For any scenario where you want to use a database, you need to identify the entities and attributes

### Entities

Should be representations of real-world objects such as events, persons, places and things

For the space scenario these are good candidates

- planets
- moons
- missions
- categories

Each entity should have its own table in the database

It is not an easy science to correctly identify entities. It is dependant on the scenario and often subjective

Once we have identified the entities, we can create a database table for each

### Attributes

Pieces of information which characterise and describe these entities

These become the fields or columns for each entity table in the database

You need to identify the name of the attribute such as `name`, `launch_date`, `category`

You need to identify the attribute type such as text, integer, date or similar

You need to decide whether the attribute is optional. Can it be empty

Ask whether the attribute can uniquely identify the entity

---

## Example database tables

Here are three simple example tables before we add relationships

***Planets table***

| id | name    | discovered_at |
|---:|---------|---------------|
| 1  | Jupiter | 1610-01-07    |
| 2  | Saturn  | 1610-03-25    |

***Missions table***

| id |  name       | launch_date |
|---:|-------------|-------------|
| 1  | Voyager 1   | 1977-09-05  |
| 2  | Cassini     | 1997-10-15  |

***Categories table***

| id | category |
|---:|----------|
| 1  | Ice      |
| 2  | Rocky    |
| 3  | Volcanic |

---

## Relationships

It is important to identify the relationships between tables

There are three types of relationship

1. One-to-one 1:1
2. One-to-many 1:N
3. Many-to-many N:M

### One-to-many 1:N relationships

To identify a one-to-many relationship, we use primary key to foreign key matching

We store the primary key of the one side as a foreign key in each of the many items, establishing the relationship between them

Matching keys in this way allows related information to be brought together from different tables when the database is queried

In our example, planets to moons is a one-to-many relationship. For each planet there are multiple moons, but each moon belongs to only one planet

Instead of adding the planet name to each moon row repeatedly, we will store planet details in the `planets` table

We will add a new field to the `moons` table called `planet_id`. Here we will put the unique primary key from the planet table as a foreign key in the moon table

Now the planet details need only be stored once. If the planet name were to change, we would only need to update a single record in the planet table and it would apply for all related moons

Here is our example **moons** table including the foreign key to tie the one-to-many relationship

***Moons table***

| id | planet_id | name    | discovered_at |
|---:|-----------|---------|---------------|
| 1  | 1         | Europa  | 1610-01-08    |
| 2  | 1         | Io      | 1610-01-08    |
| 3  | 2         | Titan   | 1655-03-25    |

### Many-to-many N:M relationships

For a many-to-many relationship, on both sides of the relationship there can be multiple entities in each table that are inter-related

For example, one mission may visit several planets and one planet may be visited by several missions

To record this relationship we create a separate database table containing two foreign keys which relate to the primary keys for each of the two relevant entities

Here is our **missions to planets** join table

***Missions to Planets join table***

| id | mission_id | planet_id |
|---:|------------|-----------|
| 1  | 1          | 1         |
| 2  | 1          | 2         |
| 3  | 2          | 2         |

We will also use a many-to-many relationship for **moons to categories**

***Moons to Categories join table***

| id | moon_id | category_id |
|---:|---------|-------------|
| 1  | 1       | 1           |
| 2  | 1       | 2           |
| 3  | 2       | 3           |
| 4  | 3       | 1           |

**Further learning**
- [MySQL foreign keys and referential integrity](https://dev.mysql.com/doc/refman/8.0/en/innodb-foreign-key-constraints.html)

---

## SQL

We have designed our database

We need to know how to create it, populate it and access this data

This is where we need SQL

Structured Query Language SQL is the language used by most databases to perform queries and manipulate data

### SQL rules

A few SQL rules to bear in mind

- SQL is generally case insensitive
- By convention SQL commands such as `SELECT` and `UPDATE` are written in uppercase
- String values should be surrounded by quotes. Single quotes are standard
- Table and column names can optionally be surrounded by backticks in MySQL. This helps when names might clash with reserved words
- All commands should terminate with a semicolon

**Further learning**
- [MySQL SQL syntax reference](https://dev.mysql.com/doc/refman/8.0/en/sql-statements.html)

---

## Creating a database

If you need to create a new database yourself, you would use the following command

```
CREATE DATABASE `space_data`
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_0900_ai_ci;
```

To see a list of all available databases you would enter

```
SHOW DATABASES;
```

To select a database you would enter

```
USE `space_data`;
```

To delete a database you would enter

```
DROP DATABASE `space_data`;
```

***THERE IS NO UNDO***

**Further learning**
- [CREATE DATABASE](https://dev.mysql.com/doc/refman/8.0/en/create-database.html)
- [DROP DATABASE](https://dev.mysql.com/doc/refman/8.0/en/drop-database.html)

---

## Creating database tables

We have already planned the structure for our database tables. Now we will turn these into SQL

General pattern

```
CREATE TABLE `table_name` (
  `column_name` column_type column_attributes
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

Example schema for the space scenario using modern MySQL features such as InnoDB, utf8mb4, unique constraints and foreign keys

```
CREATE TABLE `planets` (
  `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `name` VARCHAR(100) NOT NULL,
  `discovered_at` DATE NULL,
  UNIQUE KEY `uniq_planet_name` (`name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

CREATE TABLE `moons` (
  `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `planet_id` INT NOT NULL,
  `name` VARCHAR(100) NOT NULL,
  `discovered_at` DATE NULL,
  UNIQUE KEY `uniq_moon_per_planet` (`planet_id`, `name`),
  CONSTRAINT `fk_moons_planet`
    FOREIGN KEY (`planet_id`) REFERENCES `planets` (`id`)
    ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

CREATE TABLE `categories` (
  `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `category` VARCHAR(100) NOT NULL,
  UNIQUE KEY `uniq_category` (`category`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

CREATE TABLE `moons_categories` (
  `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `moon_id` INT NOT NULL,
  `category_id` INT NOT NULL,
  UNIQUE KEY `uniq_moon_category` (`moon_id`, `category_id`),
  CONSTRAINT `fk_mc_moon`
    FOREIGN KEY (`moon_id`) REFERENCES `moons` (`id`)
    ON DELETE CASCADE,
  CONSTRAINT `fk_mc_category`
    FOREIGN KEY (`category_id`) REFERENCES `categories` (`id`)
    ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

CREATE TABLE `missions` (
  `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `name` VARCHAR(255) NOT NULL,
  `launch_date` DATE NULL,
  UNIQUE KEY `uniq_mission_name` (`name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

CREATE TABLE `missions_planets` (
  `id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  `mission_id` INT NOT NULL,
  `planet_id` INT NOT NULL,
  UNIQUE KEY `uniq_mission_planet` (`mission_id`, `planet_id`),
  CONSTRAINT `fk_mp_mission`
    FOREIGN KEY (`mission_id`) REFERENCES `missions` (`id`)
    ON DELETE CASCADE,
  CONSTRAINT `fk_mp_planet`
    FOREIGN KEY (`planet_id`) REFERENCES `planets` (`id`)
    ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

Taking the example of the column called `id`

```
`id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY
```

- It will contain an integer
- This column is not allowed to be left blank
- This column acts as a unique identifier for entries in this table
- If we do not specify a value when adding a new entry, MySQL will pick the next integer value automatically

Within a database, you can request to see what tables exist

```
SHOW TABLES;
```

You can also request to see the structure of a specific table

```
DESCRIBE `planets`;
```

It is possible to update the structure of an existing database table using the `ALTER TABLE` command

To add a column

```
ALTER TABLE `moons` ADD `diameter_km` INT NULL;
```

To update the name or attributes of a column

```
ALTER TABLE `missions` CHANGE `launch_date` `launch_date` DATE NULL;
```

To remove a column

```
ALTER TABLE `moons` DROP `diameter_km`;
```

To empty a table use the `TRUNCATE` command

```
TRUNCATE TABLE `missions_planets`;
```

To delete a table use the `DROP` command

```
DROP TABLE `missions_planets`;
```

***THERE IS NO UNDO***

**Further learning**
- [CREATE TABLE](https://dev.mysql.com/doc/refman/8.0/en/create-table.html)
- [ALTER TABLE](https://dev.mysql.com/doc/refman/8.0/en/alter-table.html)
- [DESCRIBE and SHOW](https://dev.mysql.com/doc/refman/8.0/en/show.html)

---

## Populating a database

Our database and tables are now ready to go

We need to know how to populate them with data and then retrieve this data

### CRUD

Data-related tasks broadly fall into one of four categories

- Create new data in a database
- Request or Read data from a database
- Update existing data in a database
- Delete data from a database

SQL allows us to do just that

- Create equals `INSERT`
- Request equals `SELECT`
- Update equals `UPDATE`
- Delete equals `DELETE`

### INSERT

To add data to the tables we have created, we use an `INSERT` command

```
INSERT INTO `planets` (`name`, `discovered_at`)
VALUES ('Jupiter', '1610-01-07'),
       ('Saturn',  '1610-03-25'),
       ('Mars',    NULL);
```

You can also insert multiple rows in a single SQL statement as shown above

### UPDATE

To update data in a table we use an `UPDATE` command

```
UPDATE `missions`
SET `launch_date` = '1977-09-05'
WHERE `name` = 'Voyager 1';
```

Note the use of the `WHERE` clause. Without this all items in the table would be updated

### DELETE

To delete data from a table we use a `DELETE` command

```
DELETE FROM `moons`
WHERE `name` = 'Io' AND `planet_id` = 1;
```

Note the use of the `WHERE` clause. Without this all items in the table would be deleted

***THERE IS NO UNDO***

**Further learning**
- [INSERT](https://dev.mysql.com/doc/refman/8.0/en/insert.html)
- [UPDATE](https://dev.mysql.com/doc/refman/8.0/en/update.html)
- [DELETE](https://dev.mysql.com/doc/refman/8.0/en/delete.html)

### Populating our example database tables

```
INSERT INTO `planets` (`id`, `name`, `discovered_at`) VALUES
(1, 'Jupiter', '1610-01-07'),
(2, 'Saturn',  '1610-03-25'),
(3, 'Mars',     NULL);

INSERT INTO `moons` (`id`, `planet_id`, `name`, `discovered_at`) VALUES
(1, 1, 'Europa', '1610-01-08'),
(2, 1, 'Io',     '1610-01-08'),
(3, 2, 'Titan',  '1655-03-25'),
(4, 3, 'Phobos', NULL),
(5, 3, 'Deimos', NULL);

INSERT INTO `categories` (`id`, `category`) VALUES
(1, 'Ice'),
(2, 'Rocky'),
(3, 'Volcanic');

INSERT INTO `moons_categories` (`id`, `moon_id`, `category_id`) VALUES
(1, 1, 1),
(2, 1, 2),
(3, 2, 3),
(4, 3, 1);

INSERT INTO `missions` (`id`, `name`, `launch_date`) VALUES
(1, 'Voyager 1', '1977-09-05'),
(2, 'Cassini',   '1997-10-15'),
(3, 'Mars Express', '2003-06-02');

INSERT INTO `missions_planets` (`id`, `mission_id`, `planet_id`) VALUES
(1, 1, 1),
(2, 1, 2),
(3, 2, 2),
(4, 3, 3);
```

---

## Querying a database

To read data from a table or multiple tables we use a `SELECT` command

The simplest `SELECT` command will return everything in a database table

```
SELECT * FROM `planets`;
```

Rather than returning everything, it is possible to specify just the field names columns you want

```
SELECT `name`, `discovered_at` FROM `planets`;
```

Multiple field names are separated by commas

```
SELECT `name`, `discovered_at` FROM `planets` ORDER BY `name`;
```

Rather than returning all results, we can add optional parameters to filter our request using `WHERE`

```
SELECT * FROM `planets` WHERE `name` = 'Mars';
```

```
SELECT `name` FROM `moons` WHERE `planet_id` = 1;
```

We can order our results using `ORDER BY`

```
SELECT * FROM `moons` ORDER BY `name` ASC;
```

We can change the order using `ASC` or `DESC`

```
SELECT * FROM `planets` WHERE `id` > 1 ORDER BY `discovered_at` DESC;
```

We can limit the number of results returned using `LIMIT`

```
SELECT * FROM `moons` ORDER BY `name` LIMIT 2;
```

This will return the first two records in the specified sort order

We can specify an offset to start the `LIMIT` from

```
SELECT * FROM `moons` ORDER BY `name` LIMIT 2 OFFSET 2;
```

This will return two records, starting from record three. This is useful for pagination of results

We can combine conditions using `AND` and `OR`

```
SELECT
  `name`
FROM
  `moons`
WHERE
  `planet_id` = 1
AND
  `name` LIKE 'E%';
```

**Further learning**
- [SELECT syntax](https://dev.mysql.com/doc/refman/8.0/en/select.html)
- [WHERE clause](https://dev.mysql.com/doc/refman/8.0/en/where-optimizations.html)

### Joining multiple tables

All of the `SELECT` examples so far have been on only a single table

When we normalised the data we specifically moved content into separate tables

Now we need to know how to recombine it

We need to add clauses to match the primary keys and foreign keys

***Moons table***

| id | planet_id | name    | discovered_at |
|---:|-----------|---------|---------------|
| 1  | 1         | Europa  | 1610-01-08    |
| 2  | 1         | Io      | 1610-01-08    |
| 3  | 2         | Titan   | 1655-03-25    |

***Planets table***

| id | name    | discovered_at |
|---:|---------|---------------|
| 1  | Jupiter | 1610-01-07    |
| 2  | Saturn  | 1610-03-25    |

**SELECT with an explicit join preferred**

```
SELECT
  m.id,
  m.name     AS moon,
  p.name     AS planet,
  m.discovered_at
FROM
  `moons` AS m
JOIN
  `planets` AS p
ON
  m.`planet_id` = p.`id`;
```

| id | moon   | planet  | discovered_at |
|---:|--------|---------|---------------|
| 1  | Europa | Jupiter | 1610-01-08    |
| 2  | Io     | Jupiter | 1610-01-08    |
| 3  | Titan  | Saturn  | 1655-03-25    |

We can then add clauses, as before

```
SELECT
  m.name AS moon,
  p.name AS planet
FROM
  `moons` AS m
JOIN
  `planets` AS p
ON
  m.`planet_id` = p.`id`
WHERE
  p.`name` = 'Jupiter';
```

**SELECT without explicit joins legacy syntax**

You may also see legacy syntax that lists tables separated by commas and uses `WHERE` to join. This is functionally the same as an inner join but modern code should use explicit `JOIN` as above for clarity

```
SELECT
  m.name AS moon,
  p.name AS planet
FROM
  `moons` AS m, `planets` AS p
WHERE
  m.`planet_id` = p.`id`;
```

**Further learning**
- [MySQL joins](https://dev.mysql.com/doc/refman/8.0/en/join.html)
- [Relational joins overview - Wikipedia](https://en.wikipedia.org/wiki/Join_(SQL))

### Multiple tables in a query and aliasing

When we query across multiple tables the attributes from each table are flattened into a single result set

There may be times when there are fields that we want to retrieve that have identical column names in more than one table for example `id`

If we try to do this, it will only return one of the named columns in some clients or it will be ambiguous. To resolve this we use `AS` in our SQL to alias the field names to something else to make them unique

```
SELECT
  p.`id`   AS `planet_id`,
  p.`name` AS `planet`,
  m.`id`   AS `moon_id`,
  m.`name` AS `moon`
FROM
  `planets` AS p
JOIN
  `moons`   AS m
ON
  p.`id` = m.`planet_id`;
```

### Many-to-many joins

List missions that visited each planet

```
SELECT
  ms.`name` AS mission,
  p.`name`  AS planet
FROM
  `missions` AS ms
JOIN
  `missions_planets` AS mp
ON
  ms.`id` = mp.`mission_id`
JOIN
  `planets` AS p
ON
  p.`id` = mp.`planet_id`
ORDER BY
  ms.`name`, p.`name`;
```

List categories for a moon

```
SELECT
  m.`name` AS moon,
  c.`category`
FROM
  `moons` AS m
JOIN
  `moons_categories` AS mc
ON
  m.`id` = mc.`moon_id`
JOIN
  `categories` AS c
ON
  c.`id` = mc.`category_id`
WHERE
  m.`name` = 'Europa'
ORDER BY
  c.`category`;
```

**Further reading**
- [MySQL join types](https://dev.mysql.com/doc/refman/8.0/en/join.html)

### Grouping results

If you wanted to select a list of all moons for each planet, you could perform the following query

```
SELECT
  p.`name` AS planet,
  m.`name` AS moon
FROM
  `planets` AS p
JOIN
  `moons` AS m
ON
  p.`id` = m.`planet_id`
ORDER BY
  p.`name`, m.`name`;
```

This will produce repeated planet names, once per moon

To group the moons together in a single column use `GROUP_CONCAT`

```
SELECT
  p.`name` AS planet,
  GROUP_CONCAT(m.`name` ORDER BY m.`name` SEPARATOR ', ') AS `moon_list`
FROM
  `planets` AS p
JOIN
  `moons` AS m
ON
  p.`id` = m.`planet_id`
GROUP BY
  p.`id`, p.`name`
ORDER BY
  p.`name`;
```

**Further learning**
- [Aggregate functions and GROUP BY](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html)

### Retrieving random results with MySQL

You can select a random entry from a MySQL table using the `RAND()` function

Add `ORDER BY RAND() LIMIT 1` to the end of a query

```
SELECT * FROM `planets` ORDER BY RAND() LIMIT 1;
```

This is acceptable for small tables. On large tables it can be slow because a random value is computed for each row

**Further learning**
- [RAND function](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_rand)

### Formatting a date with MySQL

We have been storing dates in MySQL using the `DATE` and `DATETIME` data types

When these are retrieved from MySQL

```
SELECT `discovered_at` FROM `planets`;
```

The output is in the format `YYYY-MM-DD` or `YYYY-MM-DD hh:mm:ss`

If you want to format this you can use `DATE_FORMAT`

```
SELECT
  `name`,
  DATE_FORMAT(`discovered_at`, '%e/%c/%y') AS `discovered_short`
FROM
  `planets`
WHERE
  `discovered_at` IS NOT NULL;
```

**Further learning**
- [DATE_FORMAT](https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_date-format)

---

## Indexing guidance

Indexes help MySQL find rows quickly

Add indexes on columns used for joins, filters or sorting, and on foreign keys. Avoid over-indexing because each extra index slows down inserts and updates

Examples already included in the schema

- `uniq_planet_name` enforces unique planet names
- `uniq_moon_per_planet` prevents duplicate moon names per planet
- Foreign keys are indexed automatically on the referenced side but you may add explicit indexes to the child side for performance if needed

**Further learning**
- [How MySQL uses indexes](https://dev.mysql.com/doc/refman/8.0/en/mysql-indexes.html)
- [Optimising queries](https://dev.mysql.com/doc/refman/8.0/en/optimization.html)

---

## Safer queries from applications

When running SQL from application code, always use **parameterised queries** rather than building SQL with string concatenation. This avoids SQL injection and quoting mistakes

**Further learning**
- [OWASP SQL injection prevention cheat sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)

---

## Practice

Try to write the SQL queries that would satisfy the following requests

- Select all planets
- Select all moons for the planet named Saturn
- Select all missions that visited Mars ordered by launch date
- For the moon named Europa, list its categories
- Count moons per planet and show only planets with at least two moons
- Add a new mission called Galileo that visited Jupiter and Saturn
- Rename the category Ice to Icy
- Delete the moon-category link that incorrectly marked Titan as Volcanic

**Stretch tasks**

- List each planet with a comma-separated list of its moons using `GROUP_CONCAT`
- List each mission with a comma-separated list of planets it visited
- Show the three planets with the most moons

**Further learning**
- [SQL style guide inspiration](https://www.sqlstyle.guide/)
