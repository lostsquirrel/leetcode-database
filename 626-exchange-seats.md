# 626. Exchange Seats
Mary is a teacher in a middle school and she has a table `seat` storing students' names and their corresponding seat ids.

The column id is continuous increment.


Mary wants to change seats for the adjacent students.


Can you write a SQL query to output the result for Mary?


```
+---------+---------+
|    id   | student |
+---------+---------+
|    1    | Abbot   |
|    2    | Doris   |
|    3    | Emerson |
|    4    | Green   |
|    5    | Jeames  |
+---------+---------+
```
For the sample input, the output is:


```
+---------+---------+
|    id   | student |
+---------+---------+
|    1    | Doris   |
|    2    | Abbot   |
|    3    | Green   |
|    4    | Emerson |
|    5    | Jeames  |
+---------+---------+
```
Note:
If the number of students is odd, there is no need to change the last one's seat.

```sql
CREATE TABLE seat (
  id INT,
  student VARCHAR(50)
);

INSERT INTO seat VALUES (1, 'Abbot');   
INSERT INTO seat VALUES (2, 'Doris');   
INSERT INTO seat VALUES (3, 'Emerson');
INSERT INTO seat VALUES (4, 'Green');   
INSERT INTO seat VALUES (5, 'Jeames');

SELECT id ^ 1 FROM seat;

-- others solution 1
SELECT
    (CASE
        WHEN MOD(id, 2) != 0 AND counts != id THEN id + 1
        WHEN MOD(id, 2) != 0 AND counts = id THEN id
        ELSE id - 1
    END) AS id,
    student
FROM
    seat,
    (SELECT
        COUNT(*) AS counts
    FROM
        seat) AS seat_counts
ORDER BY id ASC;

-- others solution 2
SELECT
    s1.id, COALESCE(s2.student, s1.student) AS student
FROM
    seat s1
        LEFT JOIN
    seat s2 ON ((s1.id + 1) ^ 1) - 1 = s2.id
ORDER BY s1.id;
```
