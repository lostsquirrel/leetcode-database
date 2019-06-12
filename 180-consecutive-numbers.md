# 180. Consecutive Numbers
Write a SQL query to find all numbers that appear at least three times consecutively.

```
+----+-----+
| Id | Num |
+----+-----+
| 1  |  1  |
| 2  |  1  |
| 3  |  1  |
| 4  |  2  |
| 5  |  1  |
| 6  |  2  |
| 7  |  2  |
+----+-----+
```
For example, given the above `Logs` table, `1` is the only number that appears consecutively for at least three times.

```
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+
```

```sql
SELECT t.Num AS ConsecutiveNums FROM Logs t JOIN Logs t2 JOIN Logs t3 on t.Num = t2.Num AND t.Num = t3.Num AND t.Id + 1 = t2.Id AND t2.Id + 1 = t3.Id LIMIT 1
```
