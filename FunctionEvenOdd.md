```
DELIMITER $$

CREATE FUNCTION IsEvenOrOdd(number INT) RETURNS VARCHAR(4)
DETERMINISTIC
BEGIN

DECLARE res VARCHAR(10);

IF number % 2 = 0 THEN
SET res = 'Even';
ELSE
SET res = 'Odd';
END IF;
RETURN res;

END $$
DELIMETER ;
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
