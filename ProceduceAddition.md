## Procedure: Addition 

```
DELIMITER //
CREATE FUNCTION AddNumbers(num1 INT, num2 INT) RETURNS INT
BEGIN
   DECLARE result INT;
   SET result = num1 + num2;
   RETURN result;
END //
DELIMITER;
```
Query OK, 0 rows affected (0.01 sec)
 
```
mysql> SELECT AddNumbers(-42, 420) AS Addition;
+----------+
| Addition |
+----------+
|      378 |
+----------+
1 row in set (0.00 sec)

Query OK, 0 rows affected (0.00 sec)
```
