# 596. Classes More Than 5 Students

There is a table `courses` with columns: student and class

Please list out all classes which have more than or equal to 5 students.

For example, the table:

```
+---------+------------+
| student | class      |
+---------+------------+
| A       | Math       |
| B       | English    |
| C       | Math       |
| D       | Biology    |
| E       | Math       |
| F       | Computer   |
| G       | Math       |
| H       | Math       |
| I       | Math       |
+---------+------------+
```
Should output:

```
+---------+
| class   |
+---------+
| Math    |
+---------+
```
```sql
SELECT count(class) as amount, class FROM courses group by class

SELECT class FROM
(
    SELECT count(class) as amount, class FROM
    (
        SELECT distinct student, class FROM courses
    ) as x group by class
) as a
WHERE amount >= 5


SELECT
    class
FROM
    (SELECT
        class, COUNT(DISTINCT student) AS num
    FROM
        courses
    GROUP BY class) AS temp_table
WHERE
    num >= 5
;
```
