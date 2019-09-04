#EXPLAIN 

[参考官方文档：explain-output](https://dev.mysql.com/doc/refman/5.7/en/explain-output.html)
[参考网上博客：MySQL 性能优化神器 Explain 使用教程](https://www.xttblog.com/?p=3524)

- EXPLAIN说明：
>The EXPLAIN statement provides information about how MySQL executes statements. EXPLAIN works with SELECT, DELETE, INSERT, REPLACE, and UPDATE statements.
>
>EXPLAIN returns a row of information for each table used in the SELECT statement. It lists the tables in the output in the order that MySQL would read them while processing the statement. MySQL resolves all joins using a nested-loop join method. This means that MySQL reads a row from the first table, and then finds a matching row in the second table, the third table, and so on. When all tables are processed, MySQL outputs the selected columns and backtracks through the table list until a table is found for which there are more matching rows. The next row is read from this table and the process continues with the next table.  

- EXPLAIN 输出格式

