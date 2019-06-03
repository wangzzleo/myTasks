今天创建函数时候遇到一个问题，如下所示：
sql：
```
DROP FUNCTION IF EXISTS xxxxxxx;
DELIMITER $
CREATE FUNCTION xxxxxxx (seq_name VARCHAR(50))     
RETURNS INTEGER
CONTAINS SQL     
BEGIN     
  DECLARE value INTEGER;     
  SET value = 0;     
  SELECT current_value INTO value     
  FROM xxx
  WHERE name = seq_name;
  RETURN value;     
END$
DELIMITER ;
```
```This function has none of DETERMINISTIC, NO SQL, or READS SQL DATA in its declaration and binary log```
因为是在本地创建的，我本地数据库是MySQL8.0版本的。所以我想当然觉得是版本问题，我还在测试上试了下（MySQL5.7），结果能运行。我第一反应觉得是高版本创建语法可能严格点儿，所以我依照官方文档：
[CREATE PROCEDURE and CREATE FUNCTION Syntax](https://dev.mysql.com/doc/refman/8.0/en/create-procedure.html)
修改了语法，如下：
```
DROP FUNCTION IF EXISTS xxxxxxx;
DELIMITER $
CREATE FUNCTION xxxxxxx (seq_name VARCHAR(50))     
RETURNS INTEGER
COMMENT '下一个值'
MODIFIES SQL DATA
CONTAINS SQL     
BEGIN     
  DECLARE value INTEGER;     
  SET value = 0;     
  SELECT current_value INTO value     
  FROM xxx
  WHERE name = seq_name;
  RETURN value;     
END$
DELIMITER ;
```
结果还是不行。
最后还是借助搜索引擎解决的，解决办法如下：
[原文在此](https://www.cnblogs.com/fzng/p/7267002.html)
```
show variables like '%func%';  
+---------------------------------+-------+  
| Variable_name                   | Value |  
+---------------------------------+-------+  
| log_bin_trust_function_creators | OFF   |  
+---------------------------------+-------+  
1 row in set (0.00 sec)  
  
mysql> set global log_bin_trust_function_creators=1;  
Query OK, 0 rows affected (0.00 sec) 
```
是自定义函数功能未开启所致。
