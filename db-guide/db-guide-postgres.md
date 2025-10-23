# DB guide - PostgreSQL edition

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
- [PostgreSQL official documentation](https://www.postgresql.org/docs/)
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

PostgreSQL treats unquoted identifiers as lower-case by default. Double quotes are only required if you use capitals or special characters which is best avoided

| id | column_1 | column_2 |
|---:|----------|----------|
| 1  | row 1    | cell     |
| 2  | row 2    | lorem    |
| 3  | cell     | ipsum    |

**Further learning**
- [Identifiers and quoting - PostgreSQL](https://www.postgresql.org/docs/current/sql-syntax-lexical.html#SQL-SYNTAX-IDENTIFIERS)

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

| id | planet  | moon    | mission       | categories     | date_added           |
|---:|---------|---------|---------------|----------------|----------------------|
| 1  | Jupiter | Europa  | Voyager 1     | Ice, Rocky     | 1979-03-05 12:00:00  |
| 2  | Jupiter | Io      | Voyager 1     | Volcanic       | 1979-03-05 12:05:00  |
| 3  | Saturn  | Titan   | Cassini       | Ice            | 2004-07-01 09:30:00  |
| 4  | Mars    | Phobos  | Mars Express  | Rocky          | 2004-01-10 08:00:00  |

This flat table is useful for thinking but contains duplicated information and multiple values inside single cells. We will remove those problems with normalisation

---

## Choosing data types

This step identifies the possible values for the data

Data types control the way the data is stored in the database to make it as efficient and safe as possible

A few example PostgreSQL data types

* String text
  - `varchar(n)` variable length up to `n` characters
  - `text` for unlimited length text
* Numeric
  - `integer` for whole numbers
  - `bigint` for large whole numbers
  - `numeric(p,s)` for exact decimal values
* Date and time
  - `date` for calendar dates
  - `timestamp with time zone` often abbreviated `timestamptz`
  - `timestamp without time zone` when you manage zones in the application
* Boolean
  - `boolean` with values `true` or `false`

Exact data types can vary depending on the database used

In our example scenario we might use the following data types

- **id** integer generated identity
- **name** variable length text
- **planet** variable length text
- **moon** variable length text
- **mission** variable length text
- **categories** text
- **date_added** `timestamptz` for audit columns

Modern defaults you should adopt for PostgreSQL

- Use **generated identity** columns rather than legacy `serial`
- Prefer **text** for free-form content and `varchar(n)` for constrained labels
- Use **timestamptz** for timestamps that represent real points in time

**Further learning**
- [PostgreSQL data types](https://www.postgresql.org/docs/current/datatype.html)
- [Identity columns](https://www.postgresql.org/docs/current/sql-createtable.html#SQL-CREATETABLE-IDENTITY)

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

The simplest primary key is an integer that gets generated for each new row

Sometimes we will want to reference the primary key from one table in another table in order to identify a relationship between the two. In the second table it is known as a **foreign key**

**Further learning**
- [Primary keys - Wikipedia](https://en.wikipedia.org/wiki/Primary_key)

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

***planets table***

| id | name    | discovered_at |
|---:|---------|---------------|
| 1  | Jupiter | 1610-01-07    |
| 2  | Saturn  | 1610-03-25    |

***missions table***

| id |  name       | launch_date |
|---:|-------------|-------------|
| 1  | Voyager 1   | 1977-09-05  |
| 2  | Cassini     | 1997-10-15  |

***categories table***

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

***moons table***

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

***missions_planets join table***

| id | mission_id | planet_id |
|---:|------------|-----------|
| 1  | 1          | 1         |
| 2  | 1          | 2         |
| 3  | 2          | 2         |

We will also use a many-to-many relationship for **moons to categories**

***moons_categories join table***

| id | moon_id | category_id |
|---:|---------|-------------|
| 1  | 1       | 1           |
| 2  | 1       | 2           |
| 3  | 2       | 3           |
| 4  | 3       | 1           |

**Further learning**
- [Referential integrity - PostgreSQL](https://www.postgresql.org/docs/current/ddl-constraints.html#DDL-CONSTRAINTS-FK)

---

## SQL

We have designed our database

We need to know how to create it, populate it and access this data

This is where we need SQL

Structured Query Language SQL is the language used by most databases to perform queries and manipulate data

### SQL rules

A few SQL rules to bear in mind

- SQL is generally case insensitive for keywords
- By convention SQL commands such as `SELECT` and `UPDATE` are written in uppercase
- String values should be surrounded by single quotes
- PostgreSQL does not use backticks. Use double quotes only when you need case sensitivity or special characters in identifiers which is best avoided
- All commands should terminate with a semicolon

**Further learning**
- [SQL syntax - PostgreSQL](https://www.postgresql.org/docs/current/sql-syntax.html)

---

## Creating a database

If you need to create a new database yourself, you would use the following command in a superuser or a role with createdb privilege

```
CREATE DATABASE space_data;
```

To list databases in `psql` you can use `\l`
To connect use `\c space_data`

To drop a database

```
DROP DATABASE space_data;
```

***THERE IS NO UNDO***

**Further learning**
- [CREATE DATABASE](https://www.postgresql.org/docs/current/sql-createdatabase.html)
- [DROP DATABASE](https://www.postgresql.org/docs/current/sql-dropdatabase.html)

---

## Creating database tables

We have already planned the structure for our database tables. Now we will turn these into SQL using identity columns, unique constraints and foreign keys

General pattern

```
CREATE TABLE table_name (
  column_name data_type column_constraints
);
```

Example schema for the space scenario

```
CREATE TABLE planets (
  id            integer GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
  name          varchar(100) NOT NULL,
  discovered_at date,
  CONSTRAINT uniq_planet_name UNIQUE (name)
);

CREATE TABLE moons (
  id            integer GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
  planet_id     integer NOT NULL,
  name          varchar(100) NOT NULL,
  discovered_at date,
  CONSTRAINT uniq_moon_per_planet UNIQUE (planet_id, name),
  CONSTRAINT fk_moons_planet
    FOREIGN KEY (planet_id) REFERENCES planets (id)
      ON DELETE CASCADE
);

CREATE TABLE categories (
  id       integer GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
  category varchar(100) NOT NULL,
  CONSTRAINT uniq_category UNIQUE (category)
);

CREATE TABLE moons_categories (
  id          integer GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
  moon_id     integer NOT NULL,
  category_id integer NOT NULL,
  CONSTRAINT uniq_moon_category UNIQUE (moon_id, category_id),
  CONSTRAINT fk_mc_moon
    FOREIGN KEY (moon_id) REFERENCES moons (id)
      ON DELETE CASCADE,
  CONSTRAINT fk_mc_category
    FOREIGN KEY (category_id) REFERENCES categories (id)
      ON DELETE CASCADE
);

CREATE TABLE missions (
  id          integer GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
  name        varchar(255) NOT NULL,
  launch_date date,
  CONSTRAINT uniq_mission_name UNIQUE (name)
);

CREATE TABLE missions_planets (
  id         integer GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY,
  mission_id integer NOT NULL,
  planet_id  integer NOT NULL,
  CONSTRAINT uniq_mission_planet UNIQUE (mission_id, planet_id),
  CONSTRAINT fk_mp_mission
    FOREIGN KEY (mission_id) REFERENCES missions (id)
      ON DELETE CASCADE,
  CONSTRAINT fk_mp_planet
    FOREIGN KEY (planet_id) REFERENCES planets (id)
      ON DELETE CASCADE
);
```

Taking the example of the column called `id`

```
id integer GENERATED BY DEFAULT AS IDENTITY PRIMARY KEY
```

- It will contain an integer
- This column is not allowed to be left blank
- This column acts as a unique identifier for entries in this table
- If we do not specify a value when adding a new entry, PostgreSQL will generate the next value automatically

Within a database, you can request to see what tables exist

```
SELECT tablename
FROM pg_catalog.pg_tables
WHERE schemaname = 'public';
```

You can also request to see the structure of a specific table

```
\d+ planets  -- in psql client
```

It is possible to update the structure of an existing database table using the `ALTER TABLE` command

To add a column

```
ALTER TABLE moons ADD COLUMN diameter_km integer;
```

To update the name or attributes of a column

```
ALTER TABLE missions ALTER COLUMN launch_date TYPE date;
```

To remove a column

```
ALTER TABLE moons DROP COLUMN diameter_km;
```

To empty a table use the `TRUNCATE` command

```
TRUNCATE TABLE missions_planets;
```

To delete a table use the `DROP` command

```
DROP TABLE missions_planets;
```

***THERE IS NO UNDO***

**Further learning**
- [CREATE TABLE](https://www.postgresql.org/docs/current/sql-createtable.html)
- [ALTER TABLE](https://www.postgresql.org/docs/current/sql-altertable.html)

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
INSERT INTO planets (name, discovered_at)
VALUES ('Jupiter', '1610-01-07'),
       ('Saturn',  '1610-03-25'),
       ('Mars',     NULL);
```

You can also insert multiple rows in a single SQL statement as shown above

### UPDATE

To update data in a table we use an `UPDATE` command

```
UPDATE missions
SET launch_date = '1977-09-05'
WHERE name = 'Voyager 1';
```

Note the use of the `WHERE` clause. Without this all items in the table would be updated

### DELETE

To delete data from a table we use a `DELETE` command

```
DELETE FROM moons
WHERE name = 'Io' AND planet_id = 1;
```

Note the use of the `WHERE` clause. Without this all items in the table would be deleted

***THERE IS NO UNDO***

**Further learning**
- [INSERT](https://www.postgresql.org/docs/current/sql-insert.html)
- [UPDATE](https://www.postgresql.org/docs/current/sql-update.html)
- [DELETE](https://www.postgresql.org/docs/current/sql-delete.html)

### Populating our example database tables

```
INSERT INTO planets (id, name, discovered_at) VALUES
(1, 'Jupiter', '1610-01-07'),
(2, 'Saturn',  '1610-03-25'),
(3, 'Mars',     NULL);

INSERT INTO moons (id, planet_id, name, discovered_at) VALUES
(1, 1, 'Europa', '1610-01-08'),
(2, 1, 'Io',     '1610-01-08'),
(3, 2, 'Titan',  '1655-03-25'),
(4, 3, 'Phobos', NULL),
(5, 3, 'Deimos', NULL);

INSERT INTO categories (id, category) VALUES
(1, 'Ice'),
(2, 'Rocky'),
(3, 'Volcanic');

INSERT INTO moons_categories (id, moon_id, category_id) VALUES
(1, 1, 1),
(2, 1, 2),
(3, 2, 3),
(4, 3, 1);

INSERT INTO missions (id, name, launch_date) VALUES
(1, 'Voyager 1', '1977-09-05'),
(2, 'Cassini',   '1997-10-15'),
(3, 'Mars Express', '2003-06-02');

INSERT INTO missions_planets (id, mission_id, planet_id) VALUES
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
SELECT * FROM planets;
```

Rather than returning everything, it is possible to specify just the field names columns you want

```
SELECT name, discovered_at FROM planets;
```

Multiple field names are separated by commas

```
SELECT name, discovered_at FROM planets ORDER BY name;
```

Rather than returning all results, we can add optional parameters to filter our request using `WHERE`

```
SELECT * FROM planets WHERE name = 'Mars';
```

```
SELECT name FROM moons WHERE planet_id = 1;
```

We can order our results using `ORDER BY`

```
SELECT * FROM moons ORDER BY name ASC;
```

We can change the order using `ASC` or `DESC`

```
SELECT * FROM planets WHERE id > 1 ORDER BY discovered_at DESC;
```

We can limit the number of results returned using `LIMIT`

```
SELECT * FROM moons ORDER BY name LIMIT 2;
```

We can specify an offset to start the `LIMIT` from

```
SELECT * FROM moons ORDER BY name LIMIT 2 OFFSET 2;
```

This is useful for pagination of results

We can combine conditions using `AND` and `OR`

```
SELECT
  name
FROM
  moons
WHERE
  planet_id = 1
AND
  name LIKE 'E%';
```

**Further learning**
- [SELECT syntax](https://www.postgresql.org/docs/current/sql-select.html)
- [Indexes and the planner](https://www.postgresql.org/docs/current/indexes-intro.html)

### Joining multiple tables

All of the `SELECT` examples so far have been on only a single table

When we normalised the data we specifically moved content into separate tables

Now we need to know how to recombine it

We need to add clauses to match the primary keys and foreign keys

***moons table***

| id | planet_id | name    | discovered_at |
|---:|-----------|---------|---------------|
| 1  | 1         | Europa  | 1610-01-08    |
| 2  | 1         | Io      | 1610-01-08    |
| 3  | 2         | Titan   | 1655-03-25    |

***planets table***

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
  moons AS m
JOIN
  planets AS p
ON
  m.planet_id = p.id;
```

We can then add clauses, as before

```
SELECT
  m.name AS moon,
  p.name AS planet
FROM
  moons AS m
JOIN
  planets AS p
ON
  m.planet_id = p.id
WHERE
  p.name = 'Jupiter';
```

### Many-to-many joins

List missions that visited each planet

```
SELECT
  ms.name AS mission,
  p.name  AS planet
FROM
  missions AS ms
JOIN
  missions_planets AS mp
    ON ms.id = mp.mission_id
JOIN
  planets AS p
    ON p.id = mp.planet_id
ORDER BY
  ms.name, p.name;
```

List categories for a moon

```
SELECT
  m.name AS moon,
  c.category
FROM
  moons AS m
JOIN
  moons_categories AS mc
    ON m.id = mc.moon_id
JOIN
  categories AS c
    ON c.id = mc.category_id
WHERE
  m.name = 'Europa'
ORDER BY
  c.category;
```

**Further learning**
- [JOIN types in PostgreSQL](https://www.postgresql.org/docs/current/queries-table-expressions.html#QUERIES-JOIN)

### Grouping results

If you wanted to select a list of all moons for each planet, you could perform the following query

```
SELECT
  p.name AS planet,
  m.name AS moon
FROM
  planets AS p
JOIN
  moons   AS m
ON
  p.id = m.planet_id
ORDER BY
  p.name, m.name;
```

This will produce repeated planet names, once per moon

To group the moons together in a single column use `string_agg`

```
SELECT
  p.name AS planet,
  string_agg(m.name, ', ' ORDER BY m.name) AS moon_list
FROM
  planets AS p
JOIN
  moons   AS m
ON
  p.id = m.planet_id
GROUP BY
  p.id, p.name
ORDER BY
  p.name;
```

**Further learning**
- [Aggregate functions and GROUP BY](https://www.postgresql.org/docs/current/functions-aggregate.html)

### Retrieving random results with PostgreSQL

You can select a random entry from a table using the `random()` function

Add `ORDER BY random() LIMIT 1` to the end of a query

```
SELECT * FROM planets ORDER BY random() LIMIT 1;
```

This is acceptable for small tables. On large tables it can be slow because a random value is computed for each row

**Further learning**
- [Random function](https://www.postgresql.org/docs/current/functions-math.html)

### Formatting a date with PostgreSQL

We have been storing dates in PostgreSQL using the `date` and `timestamp` data types

When these are retrieved, you can format them with `to_char`

```
SELECT
  name,
  to_char(launch_date, 'DD Mon YYYY') AS launch_pretty
FROM missions
WHERE launch_date IS NOT NULL;
```

**Further learning**
- [to_char for dates](https://www.postgresql.org/docs/current/functions-formatting.html)

---

## Indexing guidance

Indexes help PostgreSQL find rows quickly

Add indexes on columns used for joins, filters or sorting, and on foreign keys. Avoid over-indexing because each extra index slows down inserts and updates

Examples to consider in addition to unique constraints

```
CREATE INDEX idx_moons_planet ON moons (planet_id);
CREATE INDEX idx_mp_planet ON missions_planets (planet_id);
CREATE INDEX idx_mc_category ON moons_categories (category_id);
```

Use `EXPLAIN ANALYSE` to understand query performance

```
EXPLAIN ANALYSE
SELECT p.name, count(m.id)
FROM planets p
JOIN moons m ON m.planet_id = p.id
GROUP BY p.id, p.name;
```

**Further learning**
- [Introduction to indexes](https://www.postgresql.org/docs/current/indexes-intro.html)
- [Using EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html)

---

## Safer queries from applications

When running SQL from application code, always use **parameterised queries** rather than building SQL with string concatenation. This avoids SQL injection and quoting mistakes

PostgreSQL uses placeholders in prepared statements such as `$1`, `$2`

```
-- example pattern in SQL
PREPARE get_moons(integer) AS
  SELECT name FROM moons WHERE planet_id = $1;

EXECUTE get_moons(1);
```

**Further learning**
- [PREPARE and EXECUTE](https://www.postgresql.org/docs/current/sql-prepare.html)
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

- List each planet with a comma-separated list of its moons using `string_agg`
- List each mission with a comma-separated list of planets it visited
- Show the three planets with the most moons

**Further reading**
- [SQL command reference - PostgreSQL](https://www.postgresql.org/docs/current/sql-commands.html)
- [Query planning and optimisation](https://www.postgresql.org/docs/current/runtime-config-query.html)
- [A style guide for SQL](https://www.sqlstyle.guide/)
