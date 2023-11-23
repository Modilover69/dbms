## Function: Palindrome

```
delimiter $
create procedure palindrome (IN s VARCHAR(255), OUT r BOOL)
begin
    if (s <> reverse(s)) then
        select false;
    else
        select true;
    end if;
END$
```
Query OK, 0 rows affected (0.00 sec)

```
mysql> call palindrome('apaffpa', @r);
+-------+
| false |
+-------+
|     0 |
+-------+
1 row in set (0.00 sec)

Query OK, 0 rows affected (0.00 sec)

mysql>
```
