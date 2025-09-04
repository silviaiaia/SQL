## SQL notebook

### Table of Contents
1. [select all data](#select-all-data)
2. [select one column](#select-one-column)
3. [select distinct values](#select-distinct-values)
4. [skip top 10 rolls and show 5 rolls at one time](#skip-top-10-rolls-and-show-5-rolls-at-one-time)
5. [use where as a filter](#use-where-as-a-filter)
6. [select words start with...](#select-words-start-with)
7. [set an order](#set-an-order)
8. [set groups](#set-gruops)
9. [calculate](#calculate)
10. [use AS to reset column names](#use-as-to-reset-column-names)
11. [when there are groups, use HAVING as a filter, not WHERE](#when-there-are-groups-use-having-as-a-filter-not-where)
12. [count rolls](#count-rolls)

### select all data
```sql
SELECT *
FROM table_name;
```
- `;` means an end

### select one column
```sql
SELECT column_name
FROM table_name;
```

### select distinct values
```sql
SELECT DISTINCT column_name
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

```sql
```





