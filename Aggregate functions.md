```
mysql> use db_for_agg_fn
Database changed
mysql> select * from company;
+------+---------------------+------------+--------+
| id   | name                | role       | salary |
+------+---------------------+------------+--------+
|    1 | Darshan Soni        | CEO        |  10000 |
|    2 | Ninad Borawake      | Manager    |  20000 |
|    3 | Rohan Soni          | Safai wala |  30000 |
|    4 | Garima Negi         | Employee   |  40000 |
|    5 | Atharva Borkar      | Developer  |  10000 |
|    6 | Satyam Pokharna     | AIML dev   |  20000 |
|    7 | Satyam Pathak       | AIML dev   |  30000 |
|    8 | Abhay Dube          | Employee   |  40000 |
|    9 | Amit Agrawal        | Safai Wala |  10000 |
|   10 | Tavish Negi         | Safai Wala |  10000 |
|   11 | Krishnansh Vasaniya | AIML dev   |  20000 |
|   12 | Anvay Khedulkar     | Developer  |  30000 |
|   13 | Ajay Rathod         | Employee   |  40000 |
|   14 | Havva lokhandwala   | Developer  |  10000 |
+------+---------------------+------------+--------+
14 rows in set (0.06 sec)

mysql> select count(*) from company;
+----------+
| count(*) |
+----------+
|       14 |
+----------+
1 row in set (0.05 sec)

mysql> select role,count(*) from company group by role;
+------------+----------+
| role       | count(*) |
+------------+----------+
| CEO        |        1 |
| Manager    |        1 |
| Safai wala |        3 |
| Employee   |        3 |
| Developer  |        3 |
| AIML dev   |        3 |
+------------+----------+
6 rows in set (0.01 sec)

mysql> select role,count(*) from company group by role having role = "Safai wala";
+------------+----------+
| role       | count(*) |
+------------+----------+
| Safai wala |        3 |
+------------+----------+
1 row in set (0.00 sec)

mysql> select sum(salary) from company;
+-------------+
| sum(salary) |
+-------------+
|      320000 |
+-------------+
1 row in set (0.04 sec)

mysql> select role,sum(salary) from company group by role;
+------------+-------------+
| role       | sum(salary) |
+------------+-------------+
| CEO        |       10000 |
| Manager    |       20000 |
| Safai wala |       50000 |
| Employee   |      120000 |
| Developer  |       50000 |
| AIML dev   |       70000 |
+------------+-------------+
6 rows in set (0.00 sec)

mysql> select role,sum(salary) from company group by role having role= "Employee";
+----------+-------------+
| role     | sum(salary) |
+----------+-------------+
| Employee |      120000 |
+----------+-------------+
1 row in set (0.00 sec)

mysql> select max(salary) from company;
+-------------+
| max(salary) |
+-------------+
|       40000 |
+-------------+
1 row in set (0.00 sec)

mysql> select max(salary) from company group by role;
+-------------+
| max(salary) |
+-------------+
|       10000 |
|       20000 |
|       30000 |
|       40000 |
|       30000 |
|       30000 |
+-------------+
6 rows in set (0.04 sec)

mysql> select role,max(salary) from company group by role;
+------------+-------------+
| role       | max(salary) |
+------------+-------------+
| CEO        |       10000 |
| Manager    |       20000 |
| Safai wala |       30000 |
| Employee   |       40000 |
| Developer  |       30000 |
| AIML dev   |       30000 |
+------------+-------------+
6 rows in set (0.00 sec)

mysql> select name,max(salary) from company;
ERROR 1140 (42000): In aggregated query without GROUP BY, expression #1 of SELECT list contains nonaggregated column 'db_for_agg_fn.company.name'; this is incompatible with sql_mode=only_full_group_by
mysql> select max(salary) from company group by role having role="AIML dev";
+-------------+
| max(salary) |
+-------------+
|       30000 |
+-------------+
1 row in set (0.00 sec)

mysql> select min(salary) from company;
+-------------+
| min(salary) |
+-------------+
|       10000 |
+-------------+
1 row in set (0.00 sec)

mysql> select avg(salary) from company;
+-------------+
| avg(salary) |
+-------------+
|  22857.1429 |
+-------------+
1 row in set (0.04 sec)

mysql> select avg(salary) from company group by role;
+-------------+
| avg(salary) |
+-------------+
|  10000.0000 |
|  20000.0000 |
|  16666.6667 |
|  40000.0000 |
|  16666.6667 |
|  23333.3333 |
+-------------+
6 rows in set (0.04 sec)

mysql>
```
