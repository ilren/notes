explain select * from Task;
+----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+-------+
| id | select_type | table | partitions | type | possible_keys | key  | key_len | ref  | rows | filtered | Extra |
+----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+-------+
|  1 | SIMPLE      | Task  | NULL       | ALL  | NULL          | NULL | NULL    | NULL |    5 |   100.00 | NULL  |
+----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+-------+
1 row in set, 1 warning (0.00 sec)
它的输出格式细节可以关注 MySQL explain format(http://dev.mysql.com/doc/refman/5.6/en/explain-output.html)，
在输出中最要注意的是：

1. type：ALL是效率最差，最要注意的

2. key：是否有使用Key，key长度如何

3. Extra：最好不要出现filesort以及temporary，最主要是要关注在orderby和groupby。


SQL优化是个很复杂的过程，有可能出现拆东墙补西墙的情况：
比如给数据库表加入了索引之后，确实查询快了，可是存储空间加多了，插入删除操作耗时也增加了，如果在一个写多读少的系统中，执行这种优化可能会起到反效果。
所以优化完之后千万不能大意，要持续监控系统，防止出现引入新瓶颈的情况。