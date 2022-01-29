---
layout: post
title: Intro to Relational Databases
subtitle: Notes from Datacamp Course
categories: Databases
tags: [Relational Databases, Intro]
---

Most of the content (and all images if not specified differently) is taken from [Introduction to relational databases in SQL](https://campus.datacamp.com/courses/introduction-to-relational-databases-in-sql) by Timo Grossenbacher.

## Prerequisites

[Introduction to SQL](https://www.datacamp.com/courses/introduction-to-sql)

## Relational Databases

- real-life *entitites* become *tables*
- reduced redundancy
- data integrity by *relationships*

### Inspecting PostgreSQL databases

- `information_schema`: 
    - a meta-database that holds information about your current database
    - has multiple tables you can query with the known SELECT * FROM syntax

`information_schema.tables`: information about all tables in your current database

```SQL
 SELECT table_schema, table_name 
 FROM information_schema.tables;
```

`information_schema.columns`: information about all columns in all of the tables in your current database

```SQL
SELECT table_name, column_name, data_type 
FROM information_schema.columns
WHERE table_name = 'pg_config';
```

### Create new tables
#### Syntax

```SQL
CREATE TABLE table_name (
    column_a data_type,
    column_b data_type,
    column_c data_type
    );
```
#### Example

```SQL
CREATE TABLE weather (
    clouds text, 
    temperature numeric, 
    weather_station char(5)
    );
```
### Add a column to table

```SQL
ALTER TABLE table_name
ADD COLUMN column_name data_type;
```

### Rename a column

```SQL
ALTER TABLE table_name
RENAME COLUMN old_name TO new_name;
```

### Drop a column

```SQL
ALTER TABLE table_name
DROP COLUMN column_name;
```

### Insert records
#### General

```SQL
 INSERT INTO table_name (column_a, column_b) 
 VALUES ("value_a", "value_b");
```

#### Migrate (distinct) data

```SQL
INSERT INTO table_name_1
SELECT DISTINCT column_name_1, column_name_2
FROM table_name_2;
```

### Delete a table

```SQL
DROP TABLE table_name;
```

## Constraints

- Constraints
    - give the data structure
    - help with consistency, and thus data quality
- PostgreSQL helps with enforcement

### Attribute constraints

#### Data types

(see [documentation of PostgreSQL](https://www.postgresql.org/docs/10/datatype.html))

- enforced on columns (i.e. attributes)
- define the so-called ***domain*** of a column
- define what operations are possible
- enforce consistent storage of values
- check out [PostgreSQL's data type](https://www.postgresql.org/docs/10/datatype.html) options
- most common types:
    - `text`: character strings of any length
    - `varchar [ (n) ]`: a maximum of `n` characters
    - `char [ (n) ]`: a fixed-length string of `n` characters
    - `boolean`: can only take three states, e.g., `TRUE`, `FALSE` and `NULL` (unknown)
    - `date`, `time` and `timestamp`: various formats for date and time calculations
    - `numeric`: arbitrary precision numbers, e.g. `3.1457`
    - `integer`: whole numbers in the range of `-2147483648` and `2147483647`

#### Casting

```SQL
CREATE TABLE weather ( 
    temperature integer,
    wind_speed text
    );
SELECT temperature * wind_speed AS wind_chill
FROM weather;
```

```OUTPUT
operator does not exist: integer * text
HINT: No operator matches the given name and argument type(s). You might need to add explicit type casts.
```

```SQL
CREATE TABLE weather ( 
    temperature integer,
    wind_speed text
    );
SELECT temperature * CAST(wind_speed AS integer) AS wind_chill
FROM weather;
```
<hr>

```SQL
SELECT CAST(some_column AS integer)
FROM table;
```

#### Alter types (after table creation)

```SQL
ALTER TABLE table_name
ALTER COLUMN column_name
TYPE integer;
```
<hr>

```SQL
ALTER TABLE table_name
ALTER COLUMN column_name
TYPE integer
-- Turns 5.54 into 6, not 5, before type conversion
USING ROUND(column_name);
```

```SQL
ALTER TABLE table_name
ALTER COLUMN column_name
TYPE varchar(x)
-- If you don't want to reserve too much space for a certain varchar column, you can truncate the values before converting its type
USING SUBSTRING(column_name FROM 1 FOR x)
```

#### not-null constraint
##### General

- disallow `NULL` values in a certain column
- must hold true for the current state of the column
- must hold true for any future state of the column

##### Meaning of Null

- unknown
- does not exist
- does not apply
- ...

##### Set null constraint

```SQL
CREATE TABLE table_name (
    unique_id integer not null
    lastname varchar(64) not null,
    home_phone integer,
    office_phone integer
    );
```

```SQL
ALTER TABLE table_name
ALTER COLUMN home_phone
SET NOT NULL
```

##### Remove null constraint

```SQL
ALTER TABLE table_name
ALTER COLUMN lastname
DROP NOT NULL
```

#### unique constraint

##### General

- disallow duplicate values in a column
- must hold true for the current state of the column
- must hold true for any future state of the column

##### Adding unique constraints

```SQL
CREATE TABLE table_name (
    column_name UNIQUE
    );
```

```SQL
ALTER TABLE table_name
-- you have to give a name to the constraint (some_name)
ADD CONSTRAINT some_name UNIQUE(column_name);
```

### Key constraints



### Referential integrity constraints
