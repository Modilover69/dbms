## Procedure: Avg

```
DELIMITER //
CREATE FUNCTION CalculateAverage(x1 FLOAT, x2 FLOAT, x3 FLOAT, x4 FLOAT, x5 FLOAT)
RETURNS FLOAT
DETERMINISTIC
BEGIN
   DECLARE avg FLOAT;
   SET avg = (x1 + x2 + x3 + x4 + x5) / 5;
   RETURN avg;
END //
DELIMITER ;
```
Query OK, 0 rows affected (0.01 sec)

```
mysql> 

mysql> SELECT CalculateAverage(100, 1000000, -1000, -10000, -90) AS AVG;
+--------+
| AVG    |
+--------+
| 197802 |
+--------+
1 row in set (0.00 sec)
```
