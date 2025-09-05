## SQL notebook

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
13. [left join](#left-join)
14. [inner join](#inner-join)
15. [create table](#create-table)
16. [drop table](#drop-table)
17. [insert data](#insert-data)
18. [update date](#update-data)
19. [delete data](#delete-data)

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
- `<>` means exclude
- comparison operators : `>=` `<=` `OR` `AND` `BETWEEN AND` `IN`

> ```sql
> SELECT employee_id, name
> FROM employee
> WHERE employee_id = 101;
> ```

#### `IN` can replace `OR`
```sql
column1 = 'something' OR column1 = 'something'
```
can be simplified to 
```sql
column IN ('something', 'something')
```

> ```sql
> employee_id = 101 OR employee_id = 102 OR employee_id = 103 can be simplified to
> employee_id IN (101, 102, 103)
> ```

### select words start with...
```sql
SELECT column1, column2
FROM table_name
WHERE column1 LIKE 'A%';
WHERE column1 LIKE 'A_';
```
- `A%` means all words start with A (eg. Apple, Ann)
- `A_` means all words start with A and have a length of 2 characters (eg. Ad, At)

> ```sql
> SELECT employee_id, name
> FROM employee
> WHERE name LIKE 'P%';
> ```
>
> | employee_id | name |
> | :--- | :--- |
> | 101 | Potato |
> | 325 | Papaya |
> | 497 | Pistachio |

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

> ```sql
> SELECT employee_id, name, gender
> FROM employee
> GROUP BY gender
> ORDER BY employee_id;
> ```
>
> | employee_id | name | gender |
> | :--- | :--- | :--- |
> | 101 | Potato | male |
> | 102 | Tomato | male |
> | 325 | Papaya | male |
> | 103 | Biscuit | female |
> | 497 | Pistachio | female |

### calculate
```sql
SELECT AVG(column1), SUM(column1), MAX(column1), MIN(column1), COUNT(column1)
FROM table_name;
```
- `null` will be ignored when calculating average
- `COUNT` calculates the total number of **non-null** values in column1

> ```sql
> SELECT AVG(salary), SUM(salary), MAX(salary), MIN(salary), COUNT(salary)
> FROM salary;
> ```
>
> | AVG(salary) | SUM(salary) | MAX(salary) | MIN(salary) | COUNT(salary) |
> |:--- | :--- | :---| :--- | :--- |
> | 200 | 10000 | 5000 | 10 | 20 |

### use `AS` to reset column names
```sql
SELECT column1 AS new_column1,
       column2 AS new_column2
FROM table_name;
```

> ```sql
> SELECT employee_id AS e_id,
> FROM employee;
> ```

```sql
SELECT AVG(column1) AS Average,
       MAX(column1) AS Maximum
FROM table_name;
```

> ```sql
> SELECT AVG(salary) AS Average_salary
>        MAX(salary) AS Maximum_salary
> FROM salary;
> ```

### when there are groups, use `HAVING` as a filter, not `WHERE`
```sql
SELECT column1, column2 = new_column2
FROM table_name
GROUP BY column1
HAVING new_column2 = 'something'
ORDER BY new_column2 DESC;
```

> ```sql
> SELECT name, gender, department, employee_id
> FROM salary
> GROUP BY genger
> HAVING department = 'IT Division'
> ORDER BY employee_id
> ```
>
> | name | gender | department | employee_id |
> | :-- | :-- | :-- | :-- |
> | Potato | male | IT Division | 101 |
> | Biscuit | female | IT Division | 103 |
> | Pistachio | female | IT Division | 497 |

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

> ```sql
> SELECT DISTINCT country
> FROM employee;
> ```
>
> | country |
> | :---: |
> | Taiwan |
> | Australia |
> | USA |
> | Japan |

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

> ```sql
> SELECT COUNT(DISTINCT country)
> FROM country;
> ```
>
> | count(country) |
> | :---: |
> | 4 |

### left join

```sql
SELECT table1.column1, table2.column2
FROM table1
LEFT JOIN table2
ON table1.column3 = table2.column3
```
- refer table2 to table1
- find the values where table1.column1 matches table2.column2
- if no matched value is found in table2.column2, `null` will be filled in the blank

> ```sql
> SELECT employee.name, salary.salary
> FROM employee
> LEFT JOIN salary
> ON employee.employee_id = salary.employee_id
> ```
>
> | name | salary |
> | :--- | :--- |
> | Potato | 1000 |
> | Tomato | 2000 |
> | Pistachio | null |

### inner join

```sql
SELECT table1.column1, table2.column2
FROM table1
INNER JOIN table2
ON table1.column3 = table2.column3
```
- `INNER JOIN` will only show the values that are both matched in table1 and table2
- no `null` will be filled in

> ```sql
> SELECT employee.name, salary.salary
> FROM employee
> INNER JOIN salary
> ON employee.employee_id = salary.employee_id
> ```
>
> | name | salary |
> | :--- | :--- |
> | Potato | 1000 |
> | Tomato | 2000 |

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
>  CREATE TABLE years_of_service (
>        employee_id INT PRIMARY KEY,
>        name VARCHAR(100),
>        on_board_date DATE
>        years_of_service INT
> );
> ```
>
> | empolyee_id | name | on_board_date | years_of_service |
> | :-- | :-- | :-- | :-- |
> |  |  |  |  |
> |  |  |  |  |

- `name VARCHAR(100)` means storing text of up to 100 characters
- `PRIMARY KEY` ensures that all values in `student_id` is unique and no null values

### drop table

```sql
DROP TABLE table_name;
```

> [!NOTE]
> this will permanently delete the table

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

> ```sql
> INSERT INTO years_of_service (
>        employee_id,
>        name,
>        on_board_date,
>        years_of_service
> )
> VALUES (
>        101,
>        'Potato',
>        '2022-09-05',
>        3
> ),
>        (
>        102,
>        'Tomato',
>        '2020-09-05',
>        5
> );
> SELECT * FROM years_of_service;
> ```
>
> | empolyee_id | name | on_board_date | years_of_service |
> | :-- | :-- | :-- | :-- |
> | 101 | Potato | 2022-09-05 | 3 |
> | 102 | Tomato | 2020-09-05 | 5 |

### update data

```sql
UPDATE table_name
SET column1 = new_value1, column2 = new_value2
WHERE column3 = something;
```

> ```sql
> UPDATE years_of_service
> SET employee_id = '497', on_board_date = '2025-09-07'
> WHERE name = 'Pistachio';
> SELECT employee_id, name, on_board_date
> FROM years_of_service
> WHERE name = 'Pistachio';
>
> | employee_id | name | on_board_date |
> | :--- | :--- | :--- |
> | 497 | Pistachio | 2025-09-07 |

### delete data

```sql
DELETE FROM table_name
WHERE column1 = something;
```

> ```sql
> DELETE FROM employee
> WHERE employee_id = 104;
> ```












