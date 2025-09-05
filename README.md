## my SQL notebook

### Table of Contents
1. [select all data](#select-all-data)
2. [select one column](#select-one-column)
3. [skip top 10 rolls and show 5 rolls at one time](#skip-top-10-rolls-and-show-5-rolls-at-one-time)
4. [use where as a filter](#use-where-as-a-filter)
5. [select words start with...](#select-words-start-with)
6. [set an order](#set-an-order)
7. [set groups](#set-groups)
8. [calculate](#calculate)
9. [use AS to reset column names](#use-as-to-reset-column-names)
10. [when there are groups, use HAVING as a filter, not WHERE](#when-there-are-groups-use-having-as-a-filter-not-where)
11. [count rolls](#count-rolls)
12. [distinct values](#distinct-values)
13. [LEFT JOIN](#left-join)
14. [INNER JOIN](#inner-join)

## Querying Data

### select all data
```sql
SELECT *
FROM table_name;
```
- `*` means all value
- `;` means an end

### select one column
```sql
SELECT column_name
FROM table_name;
```

### skip top 10 rolls and show 5 rolls at one time
```sql
SELECT column1, column2
FROM table_name
LIMIT 5
OFFSET 10;
```

### use `where` as a filter
```sql
SELECT column1, column2
FROM table_name
WHERE column1 = 'something';
WHERE column1 <> 'something';
```
- `<>` means exclude <br/>
- comparison operators : `>=` `<=` `OR` `AND` `BETWEEN AND` `IN` 

#### `IN` can replace `OR`
```sql
column1 = 'something' OR column1 = 'someone'
```
can be simplified to 
```sql
column IN ('something', 'someone')
```

### select words start with...
```sql
SELECT column1, column2
FROM table_name
WHERE column1 LIKE 'A%';
WHERE column1 LIKE 'A_';
```
- `A%` means all words start with A (eg. Apple, Ann) <br />
- `A_` means all words start with A and have a length of 2 characters (eg. Ad, At)

### set an order
default order is ascending
```sql
SELECT column1, column2
FROM table_name
ORDER BY column1;
```
dscending order
```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 DESC;
```

### set groups
```sql
SELECT column1, column2
FROM table_name
GROUP BY column1
ORDER BY column2;
```

### calculate
```sql
SELECT AVG(column1), SUM(column1), MAX(column1), MIN(column1), COUNT(column1)
FROM table_name;
```

### use `AS` to reset column names
```sql
SELECT column1 AS new_column1,
       column2 AS new_column2
FROM table_name;
```
```sql
SELECT AVG(column1) AS Average,
       MAX(column1) AS Maximum
FROM table_name;
```

### when there are groups, use `HAVING` as a filter, not `WHERE`
```sql
SELECT column1, AVG(column2) AS Average
FROM table_name
GROUP BY column1
HAVING Average = 'something'
ORDER BY Average DESC;
```

### count rolls
```sql
SELECT COUNT(*)
FROM table_name;
```

```sql
SELECT COUNT(column1)
FROM table_name;
```
- blank values will be ignored

### distinct values

#### select distinct values

```sql
SELECT DISTINCT column1
FROM table_name;
```

#### select distinct values and ignore blank values

```sql
SELECT DISTINCT column1
FROM table_name
WHERE column1 IS NOT null
ORDER BY column1;
```

#### count the number of distinct values in column1

```sql
SELECT COUNT(DISTINCT column1)
FROM table_name;
```

### LEFT JOIN

```sql
SELECT table1.column1, table2.column2
FROM table1
LEFT JOIN table2
ON table1.column3 = table2.column3
```

- refer table2 to table1
- find the values where table1.column1 matches table2.column2
- if no matched value is found in table2.column2, `null` will be filled in the blank

### INNER JOIN

```sql
SELECT table1.column1, table2.column2
FROM table1
INNER JOIN table2
ON table1.column3 = table2.column3
```

- `INNER JOIN` will only show the values that are both matched in table1 and table2
- no `null` will be filled in

## Modifying Data

### create table

```sql
CREATE TABLE new_table_name (
       column1 datatype,
       column2 datatype,
       column3 datatype,
);
```

- `datatype` includes `INT` (integer), `VARCHAR` (text), `DATE`...

>  ```sql
>  CREATE TABLE students (
>        student_id INT PRIMARY KEY,
>        name VARCHAR(100),
>        birth_date DATE
> );
> ```

- `name VARCHAR(100)` means storing text of up to 100 characters
- `PRIMARY KEY` ensures that all values in `student_id` is unique and no null values

### drop table

```sql
DROP TABLE table_name;
```

- this will permanently delete the table

### insert data

```sql
INSERT INTO table_name (
       column1,
       column2,
       column3
)
VALUES (
       value1,
       value2,
       value3
);
```

> INSERT INTO students (
>        student_id,
>        name,
>        birth_date
> )
> VALUES (
>        101,
>        'Potato'
>        '2025-09-05
> ),
>        (
>        102,
>        'Tomato'
>        '2025-09-05'
> );
> SELECT * FROM students;
> ```

### update data

```sql
UPDATE table_name
SET column1 = new_value1, column2 = new_value2
WHERE column3 = something;
```

> ```sql
> UPDATE students
> SET student_id = '101', birth_date = '2025-09-05'
> WHERE name = 'Potato';
> ```











