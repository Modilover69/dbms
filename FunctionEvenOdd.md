```
DELIMETER //
CREATE FUNCTION IsEvenOrOdd(number INT) RETURNS VARCHAR(4)
BEGIN
DECLARE result VARCHAR(10);

IF number % 2 = 0 THEN
     SET result = 'Even';
ELSE
     SET result = 'Odd';
END IF;
     RETURN result;
END //
DELIMETER;
```
Query OK, 0 rows affected (0.01 sec)

```
mysql> SELECT IsEvenOrOdd(10);
+-----------------+
| IsEvenOrOdd(10) |
+-----------------+
| Even            |
+-----------------+
1 row in set (0.00 sec)

mysql> SELECT IsEvenOrOdd(21);
+-----------------+
| IsEvenOrOdd(21) |
+-----------------+
| Odd             |
+-----------------+
1 row in set (0.00 sec)
```
