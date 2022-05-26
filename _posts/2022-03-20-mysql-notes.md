---
layout: post
title: SQL Notes
categories: [coding, SQL]
---


### JOIN vs. RIGHT JOIN vs. LEFT JOIN

Extracted from [this source](https://www.w3schools.com/sql/sql_join.asp)

* (INNER) JOIN: Returns records that have matching values in both tables

* LEFT (OUTER) JOIN: Returns all records from the left table, and the matched records from the right table

* RIGHT (OUTER) JOIN: Returns all records from the right table, and the matched records from the left table

* FULL (OUTER) JOIN: Returns all records when there is a match in either left or right table


![This is website](/media/inner_join.png "This is website")

### HAVING vs. WHERE

```sql
SELECT column_name(s)
FROM table_name
WHERE condition
GROUP BY column_name(s)
HAVING condition
ORDER BY column_name(s);
```
* `WHERE`: Like if after `SELECT xx FROM yy`
* `HAVING`: Only after every `GROUP BY`, it's like `WHERE` but for aggregate functions.

### 

