
# Introduction

## PostgreSQL Database: SQL Fundamentals I

---

## Lesson Objectives

After completing this lesson, you should be able to:

* Identify the development environments used in this course
* Describe the database and schema used in this course
* Understand the goals of the course
* List the features of PostgreSQL Database
* Discuss theoretical and physical aspects of a relational database
* Describe PostgreSQL server’s implementation of:

  * RDBMS
  * Object-Relational Database Management System

---

## Relational and Object-Relational Database Management Systems

* Relational model and object-relational model
* User-defined data types and objects
* Fully compatible with relational database
* Supports multimedia and large objects
* High-quality database server features





---

## Data Storage on Different Media


Data can be stored in:

* Electronic spreadsheets
* Filing cabinets (manual storage)
* Databases (structured digital storage)

Databases provide structured, scalable, and secure storage compared to other methods.

---

## Relational Database Concept

* Proposed by **Dr. E. F. Codd (1970)**
* Basis for the Relational Database Management System (RDBMS)
* Consists of:

  * Collection of relations (tables)
  * Set of operators to act on relations
  * Data integrity rules for accuracy and consistency



---

## Definition of a Relational Database

A **relational database** is a collection of relations (two-dimensional tables).

Example tables:

* `EMPLOYEES`
* `DEPARTMENTS`

Each table consists of rows and columns.

---

## Data Models

* Client’s mental model
* Entity model
* Table model (physical implementation)
* Database server stores tables on disk

The progression:

> Business Concept → Entity Model → Tables → Database Storage

---

## Entity Relationship (ER) Model

Scenario example:

> "Assign one or more employees to a department."
> "Some departments may not have employees."

### Entities:

* `EMPLOYEE`
* `DEPARTMENT`

### Attributes:

* Employee: number, name, job title
* Department: number, name, location

Relationships:

* Employee **assigned to** Department
* Department **composed of** Employees

---

## Entity Relationship Modeling Conventions

### Entity

* Singular name
* Uppercase
* Unique
* Represented in a soft box

### Unique Identifier (UID)

* Primary marked with `#`
* Secondary marked with `(#)`

### Attribute

* Singular name
* Lowercase
* `*` Mandatory
* `o` Optional

---

## Relating Multiple Tables

* Each row is uniquely identified by a **Primary Key**
* Tables relate using **Foreign Keys**

Example:

* `employees.department_id` → references `departments.department_id`

---

## Relational Database Terminology

Key terms:

* Table (Relation)
* Row (Tuple)
* Column (Attribute)
* Primary Key
* Foreign Key
* Schema

---

## Using SQL to Query Your Database

Structured Query Language (SQL) is:

* ANSI standard language
* Efficient and easy to use
* Functionally complete
* Used to define, retrieve, and manipulate data

Example:

```sql
SELECT department_name
FROM departments;
```

---

## SQL Statement Categories

### DML (Data Manipulation Language)

* SELECT
* INSERT
* UPDATE
* DELETE
* MERGE

### DDL (Data Definition Language)

* CREATE
* ALTER
* DROP
* RENAME
* TRUNCATE

### DCL (Data Control Language)

* GRANT
* REVOKE

### Transaction Control

* COMMIT
* ROLLBACK
* SAVEPOINT

---

## The Human Resources (HR) Schema

Core tables used:

* EMPLOYEES
* DEPARTMENTS
* JOBS
* JOB_HISTORY
* LOCATIONS
* COUNTRIES
* REGIONS
* JOB_GRADES

---

## Tables Used in the Course

Primary tables:

* **EMPLOYEES**
* **DEPARTMENTS**
* **JOB_GRADES**

These tables are used throughout the SQL lessons for demonstrations and practice.

---

# Summary

In this introduction, you learned:

* What a relational database is
* The relational and object-relational models
* ER modeling basics
* Keys and table relationships
* SQL fundamentals
* HR schema structure

---


# Chapter 1 – Retrieving Data Using the SQL SELECT Statement

---

## 1.1 – Title

# Retrieving Data Using the SQL SELECT Statement

---

## 1.2 – Objectives

After completing this lesson, you should be able to:

* List the capabilities of SQL SELECT statements
* Execute a basic SELECT statement

---

## 1.3 – Capabilities of SQL SELECT Statements

* **Projection** (select specific columns)
* **Selection** (select specific rows)
* **Join** (combine multiple tables)

---

## 1.4 – Basic SELECT Statement

* `SELECT` identifies the columns to be displayed.
* `FROM` identifies the table containing those columns.

### Syntax

```sql
SELECT * | {[DISTINCT] column | expression [alias], ...}
FROM table;
```

---

## 1.5 – Selecting All Columns

```sql
SELECT *
FROM departments;
```

---

## 1.6 – Selecting Specific Columns

```sql
SELECT department_id, location_id
FROM departments;
```

---

## 1.7 – Writing SQL Statements

* SQL statements are not case-sensitive.
* SQL statements can be written on one or multiple lines.
* Keywords cannot be abbreviated or split across lines.
* Clauses are usually placed on separate lines.
* Indentation improves readability.
* In `psql`, statements must end with a semicolon (`;`).
* Semicolons are required when executing multiple SQL statements.

---

## 1.8 – Arithmetic Expressions

You can create expressions using:

| Operator | Description |
| -------- | ----------- |
| `*`      | Multiply    |
| `/`      | Divide      |
| `+`      | Add         |
| `-`      | Subtract    |

---

## 1.9 – Using Arithmetic Operators

```sql
SELECT last_name, salary, salary + 300
FROM employees;
```

---

## 1.10 – Operator Precedence

```sql
SELECT last_name, salary, 12*salary+100
FROM employees;

SELECT last_name, salary, 12*(salary+100)
FROM employees;
```

* Parentheses control execution order.

---

## 1.11 – Defining a NULL Value

* NULL represents unavailable, unassigned, unknown, or inapplicable value.
* NULL is NOT the same as zero or a blank space.

```sql
SELECT last_name, job_id, salary, commission_pct
FROM employees;
```

---

## 1.12 – NULL Values in Arithmetic Expressions

Arithmetic expressions containing NULL evaluate to NULL.

```sql
SELECT last_name, 12*salary*commission_pct
FROM employees;
```

---

## 1.13 – Defining a Column Alias

A column alias:

* Renames a column heading
* Is useful with calculations
* Follows the column name
* May use optional `AS`
* Requires double quotes if:

  * Contains spaces
  * Contains special characters
  * Is case-sensitive

---

## 1.14 – Using Column Aliases

```sql
SELECT last_name AS name, commission_pct comm
FROM employees;

SELECT last_name "Name", salary*12 "Annual Salary"
FROM employees;
```

---

## 1.15 – Concatenation Operator

* Links columns or strings
* Represented by `||`
* Produces character expression

```sql
SELECT last_name || job_id AS "Employees"
FROM employees;
```

---

## 1.16 – Literal Character Strings

* Literals are characters, numbers, or dates included in SELECT.
* Date and character literals must use single quotes.
* Output appears once per row.

---

## 1.17 – Using Literal Character Strings

```sql
SELECT last_name || ' is a ' || job_id
AS "Employee Details"
FROM employees;
```

---

## 1.18 – Duplicate Rows

By default, all rows (including duplicates) are displayed.

```sql
SELECT department_id
FROM employees;

SELECT DISTINCT department_id
FROM employees;
```

---

## 1.19 – Displaying Table Structure

* Use the Connections tree → Columns tab
* Or use:

```sql
\d employees
```

---

## 1.20 – Quiz

Identify the SELECT statements that execute successfully:

```sql
SELECT first_name, last_name, job_id, salary*12
AS Yearly Sal
FROM employees;

SELECT first_name, last_name, job_id, salary*12
yearly sal
FROM employees;

SELECT first_name, last_name, job_id, salary AS
yearly sal
FROM employees;

SELECT first_name+last_name AS name, job_Id,
salary*12 yearly sal
FROM employees;
```

---

## 1.21 – Summary

In this lesson, you learned how to:

* Write a SELECT statement that:

  * Returns all rows and columns
  * Returns specified columns
  * Uses column aliases

### Final Syntax Reminder

```sql
SELECT * | {[DISTINCT] column | expression [alias], ...}
FROM table;
```

---
Here is **Chapter 2 converted into Markdown**, slide-by-slide, based on the uploaded file .

---

# Chapter 2 – Restricting and Sorting Data

---

## 2.1 – Title

# Restricting and Sorting Data

---

## 2.2 – Objectives

After completing this lesson, you should be able to:

* Limit the rows retrieved by a query
* Sort the rows retrieved by a query
* Use substitution variables to restrict and sort output at run time

---

## 2.3 – Limiting Rows Using a Selection

Example requirement:

> Retrieve all employees in department 90.

---

## 2.4 – Limiting the Rows That Are Selected

* Use the `WHERE` clause to restrict rows.
* The `WHERE` clause follows the `FROM` clause.

### Syntax

```sql
SELECT * | {[DISTINCT] column | expression [alias], ...}
FROM table
[WHERE condition(s)];
```

---

## 2.5 – Using the WHERE Clause

```sql
SELECT employee_id, last_name, job_id, department_id
FROM employees
WHERE department_id = 90;
```

---

## 2.6 – Character Strings and Dates

* Character strings and dates must use **single quotation marks**.
* Character comparisons are case-sensitive.
* Date comparisons are format-sensitive.
* Default date format: `DD-MON-YYYY`

```sql
SELECT last_name
FROM employees
WHERE hire_date = '17-FEB-96';
```

---

## 2.7 – Comparison Operators

| Operator        | Meaning                        |
| --------------- | ------------------------------ |
| =               | Equal to                       |
| >               | Greater than                   |
| >=              | Greater than or equal to       |
| <               | Less than                      |
| <=              | Less than or equal to          |
| <>              | Not equal to                   |
| BETWEEN ... AND | Between two values (inclusive) |
| IN (set)        | Match any value in list        |
| LIKE            | Pattern match                  |
| IS NULL         | Is null value                  |

---

## 2.8 – Using Comparison Operators

```sql
SELECT last_name, salary
FROM employees
WHERE salary <= 3000;
```

---

## 2.9 – BETWEEN Operator

Use `BETWEEN` for range conditions.

```sql
SELECT last_name, salary
FROM employees
WHERE salary BETWEEN 2500 AND 3500;
```

---

## 2.10 – IN Operator

Use `IN` to test membership in a list.

```sql
SELECT employee_id, last_name, salary, manager_id
FROM employees
WHERE manager_id IN (100, 101, 201);
```

---

## 2.11 – LIKE Operator

Use `LIKE` for wildcard searches.

* `%` → zero or many characters
* `_` → one character

```sql
SELECT first_name
FROM employees
WHERE first_name LIKE 'S%';
```

---

## 2.12 – Combining Wildcards

```sql
SELECT last_name
FROM employees
WHERE last_name LIKE '_o%';
```

You can use `ESCAPE` to search for actual `%` or `_`.

---

## 2.13 – Using NULL Conditions

Test for null values using `IS NULL`.

```sql
SELECT last_name, manager_id
FROM employees
WHERE manager_id IS NULL;
```

---

## 2.14 – Logical Operators

| Operator | Meaning                            |
| -------- | ---------------------------------- |
| AND      | Both conditions must be true       |
| OR       | Either condition must be true      |
| NOT      | Returns TRUE if condition is false |

---

## 2.15 – Using the AND Operator

```sql
SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary >= 10000
AND job_id LIKE '%MAN%';
```

---

## 2.16 – Using the OR Operator

```sql
SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary >= 10000
OR job_id LIKE '%MAN%';
```

---

## 2.17 – Using the NOT Operator

```sql
SELECT last_name, job_id
FROM employees
WHERE job_id NOT IN ('IT_PROG', 'ST_CLERK', 'SA_REP');
```

---

## 2.18 – Rules of Precedence

Operator execution order:

1. Arithmetic operators
2. Concatenation
3. Comparison conditions
4. IS NULL, LIKE, IN
5. BETWEEN
6. Not equal to
7. NOT
8. AND
9. OR

Use parentheses to override precedence.

---

## 2.19 – Precedence Example

```sql
SELECT last_name, job_id, salary
FROM employees
WHERE job_id = 'SA_REP'
OR job_id = 'AD_PRES'
AND salary > 15000;
```

Corrected using parentheses:

```sql
SELECT last_name, job_id, salary
FROM employees
WHERE (job_id = 'SA_REP'
OR job_id = 'AD_PRES')
AND salary > 15000;
```

---

## 2.20 – ORDER BY Clause

Sort retrieved rows using `ORDER BY`.

* ASC → Ascending (default)
* DESC → Descending

```sql
SELECT last_name, job_id, department_id, hire_date
FROM employees
ORDER BY hire_date;
```

---

## 2.21 – Sorting Examples

### Descending Order

```sql
SELECT last_name, job_id, department_id, hire_date
FROM employees
ORDER BY hire_date DESC;
```

### Sorting by Alias

```sql
SELECT employee_id, last_name, salary*12 annsal
FROM employees
ORDER BY annsal;
```

---

## 2.22 – Sorting by Column Position

```sql
SELECT last_name, job_id, department_id, hire_date
FROM employees
ORDER BY 3;
```

---

## 2.23 – Sorting by Multiple Columns

```sql
SELECT last_name, department_id, salary
FROM employees
ORDER BY department_id, salary DESC;
```

---

## 2.24 – Quiz

Which are valid operators for the WHERE clause?

1. > =
2. IS NULL
3. !=
4. IS LIKE
5. IN BETWEEN
6. <>

---

## 2.25 – Summary

In this lesson, you learned how to:

* Use `WHERE` to restrict rows
* Use:

  * Comparison operators
  * BETWEEN
  * IN
  * LIKE
  * IS NULL
  * AND, OR, NOT
* Use `ORDER BY` to sort rows

### Final Syntax

```sql
SELECT * | {[DISTINCT] column | expression [alias], ...}
FROM table
[WHERE condition(s)]
[ORDER BY {column | expr | alias} [ASC | DESC]];
```

---

## 2.26 – Practice 2 Overview

This practice covers:

* Selecting data
* Restricting rows with WHERE
* Sorting rows with ORDER BY
* Using substitution variables for flexibility

---
---

# Chapter 3 – Using Single-Row Functions to Customize Output

---

## 3.1 – Title

# Using Single-Row Functions to Customize Output

---

## 3.2 – Objectives

After completing this lesson, you should be able to:

* Describe various types of SQL functions
* Use character, number, and date functions in `SELECT` statements

---

## 3.3 – SQL Functions Overview

A function:

* Accepts input arguments
* Performs an operation
* Returns a result value

```
Function(arg1, arg2, ..., argn) → Result
```

---

## 3.4 – Two Types of SQL Functions

### 1. Single-Row Functions

* Return one result per row

### 2. Multiple-Row Functions

* Return one result per set of rows

---

## 3.5 – Single-Row Functions

Single-row functions:

* Manipulate data items
* Accept arguments
* Return one value per row
* May modify data type
* Can be nested
* Accept column names or expressions

### Syntax

```sql
function_name [(arg1, arg2, ...)]
```

---

## 3.6 – Categories of Single-Row Functions

* Character functions
* Number functions
* Date functions
* Conversion functions
* General functions

---

# Character Functions

---

## 3.7 – Character Functions Types

### Case-Conversion Functions

* LOWER
* UPPER
* INITCAP

### Character-Manipulation Functions

* CONCAT
* SUBSTR
* LENGTH
* POSITION
* LPAD
* RPAD
* TRIM
* REPLACE

---

## 3.8 – Case-Conversion Functions

| Function                | Result     |
| ----------------------- | ---------- |
| `LOWER('SQL Course')`   | sql course |
| `UPPER('SQL Course')`   | SQL COURSE |
| `INITCAP('SQL Course')` | Sql Course |

---

## 3.9 – Using Case-Conversion Functions

```sql
SELECT employee_id, last_name, department_id
FROM employees
WHERE LOWER(last_name) = 'higgins';
```

Without LOWER, this would fail if case does not match.

---

## 3.10 – Character-Manipulation Functions

Examples:

```sql
SELECT LENGTH('HelloWorld');        -- 10
SELECT SUBSTR('HelloWorld',1,5);    -- Hello
SELECT POSITION('W' IN 'HelloWorld'); -- 6
SELECT CONCAT('Hello','World');     -- HelloWorld
SELECT REPLACE('JACK and JUE','J','BL');
SELECT TRIM('H' FROM 'HelloWorld'); -- elloWorld
```

Padding:

```sql
SELECT LPAD(salary,10,'*');
SELECT RPAD(salary,10,'*');
```

---

# Number Functions

---

## 3.11 – Number Functions

| Function | Purpose           |
| -------- | ----------------- |
| ROUND    | Rounds value      |
| TRUNC    | Truncates value   |
| MOD      | Returns remainder |

Examples:

```sql
SELECT ROUND(45.926,2);  -- 45.93
SELECT TRUNC(45.926,2);  -- 45.92
SELECT MOD(1600,300);    -- 100
```

---

## 3.12 – Using ROUND

```sql
SELECT ROUND(45.923,2),
       ROUND(45.923,0),
       ROUND(45.923,-1);
```

---

## 3.13 – Using TRUNC

```sql
SELECT TRUNC(45.923,2),
       TRUNC(45.923),
       TRUNC(45.923,-1);
```

---

## 3.14 – Using MOD

```sql
SELECT last_name, salary, MOD(salary,5000)
FROM employees
WHERE job_id = 'SA_REP';
```

---

# Working with Dates

---

## 3.15 – Date Basics

* Default display format: `DD-MON-YYYY`
* PostgreSQL stores dates internally as numeric values:

  * century
  * year
  * month
  * day
  * hour
  * minute
  * second

Example:

```sql
SELECT last_name, hire_date
FROM employees
WHERE hire_date < '01-FEB-88';
```

---

## 3.16 – RR Date Format

The `RR` format helps interpret 2-digit years correctly across centuries.

It adjusts century based on current year and given year.

---

## 3.17 – Using NOW()

```sql
SELECT NOW();
```

Returns:

* Current date
* Current time

---

## 3.18 – Date Arithmetic

You can:

* Add or subtract numbers from dates
* Subtract two dates
* Add hours (divide by 24)

---

## 3.19 – Using Arithmetic with Dates

```sql
SELECT last_name,
       (NOW() - hire_date)/7 AS weeks
FROM employees
WHERE department_id = 90;
```

---

# Summary

---

## 3.20 – Summary

In this lesson, you learned how to:

* Perform calculations using functions
* Modify individual data items
* Use:

  * Character functions
  * Number functions
  * Date functions
* Perform arithmetic on dates

---

## 3.21 – Practice 3 Overview

This practice includes:

* Displaying the current date
* Using numeric functions
* Using character functions
* Using date functions
* Calculating years and months of service

---

Here is **Chapter 4 converted into Markdown**, slide-by-slide, based on the uploaded file .

---

# Chapter 4 – Using Conversion Functions and Conditional Expressions

---

## 4.1 – Title

# Using Conversion Functions and Conditional Expressions

---

## 4.2 – Objectives

After completing this lesson, you should be able to:

* Describe various types of conversion functions available in SQL
* Use `TO_CHAR`, `TO_NUMBER`, and `TO_DATE`
* Apply conditional expressions in a `SELECT` statement

---

# Conversion Functions

---

## 4.3 – Data Type Conversion

### Two Types:

1. **Implicit Conversion**

   * Automatically done by database

2. **Explicit Conversion**

   * Done manually using conversion functions

---

# TO_CHAR Function (Dates)

---

## 4.4 – TO_CHAR with Dates

### Syntax

```sql id="8q21fm"
TO_CHAR(date, 'format_model')
```

Rules:

* Format model must be in single quotes
* Case-sensitive
* Can include valid date elements
* `fm` removes padding or leading zeros
* Format model separated by comma

---

## 4.5 – Date Format Model Elements

| Element | Meaning          |
| ------- | ---------------- |
| DY      | 3-letter day     |
| DAY     | Full day name    |
| DD      | Day of month     |
| MON     | 3-letter month   |
| MONTH   | Full month       |
| MM      | Numeric month    |
| YYYY    | Full year        |
| YEAR    | Year spelled out |

---

## 4.6 – Additional Format Elements

* Add literal text using double quotes:

```sql id="q4a2vs"
DD "of" MONTH
```

Example result:

```
12 of OCTOBER
```

* Time formatting:

```sql id="8zws3o"
HH24:MI:SS AM
```

---

## 4.7 – Using TO_CHAR with Dates

```sql id="1rzzto"
SELECT last_name,
       TO_CHAR(hire_date, 'fmDD Month YYYY') AS hiredate
FROM employees;
```

---

# TO_CHAR Function (Numbers)

---

## 4.8 – TO_CHAR with Numbers

### Syntax

```sql id="wxf98n"
TO_CHAR(number, 'format_model')
```

Common format elements:

| Element | Meaning               |
| ------- | --------------------- |
| 9       | Digit                 |
| 0       | Force zero            |
| .       | Decimal point         |
| ,       | Thousands separator   |
| $       | Dollar sign           |
| L       | Local currency symbol |

---

## 4.9 – Example: Formatting Salary

```sql id="rz81pl"
SELECT TO_CHAR(salary, '$99,999.00') AS salary
FROM employees
WHERE last_name = 'Ernst';
```

---

# TO_NUMBER and TO_DATE

---

## 4.10 – Conversion to Number and Date

### TO_NUMBER

```sql id="p6l8aa"
TO_NUMBER(char [, 'format_model'])
```

### TO_DATE

```sql id="9kplk0"
TO_DATE(char [, 'format_model'])
```

* `fx` modifier enforces exact match between value and format

---

## 4.11 – Using TO_DATE with RR Format

Find employees hired before 1990:

```sql id="0otbdm"
SELECT last_name,
       TO_CHAR(hire_date, 'DD-Mon-YYYY')
FROM employees
WHERE hire_date < 
      TO_DATE('01-Jan-1990','DD-Mon-YYYY');
```

---

# Nesting Functions

---

## 4.12 – Nesting Functions

* Functions can be nested to any level
* Evaluation happens from innermost outward

General structure:

```sql id="u23s9k"
F3(F2(F1(col,arg1),arg2),arg3)
```

---

## 4.13 – Nested Function Example

```sql id="8nvaxr"
SELECT last_name,
       UPPER(CONCAT(SUBSTR(last_name,1,8),'_US'))
FROM employees
WHERE department_id = 60;
```

---

# General Functions

---

## 4.14 – NULLIF Function

Compares two expressions:

* Returns NULL if equal
* Returns first expression if not equal

```sql id="i2w0bf"
SELECT first_name, LENGTH(first_name) expr1,
       last_name, LENGTH(last_name) expr2,
       NULLIF(LENGTH(first_name), LENGTH(last_name)) result
FROM employees;
```

---

## 4.15 – COALESCE Function

* Returns first non-null expression
* Can take multiple arguments
* More flexible than NVL

```sql id="3tksn2"
SELECT last_name, employee_id,
       COALESCE(
           TO_CHAR(commission_pct,'0.00'),
           TO_CHAR(manager_id,'9999'),
           'No commission and no manager'
       ) AS commission_or_manager
FROM employees;
```

---

# Conditional Expressions

---

## 4.16 – Conditional Expressions

Provide **IF-THEN-ELSE logic** inside SQL.

Main method:

* `CASE` expression

---

## 4.17 – CASE Expression Syntax

```sql id="o33r1t"
CASE expr
     WHEN comparison_expr1 THEN return_expr1
     WHEN comparison_expr2 THEN return_expr2
     ...
     ELSE else_expr
END
```

---

## 4.18 – Using CASE Expression

```sql id="v3eaq3"
SELECT last_name, job_id, salary,
       CASE job_id
            WHEN 'IT_PROG' THEN 1.10*salary
            WHEN 'ST_CLERK' THEN 1.15*salary
            WHEN 'SA_REP' THEN 1.20*salary
            ELSE salary
       END AS revised_salary
FROM employees;
```

Acts like:

```
IF job_id = 'IT_PROG' THEN increase 10%
IF job_id = 'ST_CLERK' THEN increase 15%
IF job_id = 'SA_REP' THEN increase 20%
ELSE no change
```

---

# Summary

---

## 4.19 – Summary

In this lesson, you learned how to:

* Alter date formats using `TO_CHAR`
* Convert data types using:

  * `TO_CHAR`
  * `TO_DATE`
  * `TO_NUMBER`
* Use:

  * `NULLIF`
  * `COALESCE`
* Implement conditional logic using `CASE`

---

## 4.20 – Practice 4 Overview

This practice includes:

* Using `TO_CHAR`
* Using `TO_DATE`
* Using date functions
* Writing queries with `CASE` expressions

---


Here is **Chapter 5 converted into Markdown**, slide-by-slide, based on the uploaded file .

---

# Chapter 5 – Reporting Aggregated Data Using Group Functions

---

## 5.1 – Title

# Reporting Aggregated Data Using Group Functions

---

## 5.2 – Objectives

After completing this lesson, you should be able to:

* Identify available group functions
* Describe how group functions work
* Group data using the `GROUP BY` clause
* Restrict grouped results using the `HAVING` clause

---

# What Are Group Functions?

---

## 5.3 – Definition

Group functions:

* Operate on sets of rows
* Return **one result per group**

Example:

* Maximum salary in EMPLOYEES table
* Average salary per department

---

## 5.4 – Types of Group Functions

* `AVG`
* `COUNT`
* `MAX`
* `MIN`
* `SUM`
* `STDDEV`
* `VARIANCE`

---

## 5.5 – Group Function Syntax

```sql id="gq72fp"
SELECT group_function(column), ...
FROM table
[WHERE condition]
[ORDER BY column];
```

---

# Using Group Functions

---

## 5.6 – AVG and SUM

Used only with numeric data.

```sql id="qlo4rn"
SELECT AVG(salary),
       MAX(salary),
       MIN(salary),
       SUM(salary)
FROM employees
WHERE job_id LIKE '%REP%';
```

---

## 5.7 – MIN and MAX

Can be used with:

* Numeric
* Character
* Date data types

```sql id="y9v5kt"
SELECT MIN(hire_date),
       MAX(hire_date)
FROM employees;
```

---

## 5.8 – COUNT Function

### COUNT(*)

Returns total number of rows.

### COUNT(expression)

Returns number of non-null values.

```sql id="4kz5mv"
SELECT COUNT(commission_pct)
FROM employees
WHERE department_id = 80;

SELECT COUNT(*)
FROM employees
WHERE department_id = 50;
```

---

## 5.9 – DISTINCT with COUNT

```sql id="du3kcx"
SELECT COUNT(DISTINCT department_id)
FROM employees;
```

Returns number of unique department IDs.

---

## 5.10 – Group Functions and NULL Values

* Group functions ignore NULL values.
* Use `COALESCE` to include NULLs.

```sql id="lpa8rb"
SELECT AVG(commission_pct)
FROM employees;

SELECT AVG(COALESCE(commission_pct,0))
FROM employees;
```

---

# GROUP BY Clause

---

## 5.11 – Creating Groups

Example:

> Average salary per department

---

## 5.12 – GROUP BY Syntax

```sql id="d39gnt"
SELECT column, group_function(column)
FROM table
[WHERE condition]
[GROUP BY group_by_expression]
[ORDER BY column];
```

---

## 5.13 – Using GROUP BY

All non-aggregate columns in SELECT must appear in GROUP BY.

```sql id="u0kp19"
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id;
```

---

## 5.14 – GROUP BY Without Selecting Column

The GROUP BY column does not have to appear in SELECT.

```sql id="1kzmjo"
SELECT AVG(salary)
FROM employees
GROUP BY department_id;
```

---

## 5.15 – Grouping by Multiple Columns

```sql id="o3gtu1"
SELECT department_id, job_id, SUM(salary)
FROM employees
WHERE department_id > 40
GROUP BY department_id, job_id
ORDER BY department_id;
```

---

# Illegal Group Queries

---

## 5.16 – Incorrect Usage Examples

❌ Missing GROUP BY:

```sql id="37h6qn"
SELECT department_id, COUNT(last_name)
FROM employees;
```

✔ Correct:

```sql id="9bjs6f"
SELECT department_id, COUNT(last_name)
FROM employees
GROUP BY department_id;
```

---

❌ Column not in GROUP BY:

```sql id="mn4hwr"
SELECT department_id, job_id, COUNT(last_name)
FROM employees
GROUP BY department_id;
```

✔ Fix:

* Add `job_id` to GROUP BY
  OR
* Remove `job_id` from SELECT

---

# HAVING Clause

---

## 5.17 – Why HAVING?

* `WHERE` filters rows
* `HAVING` filters groups
* Cannot use group functions in WHERE

---

## 5.18 – HAVING Syntax

```sql id="5c0mnx"
SELECT column, group_function
FROM table
[WHERE condition]
[GROUP BY group_by_expression]
[HAVING group_condition]
[ORDER BY column];
```

---

## 5.19 – Using HAVING

```sql id="rk13az"
SELECT department_id, MAX(salary)
FROM employees
GROUP BY department_id
HAVING MAX(salary) > 10000;
```

---

## 5.20 – HAVING with WHERE

```sql id="2oxp0k"
SELECT job_id, SUM(salary) AS payroll
FROM employees
WHERE job_id NOT LIKE '%REP%'
GROUP BY job_id
HAVING SUM(salary) > 13000
ORDER BY SUM(salary);
```

Execution order:

1. WHERE filters rows
2. GROUP BY groups rows
3. HAVING filters groups

---

# Nesting Group Functions

---

## 5.21 – Nested Group Functions

Display maximum average salary:

```sql id="v05azc"
SELECT MAX(AVG(salary))
FROM employees
GROUP BY department_id;
```

---

# Quiz

---

## 5.22 – Quiz

Identify correct guidelines:

1. You cannot use a column alias in GROUP BY.
2. GROUP BY column must be in SELECT clause.
3. WHERE can exclude rows before grouping.
4. GROUP BY ensures ordering.
5. If using group function, you cannot select individual columns.

---

# Summary

---

## 5.23 – Summary

In this lesson, you learned how to:

* Use group functions:

  * `COUNT`
  * `MAX`
  * `MIN`
  * `SUM`
  * `AVG`
* Use `GROUP BY`
* Use `HAVING`
* Filter rows before grouping with `WHERE`

---

## 5.24 – Practice 5 Overview

This practice includes:

* Writing queries with group functions
* Grouping data for multiple results
* Filtering groups using HAVING

---

Here is **Chapter 6 converted into Markdown**, slide-by-slide, based on the uploaded file .

---

# Chapter 6 – Displaying Data from Multiple Tables

---

## 6.1 – Title

# Displaying Data from Multiple Tables

---

## 6.2 – Objectives

After completing this lesson, you should be able to:

* Write `SELECT` statements accessing multiple tables
* Use equijoins and nonequijoins
* Join a table to itself (self-join)
* Use OUTER joins
* Generate Cartesian products

---

# Why Joins?

---

## 6.3 – Obtaining Data from Multiple Tables

Data is often stored in separate tables:

* `EMPLOYEES`
* `DEPARTMENTS`
* `LOCATIONS`
* `JOB_GRADES`

To retrieve related data → **JOIN tables**

---

# Types of Joins (SQL:1999 Standard)

---

## 6.4 – Join Types

### Natural Joins

* `NATURAL JOIN`
* `USING`
* `ON`

### OUTER Joins

* `LEFT OUTER JOIN`
* `RIGHT OUTER JOIN`
* `FULL OUTER JOIN`

### Cross Joins

* `CROSS JOIN`

---

# SQL Join Syntax

---

## 6.5 – General Join Syntax

```sql
SELECT table1.column, table2.column
FROM table1
     [NATURAL JOIN table2]
     [JOIN table2 USING (column)]
     [JOIN table2 ON (condition)]
     [LEFT | RIGHT | FULL OUTER JOIN table2 ON (condition)]
     [CROSS JOIN table2];
```

---

# Qualifying Columns

---

## 6.6 – Ambiguous Column Names

If two tables share the same column name:

* Use **table prefixes**
* Or use **table aliases**

Example:

```sql
SELECT e.employee_id, d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
```

Table aliases:

* Shorter
* Cleaner
* More readable

---

# NATURAL JOIN

---

## 6.7 – NATURAL JOIN

* Automatically joins columns with same name
* Must have same data type
* Matches ALL columns with identical names

```sql
SELECT department_id, department_name,
       location_id, city
FROM departments
NATURAL JOIN locations;
```

⚠ Risky if unexpected column names match.

---

# USING Clause

---

## 6.8 – USING Clause

Use when:

* Columns share name
* You want to join on specific column

```sql
SELECT employee_id, last_name,
       location_id, department_id
FROM employees
JOIN departments
USING (department_id);
```

Rules:

* Do not qualify column in USING
* Cannot combine NATURAL and USING

---

## 6.9 – USING with Aliases

```sql
SELECT l.city, d.department_name
FROM locations l
JOIN departments d
USING (location_id)
WHERE d.location_id = 1400;
```

---

# ON Clause

---

## 6.10 – ON Clause

* Most flexible
* Explicit join condition
* Clear separation from WHERE

```sql
SELECT e.employee_id, e.last_name,
       e.department_id, d.location_id
FROM employees e
JOIN departments d
ON (e.department_id = d.department_id);
```

---

## 6.11 – Three-Way Join

```sql
SELECT employee_id, city, department_name
FROM employees e
JOIN departments d
ON d.department_id = e.department_id
JOIN locations l
ON d.location_id = l.location_id;
```

---

## 6.12 – Additional Conditions

Using AND:

```sql
SELECT e.employee_id, e.last_name
FROM employees e
JOIN departments d
ON (e.department_id = d.department_id)
AND e.manager_id = 149;
```

Using WHERE:

```sql
SELECT e.employee_id, e.last_name
FROM employees e
JOIN departments d
ON (e.department_id = d.department_id)
WHERE e.manager_id = 149;
```

---

# Self Join

---

## 6.13 – Joining a Table to Itself

Scenario:

* `manager_id` references `employee_id`

```sql
SELECT worker.last_name AS emp,
       manager.last_name AS mgr
FROM employees worker
JOIN employees manager
ON worker.manager_id = manager.employee_id;
```

---

# Nonequijoins

---

## 6.14 – Nonequijoins

Join using conditions other than equals.

Example:
Assign salary grades.

```sql
SELECT e.last_name, e.salary, j.grade_level
FROM employees e
JOIN job_grades j
ON e.salary BETWEEN j.lowest_sal
               AND j.highest_sal;
```

---

# OUTER JOINS

---

## 6.15 – INNER vs OUTER

* INNER JOIN → matched rows only
* LEFT OUTER → all rows from left table
* RIGHT OUTER → all rows from right table
* FULL OUTER → all rows from both

---

## 6.16 – LEFT OUTER JOIN

```sql
SELECT e.last_name,
       e.department_id,
       d.department_name
FROM employees e
LEFT OUTER JOIN departments d
ON e.department_id = d.department_id;
```

Returns:

* All employees
* Even those without department

---

## 6.17 – RIGHT OUTER JOIN

```sql
SELECT e.last_name,
       d.department_id,
       d.department_name
FROM employees e
RIGHT OUTER JOIN departments d
ON e.department_id = d.department_id;
```

Returns:

* All departments
* Even those without employees

---

## 6.18 – FULL OUTER JOIN

```sql
SELECT e.last_name,
       d.department_id,
       d.department_name
FROM employees e
FULL OUTER JOIN departments d
ON e.department_id = d.department_id;
```

Returns:

* All employees
* All departments
* Matched and unmatched rows

---

# Cartesian Products

---

## 6.19 – What Is a Cartesian Product?

Occurs when:

* Join condition missing
* Join condition invalid
* Every row of table A joins every row of table B

Rows = A × B

---

## 6.20 – CROSS JOIN

Explicit Cartesian product:

```sql
SELECT last_name, department_name
FROM employees
CROSS JOIN departments;
```

---

# Quiz

---

## 6.21 – Quiz

PostgreSQL supports which join types?

1. Equijoins
2. Nonequijoins
3. Left OUTER
4. Right OUTER
5. Full OUTER
6. Self joins
7. Natural joins
8. Cartesian products

---

# Summary

---

## 6.22 – Summary

In this lesson, you learned how to:

* Use equijoins
* Use nonequijoins
* Use self-joins
* Use OUTER joins
* Use cross joins
* Use NATURAL joins
* Avoid Cartesian products

---

## 6.23 – Practice 6 Overview

This practice includes:

* Writing equijoins
* Performing outer joins
* Performing self joins
* Adding conditions

---


Here is **Chapter 7 converted into Markdown**, slide-by-slide, based on the uploaded file .

---

# Chapter 7 – Using Subqueries to Solve Queries

---

## 7.1 – Title

# Using Subqueries to Solve Queries

---

## 7.2 – Objectives

After completing this lesson, you should be able to:

* Define subqueries
* Describe problems solved using subqueries
* List types of subqueries
* Write single-row and multiple-row subqueries

---

# What Is a Subquery?

---

## 7.3 – Solving a Problem with a Subquery

Example problem:

> Who earns more than Abel?

Steps:

1. Find Abel’s salary
2. Compare all salaries against it

The first query becomes the **subquery**.

---

# Subquery Syntax

---

## 7.4 – Basic Syntax

* The **subquery executes first**
* The result is passed to the main query

```sql id="sq1xw8"
SELECT select_list
FROM table
WHERE expr operator
      (SELECT select_list
       FROM table);
```

---

## 7.5 – Example Subquery

```sql id="o8n22k"
SELECT last_name, salary
FROM employees
WHERE salary >
      (SELECT salary
       FROM employees
       WHERE last_name = 'Abel');
```

Execution:

* Subquery returns Abel’s salary
* Main query filters salaries greater than it

---

# Subquery Guidelines

---

## 7.6 – Best Practices

* Always enclose subqueries in parentheses
* Place subqueries on right side for readability
* Match operator type:

  * Single-row operator → single-row subquery
  * Multiple-row operator → multiple-row subquery

---

# Types of Subqueries

---

## 7.7 – Two Main Types

### 1. Single-Row Subqueries

* Return exactly one row

### 2. Multiple-Row Subqueries

* Return more than one row

---

# Single-Row Subqueries

---

## 7.8 – Single-Row Operators

Used when subquery returns one value:

| Operator | Meaning          |
| -------- | ---------------- |
| =        | Equal            |
| >        | Greater than     |
| >=       | Greater or equal |
| <        | Less than        |
| <=       | Less or equal    |
| <>       | Not equal        |

---

## 7.9 – Example: Single-Row Subquery

```sql id="t4r9sx"
SELECT last_name, job_id, salary
FROM employees
WHERE job_id =
      (SELECT job_id
       FROM employees
       WHERE last_name = 'Taylor')
AND salary >
      (SELECT salary
       FROM employees
       WHERE last_name = 'Taylor');
```

---

## 7.10 – Using Group Functions in Subqueries

```sql id="nz7p1k"
SELECT last_name, job_id, salary
FROM employees
WHERE salary =
      (SELECT MIN(salary)
       FROM employees);
```

Subquery returns minimum salary.

---

## 7.11 – Subquery with HAVING

```sql id="3asx11"
SELECT department_id, MIN(salary)
FROM employees
GROUP BY department_id
HAVING MIN(salary) >
       (SELECT MIN(salary)
        FROM employees
        WHERE department_id = 50);
```

Execution order:

1. Subquery runs first
2. Main query groups
3. HAVING filters groups

---

## 7.12 – Common Mistake

❌ Using single-row operator with multi-row result:

```sql id="r9x2pb"
SELECT employee_id, last_name
FROM employees
WHERE salary =
      (SELECT MIN(salary)
       FROM employees
       GROUP BY department_id);
```

Problem:

* Subquery returns multiple rows
* `=` expects one value

---

## 7.13 – Subquery Returning No Rows

```sql id="l00kzp"
SELECT last_name, job_id
FROM employees
WHERE job_id =
      (SELECT job_id
       FROM employees
       WHERE last_name = 'Haas');
```

If subquery returns nothing:

* Main query returns no rows

---

# Multiple-Row Subqueries

---

## 7.14 – Multiple-Row Operators

| Operator | Meaning               |
| -------- | --------------------- |
| IN       | Equal to any value    |
| ANY      | Compare to any value  |
| ALL      | Compare to all values |

---

## 7.15 – Using ANY

```sql id="s2kwef"
SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary < ANY
      (SELECT salary
       FROM employees
       WHERE job_id = 'IT_PROG')
AND job_id <> 'IT_PROG';
```

Condition:

* Salary less than at least one IT_PROG salary

---

## 7.16 – Using ALL

```sql id="5vwe88"
SELECT employee_id, last_name, job_id, salary
FROM employees
WHERE salary < ALL
      (SELECT salary
       FROM employees
       WHERE job_id = 'IT_PROG')
AND job_id <> 'IT_PROG';
```

Condition:

* Salary less than every IT_PROG salary

---

# NULL Issues in Subqueries

---

## 7.17 – NULL with NOT IN

```sql id="nd9s8c"
SELECT emp.last_name
FROM employees emp
WHERE emp.employee_id NOT IN
      (SELECT mgr.manager_id
       FROM employees mgr);
```

⚠ If subquery contains NULL:

* Entire comparison may fail

Safer alternative:

* Use `NOT EXISTS`

---

# Quiz

---

## 7.18 – Quiz

Using a subquery is equivalent to performing two sequential queries and using the result of the first as input for the second.

1. True
2. False

---

# Summary

---

## 7.19 – Summary

In this lesson, you learned how to:

* Identify when subqueries are needed
* Write single-row subqueries
* Write multiple-row subqueries
* Use:

  * `IN`
  * `ANY`
  * `ALL`
* Avoid common operator mismatches

---

## 7.20 – Practice 7 Overview

This practice includes:

* Writing subqueries with unknown criteria
* Finding values in one set but not another
* Combining subqueries with grouping

---


Here is **Chapter 8 converted into Markdown**, slide-by-slide, based on the uploaded file .

---

# Chapter 8 – Using the Set Operators

---

## 8.1 – Title

# Using the Set Operators

---

## 8.2 – Objectives

After completing this lesson, you should be able to:

* Describe set operators
* Combine multiple queries into a single query
* Control the order of returned rows

---

# What Are Set Operators?

---

## 8.3 – Set Operators Overview

Set operators combine the results of two or more `SELECT` statements.

Main operators:

* `UNION`
* `UNION ALL`
* `INTERSECT`
* `MINUS`

---

# Set Operator Guidelines

---

## 8.4 – Rules for Using Set Operators

1. The number of columns in each `SELECT` must match.
2. Corresponding columns must have compatible data types.
3. Parentheses can change execution order.
4. `ORDER BY` can appear only once — at the very end.

---

## 8.5 – Behavior of Set Operators

* Duplicate rows are eliminated automatically
  (except in `UNION ALL`)
* Column names come from the first query
* Results are sorted ascending by default (except `UNION ALL`)

---

# Tables Used

---

## 8.6 – Tables Used in This Chapter

* `EMPLOYEES` – current employees
* `JOB_HISTORY` – previous job records

---

# UNION

---

## 8.7 – UNION Operator

* Combines results of two queries
* Removes duplicate rows

```
Query A
UNION
Query B
```

---

## 8.8 – Example: UNION

Display current and previous job details:

```sql id="u81xnm"
SELECT employee_id, job_id
FROM employees
UNION
SELECT employee_id, job_id
FROM job_history;
```

Result:

* Each employee appears once
* Duplicates removed

---

# UNION ALL

---

## 8.9 – UNION ALL Operator

* Combines results
* Keeps duplicates

---

## 8.10 – Example: UNION ALL

```sql id="4k8zvn"
SELECT employee_id, job_id, department_id
FROM employees
UNION ALL
SELECT employee_id, job_id, department_id
FROM job_history
ORDER BY employee_id;
```

Result:

* Includes duplicates
* Faster than UNION

---

# INTERSECT

---

## 8.11 – INTERSECT Operator

* Returns rows common to both queries

---

## 8.12 – Example: INTERSECT

Employees who returned to same job:

```sql id="y2me8r"
SELECT employee_id, job_id
FROM employees
INTERSECT
SELECT employee_id, job_id
FROM job_history;
```

Result:

* Only matching rows

---

# MINUS

---

## 8.13 – MINUS Operator

* Returns rows in first query
* Excludes rows present in second query

---

## 8.14 – Example: MINUS

Employees who never changed jobs:

```sql id="9pwx4t"
SELECT employee_id
FROM employees
MINUS
SELECT employee_id
FROM job_history;
```

---

# Matching SELECT Statements

---

## 8.15 – Matching Columns Example

Using `UNION` with missing columns:

```sql id="q89vxy"
SELECT location_id,
       department_name AS "Department",
       TO_CHAR(NULL) AS "Warehouse location"
FROM departments
UNION
SELECT location_id,
       TO_CHAR(NULL) AS "Department",
       state_province
FROM locations;
```

Important:

* Data types must match
* Use conversion functions when needed

---

## 8.16 – Matching with Different Data Types

```sql id="wq78pa"
SELECT employee_id, job_id, salary
FROM employees
UNION
SELECT employee_id, job_id, 0
FROM job_history;
```

---

# ORDER BY with Set Operators

---

## 8.17 – ORDER BY Rules

* Can appear only once
* Must be placed at the very end
* Applies to the combined result
* Refers only to columns of first SELECT

Example:

```sql id="k37ntp"
SELECT employee_id, job_id
FROM employees
UNION
SELECT employee_id, job_id
FROM job_history
ORDER BY employee_id;
```

---

# Quiz

---

## 8.18 – Quiz

Identify correct guidelines:

1. SELECT lists must match in number
2. Parentheses cannot change execution order
3. Data types must match
4. ORDER BY can be used multiple times

---

# Summary

---

## 8.19 – Summary

In this lesson, you learned how to use:

* `UNION` → distinct rows
* `UNION ALL` → include duplicates
* `INTERSECT` → common rows
* `MINUS` → difference between sets
* `ORDER BY` at the end only

---

## 8.20 – Practice 8 Overview

In this practice, you:

* Use `UNION`
* Use `INTERSECT`
* Use `MINUS`
* Build compound queries

---
Here is **Chapter 9 converted into Markdown**, slide-by-slide, based on the uploaded file .

---

# Chapter 9 – Manipulating Data

---

## 9.1 – Title

# Manipulating Data

---

## 9.2 – Objectives

After completing this lesson, you should be able to:

* Describe Data Manipulation Language (DML) statements
* Insert rows into a table
* Update rows in a table
* Delete rows from a table
* Control transactions

---

# Data Manipulation Language (DML)

---

## 9.3 – What Is DML?

DML statements are used to:

* Add new rows
* Modify existing rows
* Remove rows

A **transaction**:

* A collection of DML statements
* Forms one logical unit of work

---

# INSERT Statement

---

## 9.4 – Adding a New Row

Used to insert new data into a table.

---

## 9.5 – INSERT Syntax

```sql id="ins01"
INSERT INTO table [(column1, column2, ...)]
VALUES (value1, value2, ...);
```

* Inserts one row at a time
* Column list is optional (but recommended)

---

## 9.6 – Example: INSERT

```sql id="ins02"
INSERT INTO departments
(department_id, department_name, manager_id, location_id)
VALUES (280, 'Corporate Tax', 100, 1700);
```

---

## 9.7 – Inserting Without Column List

```sql id="ins03"
INSERT INTO departments
VALUES (290, 'Data Analytics', 102, 1800);
```

⚠ Risky if table structure changes.

---

## 9.8 – Inserting NULL Values

Method 1: Explicit NULL

```sql id="ins04"
INSERT INTO departments
VALUES (300, 'Strategy', NULL, 1700);
```

Method 2: Omit column (if allowed)

```sql id="ins05"
INSERT INTO departments (department_id, department_name, location_id)
VALUES (310, 'Innovation', 1700);
```

---

## 9.9 – Inserting Special Values

Use functions:

```sql id="ins06"
INSERT INTO employees
(employee_id, first_name, last_name, hire_date, job_id)
VALUES (999, 'John', 'Smith', NOW(), 'IT_PROG');
```

---

## 9.10 – Inserting Rows from Another Table

```sql id="ins07"
INSERT INTO sales_reps (id, name, salary)
SELECT employee_id, last_name, salary
FROM employees
WHERE job_id = 'SA_REP';
```

---

# UPDATE Statement

---

## 9.11 – UPDATE Syntax

```sql id="upd01"
UPDATE table
SET column1 = value1,
    column2 = value2
WHERE condition;
```

⚠ Without WHERE → updates ALL rows.

---

## 9.12 – Example: UPDATE

```sql id="upd02"
UPDATE employees
SET salary = salary * 1.10
WHERE department_id = 60;
```

---

## 9.13 – Updating Multiple Columns

```sql id="upd03"
UPDATE employees
SET job_id = 'SA_REP',
    salary = 6000
WHERE employee_id = 113;
```

---

## 9.14 – Using Subquery in UPDATE

```sql id="upd04"
UPDATE employees
SET salary =
    (SELECT MAX(salary)
     FROM employees)
WHERE job_id = 'IT_PROG';
```

---

# DELETE Statement

---

## 9.15 – DELETE Syntax

```sql id="del01"
DELETE FROM table
WHERE condition;
```

⚠ Without WHERE → deletes ALL rows.

---

## 9.16 – Example: DELETE

```sql id="del02"
DELETE FROM departments
WHERE department_name = 'Strategy';
```

---

## 9.17 – DELETE with Subquery

```sql id="del03"
DELETE FROM employees
WHERE department_id =
      (SELECT department_id
       FROM departments
       WHERE department_name = 'Public Relations');
```

---

# Transaction Control

---

## 9.18 – Transactions

Transaction includes:

* INSERT
* UPDATE
* DELETE

Changes are temporary until committed.

---

## 9.19 – COMMIT

```sql id="txn01"
COMMIT;
```

* Makes changes permanent
* Ends current transaction

---

## 9.20 – ROLLBACK

```sql id="txn02"
ROLLBACK;
```

* Undoes changes
* Reverts to last COMMIT

---

## 9.21 – SAVEPOINT

```sql id="txn03"
SAVEPOINT savepoint_name;
```

Allows partial rollback:

```sql id="txn04"
ROLLBACK TO savepoint_name;
```

---

# Transaction Flow

---

## 9.22 – Transaction Behavior

After DML:

* You can:

  * COMMIT
  * ROLLBACK
* DDL (CREATE, DROP, ALTER) auto-commits

---

# Summary

---

## 9.23 – Summary

In this lesson, you learned how to:

* Insert rows (`INSERT`)
* Update rows (`UPDATE`)
* Delete rows (`DELETE`)
* Control transactions using:

  * `COMMIT`
  * `ROLLBACK`
  * `SAVEPOINT`

---

## 9.24 – Practice 9 Overview

This practice includes:

* Inserting data
* Updating data
* Deleting data
* Using transaction control

---
Here is **Chapter 10 converted into Markdown**, based on the uploaded file .

---

# Chapter 10 – Creating and Managing Tables

---

## 10.1 – Title

# Creating and Managing Tables

---

## 10.2 – Objectives

After completing this lesson, you should be able to:

* Create tables
* Describe table structure
* Modify table structure
* Delete tables
* Create and manage constraints

---

# Data Definition Language (DDL)

---

## 10.3 – What Is DDL?

DDL statements:

* Define database objects
* Automatically commit changes

Common DDL commands:

* `CREATE`
* `ALTER`
* `DROP`
* `TRUNCATE`
* `RENAME`
* `COMMENT`

---

# CREATE TABLE

---

## 10.4 – CREATE TABLE Syntax

```sql id="crt01"
CREATE TABLE table_name (
    column_name datatype [DEFAULT expression],
    column_name datatype,
    ...
);
```

---

## 10.5 – Datatypes (Common Examples)

| Datatype     | Description            |
| ------------ | ---------------------- |
| INTEGER      | Whole numbers          |
| NUMERIC(p,s) | Fixed precision number |
| VARCHAR(n)   | Variable-length text   |
| CHAR(n)      | Fixed-length text      |
| DATE         | Date value             |
| TIMESTAMP    | Date + time            |

---

## 10.6 – Example: CREATE TABLE

```sql id="crt02"
CREATE TABLE departments (
    department_id INTEGER,
    department_name VARCHAR(30),
    manager_id INTEGER,
    location_id INTEGER
);
```

---

## 10.7 – DEFAULT Values

```sql id="crt03"
CREATE TABLE employees (
    employee_id INTEGER,
    first_name VARCHAR(20),
    hire_date DATE DEFAULT NOW()
);
```

If no hire date provided → current date used.

---

# Constraints

---

## 10.8 – What Are Constraints?

Constraints enforce data integrity.

Types:

* NOT NULL
* UNIQUE
* PRIMARY KEY
* FOREIGN KEY
* CHECK

---

## 10.9 – NOT NULL Constraint

```sql id="con01"
CREATE TABLE employees (
    employee_id INTEGER NOT NULL,
    last_name VARCHAR(25) NOT NULL
);
```

Prevents NULL values.

---

## 10.10 – UNIQUE Constraint

```sql id="con02"
CREATE TABLE employees (
    email VARCHAR(50) UNIQUE
);
```

Prevents duplicate values.

---

## 10.11 – PRIMARY KEY

* Unique
* Not null
* One per table

```sql id="con03"
CREATE TABLE departments (
    department_id INTEGER PRIMARY KEY,
    department_name VARCHAR(30)
);
```

---

## 10.12 – FOREIGN KEY

Enforces relationship between tables.

```sql id="con04"
CREATE TABLE employees (
    employee_id INTEGER PRIMARY KEY,
    department_id INTEGER,
    FOREIGN KEY (department_id)
        REFERENCES departments(department_id)
);
```

---

## 10.13 – CHECK Constraint

```sql id="con05"
CREATE TABLE employees (
    salary NUMERIC(8,2),
    CHECK (salary > 0)
);
```

Ensures condition is met.

---

# ALTER TABLE

---

## 10.14 – ALTER TABLE Syntax

```sql id="alt01"
ALTER TABLE table_name
ADD column_name datatype;
```

---

## 10.15 – Add Column Example

```sql id="alt02"
ALTER TABLE employees
ADD commission_pct NUMERIC(4,2);
```

---

## 10.16 – Modify Column

```sql id="alt03"
ALTER TABLE employees
ALTER COLUMN salary TYPE NUMERIC(10,2);
```

---

## 10.17 – Drop Column

```sql id="alt04"
ALTER TABLE employees
DROP COLUMN commission_pct;
```

---

# DROP TABLE

---

## 10.18 – DROP TABLE

```sql id="drop01"
DROP TABLE table_name;
```

* Removes table permanently
* All data lost

---

# TRUNCATE TABLE

---

## 10.19 – TRUNCATE

```sql id="trn01"
TRUNCATE TABLE table_name;
```

* Removes all rows
* Faster than DELETE
* Structure remains

---

# RENAME

---

## 10.20 – Rename Table

```sql id="ren01"
ALTER TABLE old_table_name
RENAME TO new_table_name;
```

---

# COMMENT

---

## 10.21 – Add Comment

```sql id="cmt01"
COMMENT ON TABLE employees
IS 'Stores employee details';
```

---

# Summary

---

## 10.22 – Summary

In this lesson, you learned how to:

* Create tables using `CREATE TABLE`
* Define constraints:

  * NOT NULL
  * UNIQUE
  * PRIMARY KEY
  * FOREIGN KEY
  * CHECK
* Modify tables using `ALTER TABLE`
* Remove tables using `DROP`
* Clear data using `TRUNCATE`
* Rename tables
* Add comments

---

Here is **Chapter 11 converted into Markdown**, based on the uploaded file .

---

# Chapter 11 – Creating Other Schema Objects

---

## 11.1 – Title

# Creating Other Schema Objects

---

## 11.2 – Objectives

After completing this lesson, you should be able to:

* Create views
* Create sequences
* Create indexes
* Create synonyms

---

# Database Objects Overview

---

## 11.3 – Schema Objects

A schema can contain:

* Tables
* Views
* Sequences
* Indexes
* Synonyms

These objects help with:

* Data abstraction
* Performance
* Security
* Simplifying queries

---

# Views

---

## 11.4 – What Is a View?

A **view**:

* Is a virtual table
* Is based on a query
* Does not store data itself
* Simplifies complex queries

---

## 11.5 – CREATE VIEW Syntax

```sql id="v01"
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table
WHERE condition;
```

---

## 11.6 – Example: Create View

```sql id="v02"
CREATE VIEW emp_dept_view AS
SELECT e.employee_id,
       e.last_name,
       d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
```

---

## 11.7 – Using a View

```sql id="v03"
SELECT *
FROM emp_dept_view;
```

View behaves like a table.

---

## 11.8 – Replacing a View

```sql id="v04"
CREATE OR REPLACE VIEW emp_dept_view AS
SELECT employee_id, last_name
FROM employees;
```

---

## 11.9 – Dropping a View

```sql id="v05"
DROP VIEW emp_dept_view;
```

---

# Sequences

---

## 11.10 – What Is a Sequence?

A **sequence**:

* Generates unique numbers
* Often used for primary keys

---

## 11.11 – CREATE SEQUENCE

```sql id="s01"
CREATE SEQUENCE emp_seq
START WITH 1
INCREMENT BY 1;
```

---

## 11.12 – Using a Sequence

```sql id="s02"
INSERT INTO employees
(employee_id, first_name, last_name)
VALUES (NEXTVAL('emp_seq'), 'John', 'Smith');
```

---

## 11.13 – Modify Sequence

```sql id="s03"
ALTER SEQUENCE emp_seq
INCREMENT BY 10;
```

---

## 11.14 – Drop Sequence

```sql id="s04"
DROP SEQUENCE emp_seq;
```

---

# Indexes

---

## 11.15 – What Is an Index?

An **index**:

* Improves query performance
* Created on frequently searched columns
* Speeds up SELECT operations

---

## 11.16 – CREATE INDEX

```sql id="i01"
CREATE INDEX emp_last_name_idx
ON employees(last_name);
```

---

## 11.17 – When to Create Indexes

Create indexes on:

* Columns frequently used in WHERE
* Columns used in JOIN
* Columns used in ORDER BY

Avoid indexing:

* Small tables
* Columns frequently updated

---

## 11.18 – Drop Index

```sql id="i02"
DROP INDEX emp_last_name_idx;
```

---

# Synonyms

---

## 11.19 – What Is a Synonym?

A **synonym**:

* Alternative name for an object
* Simplifies object access
* Useful for long object names

---

## 11.20 – Create Synonym

```sql id="syn01"
CREATE SYNONYM emp
FOR employees;
```

---

## 11.21 – Drop Synonym

```sql id="syn02"
DROP SYNONYM emp;
```

---

# Summary

---

## 11.22 – Summary

In this lesson, you learned how to:

* Create and manage views
* Create and use sequences
* Improve performance with indexes
* Simplify access using synonyms

---
Below is **Pages 313–333 converted into Markdown**, based strictly on the document content .

---

# Appendix C – PostgreSQL Join Syntax



---

## 1 – Title

# Postgres Join Syntax

---

## 2 – Objectives

After completing this appendix, you should be able to:

* Write `SELECT` statements to access data from more than one table using:

  * Equijoins
  * Nonequijoins
* Join a table to itself using a self-join
* View data that does not meet join conditions using outer joins
* Generate a Cartesian product of rows from two or more tables

---

## 3 – Obtaining Data from Multiple Tables

Data often resides in separate tables such as:

* `EMPLOYEES`
* `DEPARTMENTS`

To retrieve related information → use joins.

---

## 4 – Cartesian Products

A Cartesian product is formed when:

* A join condition is omitted
* A join condition is invalid
* All rows in table A join with all rows in table B

To avoid Cartesian products:

* Always include a valid join condition in the `WHERE` clause

---

## 5 – Generating a Cartesian Product

Example:

If:

* EMPLOYEES = 20 rows
* DEPARTMENTS = 8 rows

Then:

```
20 × 8 = 160 rows
```

---

## 6 – Types of PostgreSQL-Proprietary Joins

* Equijoin
* Nonequijoin
* Outer join
* Self-join

---

## 7 – PostgreSQL Join Syntax (Traditional)

Use the `WHERE` clause for join conditions:

```sql
SELECT table1.column, table2.column
FROM table1, table2
WHERE table1.column1 = table2.column2;
```

Guidelines:

* Write join condition in `WHERE`
* Prefix column names if duplicated across tables

---

## 8 – Qualifying Ambiguous Column Names

* Use table prefixes for duplicate column names
* Table prefixes can improve clarity and performance
* Use table aliases for shorter names

Example:

```sql
SELECT e.employee_id, d.department_name
FROM employees e, departments d
WHERE e.department_id = d.department_id;
```

* Use column aliases if needed to distinguish identical column names

---

## 9 – Equijoins

An equijoin:

* Uses equality operator (`=`)
* Typically matches:

  * Foreign key
  * Primary key

---

## 10 – Retrieving Records with Equijoins

```sql
SELECT e.employee_id,
       e.last_name,
       e.department_id,
       d.department_id,
       d.location_id
FROM employees e, departments d
WHERE e.department_id = d.department_id;
```

---

## 11 – Equijoin Example

```sql
SELECT d.department_id,
       d.department_name,
       d.location_id,
       l.city
FROM departments d, locations l
WHERE d.location_id = l.location_id;
```

---

## 12 – Additional Search Conditions

Using `AND`:

```sql
SELECT d.department_id,
       d.department_name,
       l.city
FROM departments d, locations l
WHERE d.location_id = l.location_id
AND d.department_id IN (20, 50);
```

---

## 13 – Joining More Than Two Tables

To join **n tables**, you need **n − 1 join conditions**.

Example:

To join 3 tables → minimum 2 join conditions.

Tables:

* EMPLOYEES
* DEPARTMENTS
* LOCATIONS

---

## 14 – Nonequijoins

A nonequijoin:

* Uses conditions other than equality
* Often uses `BETWEEN`

Example scenario:

`JOB_GRADES` defines:

* `LOWEST_SAL`
* `HIGHEST_SAL`

Used to assign grade levels.

---

## 15 – Nonequijoin Example

```sql
SELECT e.last_name,
       e.salary,
       j.grade_level
FROM employees e, job_grades j
WHERE e.salary
BETWEEN j.lowest_sal AND j.highest_sal;
```

---

## 16 – Returning Records with No Direct Match (Outer Joins)

Example:

Some departments may not have employees.

To include such rows → use outer joins.

---

## 17 – LEFT OUTER JOIN (Traditional PostgreSQL Syntax)

Using proprietary syntax:

```sql
SELECT e.last_name,
       d.department_id,
       d.department_name
FROM employees e, departments d
WHERE e.department_id = d.department_id(+);
```

(Conceptual example – includes unmatched departments.)

---

## 18 – RIGHT OUTER JOIN

Returns all rows from the right table, matched or not.

---

## 19 – FULL OUTER JOIN

Returns:

* All rows from both tables
* Matching and non-matching rows

---

## 20 – Self-Join

Joining a table to itself:

```sql
SELECT worker.last_name AS employee,
       manager.last_name AS manager
FROM employees worker,
     employees manager
WHERE worker.manager_id = manager.employee_id;
```

---

## 22 – Summary

In this appendix, you learned how to:

* Write equijoins using `WHERE`
* Write nonequijoins using `BETWEEN`
* Avoid Cartesian products
* Use table aliases
* Join multiple tables
* Perform self-joins
* Understand outer join behavior

---

Here is your **complete structured SQL Handbook (Chapters 1–11 + Appendix C)** compiled into a single clean Markdown document.

You can copy this directly into a `.md` file (e.g., `PostgreSQL_SQL_Fundamentals.md`).

---

# PostgreSQL SQL Fundamentals Handbook

*(Chapters 1–11 + Appendix C)*

---

# Table of Contents

1. Retrieving Data Using SELECT
2. Restricting and Sorting Data
3. Single-Row Functions
4. Conversion Functions & Conditional Expressions
5. Group Functions
6. Joins (SQL Standard Syntax)
7. Subqueries
8. Set Operators
9. Data Manipulation (DML)
10. Data Definition (DDL) & Constraints
11. Other Schema Objects (Views, Sequences, Indexes, Synonyms)
12. Appendix C – PostgreSQL Join Syntax (Traditional)

---

# 1. Retrieving Data Using SELECT

## Basic Syntax

```sql
SELECT * | {[DISTINCT] column | expression [alias], ...}
FROM table;
```

## Selecting Columns

```sql
SELECT department_id, location_id
FROM departments;
```

## Column Aliases

```sql
SELECT last_name AS name,
       salary*12 AS annual_salary
FROM employees;
```

## Arithmetic Expressions

```sql
SELECT last_name, salary, salary+300
FROM employees;
```

## DISTINCT

```sql
SELECT DISTINCT department_id
FROM employees;
```

---

# 2. Restricting and Sorting Data

## WHERE Clause

```sql
SELECT employee_id, last_name
FROM employees
WHERE department_id = 90;
```

## Comparison Operators

* =, >, <, >=, <=, <>
* BETWEEN
* IN
* LIKE
* IS NULL

## Logical Operators

* AND
* OR
* NOT

## ORDER BY

```sql
SELECT last_name, salary
FROM employees
ORDER BY salary DESC;
```

---

# 3. Single-Row Functions

## Categories

* Character
* Number
* Date
* Conversion
* General

## Character Functions

```sql
LOWER()
UPPER()
INITCAP()
SUBSTR()
LENGTH()
REPLACE()
```

Example:

```sql
SELECT UPPER(last_name)
FROM employees;
```

## Number Functions

```sql
ROUND()
TRUNC()
MOD()
```

## Date Functions

```sql
SELECT NOW();
```

Date arithmetic:

```sql
SELECT (NOW() - hire_date)/7 AS weeks
FROM employees;
```

---

# 4. Conversion Functions & Conditional Expressions

## TO_CHAR

```sql
TO_CHAR(date, 'DD-MON-YYYY')
TO_CHAR(number, '$99,999.00')
```

## TO_DATE

```sql
TO_DATE('01-Jan-1990','DD-Mon-YYYY')
```

## TO_NUMBER

```sql
TO_NUMBER(char, 'format_model')
```

## CASE Expression

```sql
SELECT last_name,
       CASE job_id
            WHEN 'IT_PROG' THEN salary*1.10
            ELSE salary
       END AS revised_salary
FROM employees;
```

## COALESCE

```sql
SELECT COALESCE(commission_pct, 0)
FROM employees;
```

---

# 5. Group Functions

## Common Group Functions

* AVG
* COUNT
* MAX
* MIN
* SUM

Example:

```sql
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id;
```

## HAVING Clause

```sql
SELECT department_id, MAX(salary)
FROM employees
GROUP BY department_id
HAVING MAX(salary) > 10000;
```

---

# 6. Joins (SQL:1999 Syntax)

## INNER JOIN

```sql
SELECT e.employee_id, d.department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
```

## LEFT OUTER JOIN

```sql
SELECT e.last_name, d.department_name
FROM employees e
LEFT OUTER JOIN departments d
ON e.department_id = d.department_id;
```

## FULL OUTER JOIN

```sql
SELECT *
FROM employees e
FULL OUTER JOIN departments d
ON e.department_id = d.department_id;
```

## Self Join

```sql
SELECT worker.last_name, manager.last_name
FROM employees worker
JOIN employees manager
ON worker.manager_id = manager.employee_id;
```

---

# 7. Subqueries

## Single-Row Subquery

```sql
SELECT last_name
FROM employees
WHERE salary >
      (SELECT salary
       FROM employees
       WHERE last_name = 'Abel');
```

## Multiple-Row Subqueries

Operators:

* IN
* ANY
* ALL

Example:

```sql
SELECT employee_id
FROM employees
WHERE salary < ALL
      (SELECT salary
       FROM employees
       WHERE job_id = 'IT_PROG');
```

---

# 8. Set Operators

## UNION

```sql
SELECT employee_id FROM employees
UNION
SELECT employee_id FROM job_history;
```

## UNION ALL

Includes duplicates.

## INTERSECT

Returns common rows.

## MINUS

Returns rows from first query not in second.

Rules:

* Same number of columns
* Compatible data types
* ORDER BY only at end

---

# 9. Data Manipulation (DML)

## INSERT

```sql
INSERT INTO departments
(department_id, department_name)
VALUES (280, 'Corporate Tax');
```

## INSERT with Subquery

```sql
INSERT INTO sales_reps
SELECT employee_id, last_name, salary
FROM employees
WHERE job_id = 'SA_REP';
```

## UPDATE

```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department_id = 60;
```

## DELETE

```sql
DELETE FROM employees
WHERE employee_id = 113;
```

## Transaction Control

```sql
COMMIT;
ROLLBACK;
SAVEPOINT sp1;
ROLLBACK TO sp1;
```

---

# 10. Data Definition (DDL) & Constraints

## CREATE TABLE

```sql
CREATE TABLE departments (
    department_id INTEGER PRIMARY KEY,
    department_name VARCHAR(30)
);
```

## Constraints

* NOT NULL
* UNIQUE
* PRIMARY KEY
* FOREIGN KEY
* CHECK

Example:

```sql
salary NUMERIC(8,2)
CHECK (salary > 0)
```

## ALTER TABLE

```sql
ALTER TABLE employees
ADD commission_pct NUMERIC(4,2);
```

## DROP TABLE

```sql
DROP TABLE departments;
```

## TRUNCATE

```sql
TRUNCATE TABLE employees;
```

---

# 11. Other Schema Objects

## Views

```sql
CREATE VIEW emp_view AS
SELECT employee_id, last_name
FROM employees;
```

## Sequences

```sql
CREATE SEQUENCE emp_seq
START WITH 1
INCREMENT BY 1;
```

Use:

```sql
NEXTVAL('emp_seq')
```

## Indexes

```sql
CREATE INDEX emp_last_name_idx
ON employees(last_name);
```

## Synonyms

```sql
CREATE SYNONYM emp FOR employees;
```

---

# Appendix C – PostgreSQL Join Syntax (Traditional)

## Traditional Join (WHERE clause)

```sql
SELECT e.employee_id, d.department_name
FROM employees e, departments d
WHERE e.department_id = d.department_id;
```

## Cartesian Product

Occurs when:

* Join condition omitted
* Join condition invalid

## Nonequijoin

```sql
SELECT e.last_name, j.grade_level
FROM employees e, job_grades j
WHERE e.salary
BETWEEN j.lowest_sal AND j.highest_sal;
```

## Joining Multiple Tables

To join n tables → need n−1 join conditions.

---

# Final Notes

This handbook now contains:

* Core SQL querying
* Filtering & sorting
* Functions
* Aggregation
* Joins (modern + traditional)
* Subqueries
* Set operations
* DML
* DDL
* Schema objects
* Transaction management

---





