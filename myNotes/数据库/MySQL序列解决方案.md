#####*注：因为技术能力所限，所有观点可能有疏漏甚至较严重错误，希望读者可以指正谢谢*
项目中需要使用序列，但是MySQL不支持，所以使用自定义序列表方式实现。
## 表结构如下：
```
CREATE TABLE `sequence` (
  `name` varchar(50) NOT NULL,
  `current_value` int(11) NOT NULL,
  `increment` int(11) NOT NULL DEFAULT '1',
  PRIMARY KEY (`name`)
) 
```
CURRRVAL与NEXTVAL使用自定义函数实现：

# 不加锁
### CURRRVAL函数
```
CREATE FUNCTION `currval`(seq_name VARCHAR(50)) 
RETURNS int(11)
BEGIN     
  DECLARE value INTEGER;     
  SET value = 0;     
  SELECT current_value INTO value     
  FROM sequence
  WHERE name = seq_name;
  RETURN value; 
END
```
### NEXTVAL函数
```
CREATE  FUNCTION `nextval`(seq_name VARCHAR(50)) RETURNS int(11)
    COMMENT '下一个值'
BEGIN
   UPDATE sequence SET current_value = current_value + increment WHERE name = seq_name;
   RETURN currval(seq_name);
END
```
到这里看起来很简单实现类，不过有个问题，```NEXTVAL```函数可能存在并发问题。试想下，如果```UPDATE```语句执行完成后还未执行```CURRVAL```，另一个线程执行了```NEXTVAL```，返回的值便出现问题。简单的解决方案是加悲观锁实现。
# 悲观锁
### NEXTVAL函数
```
CREATE  FUNCTION `nextval`(seq_name VARCHAR(50)) 
RETURNS int(11)
    COMMENT '下一个值'
BEGIN
   DECLARE value INTEGER;     
   SET value = 0;
   SELECT current_value INTO value FROM sequence WHERE name = seq_name for update;
   UPDATE sequence SET current_value = current_value + increment WHERE name = seq_name;
   RETURN value;
END
```