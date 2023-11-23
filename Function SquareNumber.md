## Function: Square Number input from user 

```
DELIMITER //

CREATE FUNCTION SquareNumber(inputNumber INT) RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE result INT;
    SET result = inputNumber * inputNumber;
    RETURN result;
END //

DELIMITER ;
```
Query OK, 0 rows affected (0.01 sec)

Output:
```
mysql> select SquareNumber(9);
+-----------------+
| SquareNumber(9) |
+-----------------+
|              81 |
+-----------------+
1 row in set (0.00 sec)

mysql>
```
